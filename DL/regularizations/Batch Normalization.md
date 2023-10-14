#regularization, #FutureReturn
[Источник](https://arxiv.org/pdf/1502.03167.pdf)
## Описание
Нормирует вход слоя сети по каждому обучающиму mini-batch (то есть m > 1).

Эффекты слоя:
- решает проблему Internal Covariate Shift*, что **сильно ускоряет сходимость**;
- так же действует в качестве регулиризатора, что позволяет убрать или снизить влияние [[Dropout]];
- позволяет использовать saturated nonlinearties (например [[Sigmoid]]);
- позволяет использовать высокий learning rate без риска несходимости и более небрежную иницилизацию весов.

>По поводу того, где ставить ведутся дискуссии, но анализируя мнение в интернете люди ставят после функции активации
>Но нельзя не отметить, что авторы статьи ставят перед функцией активации(хотя далее сообщеет разработчик Keras, что автор статьи сейчас ставит после функции активации)
>[Обсуждение на stackoverflow](https://stackoverflow.com/questions/39691902/ordering-of-batch-normalization-and-dropout) также рассматривается и вопрос куда ставить [[Dropout]].

## Подробнее
Сходимость нейросети ускоряется, если на вход сети подаются нормализованные данные. То же самое верно и для "подсетей" нейросети (1 и более слоёв).

Для преобразования данных внутри слоёв сети данный слой используется два упрощения позволяющих решить задачу нормализации слоёв на всей статистики обучения:
1. Нормализировать каждую scalar input features независимо (var=1, mean=0);
2. Каждый мини-батч выдаёт оценку дисперсии и мат. ожидания для входа.

### Covariate Shift
**Covariate Shift** представляет из себя проблему при которой изменяется распределения входа нейросети, которое приводит к тому, что нужно подстраиваться под новое распределение, что замедляет обучение.

**Internal Covariate Shift** является той же проблемой только в масштабах "подсети" нейросети, то есть проблемой для одного или нескольких слоёв. Так после очередного gradient otimizer step распределение на выходе одного из слоёв может изменится, что заставит последующие подстраиваться.

### Метод
1. Принимаем на вход мини-батч выхода предыдущего слоя размера m>1.
2. Нормализируем все фичи отдельно для выхода предыдущего слоя с $d$ измерениями $x=(x^{(1)}, x^{(2)}, ..., x^{(d)})$.	$$\large\hat{x}^{(k)} = \frac {x^{(k)} − E[x^{(k)}]}{\sqrt{Var[x(k)]}}$$
3. Scale and shift the normalize values, используя trainable параметры $\gamma^{(k)}, \beta^{(k)}$, которые "учатся" восстановливать representation power of the model.
$$\large{\hat{y}^{(k)} = \gamma^{(k)}\hat{x}^{(k)} + \beta^{(k)}}$$
> Note. Нормализация входа слоя может приводить к изменению того что может представлять слой. Например, так сигмоиду можно перевести в линейный режим (значения близкие к нулю). Эту проблему и призвана решить линейная трансформация, представленная выше, которая способна репрезентовать идентичную.

**Алгоритм**:
Рассмотрим мини-батч $B={x_{1...m}}$. Опустим $k$, чтобы рассмотреть алгоритм относительно конкретной фичи.
![[algorithmBatchNorm.png|500]]
>The distributions of values of any $\hat{x}$ has the expected value of 0 and the variance of 1, as long as the elements of each mini-batch are sampled from **the same distribution**,and if we neglect $\epsilon$.

### Training
Производные для backprop. Для infernce мы также собираем экспоненциальное скользящие среднее мат. ожидания и дисперсии, представляющие из себя:
$M=M \times c+v \times (1-c)$, где $M$ скользящее среднее, $0< c < 1$, $v$ новый элемент. Я брал $c=0.9$.
![[gradBatchNorm.png|500]]

### Inference
Фиксируем параметры $\gamma, \beta$ и берём мат. ожидание и дисперсию, как скользящее среднее от значений при обучение. 
![[inferenceBatchNorm.png]]

## Code
```python
class BatchNorm(Module):

	 def __init__(self, num_features, eps=1e-8):
		 super().__init__()
		 self.eps = eps
		 self.gamma = np.ones((1, num_features))
		 self.beta = np.zeros((1, num_features))
		 self.sigma_mean = 1
		 self.mu_mean = 0

	 def forward(self, input):

		 if self._train:
			 assert input.shape[0] > 1, "Batch size need to be >1"
			 self._mu = np.mean(input, axis=0)
			 self._sigma = np.var(input, axis=0)
			 self.mu_mean = self.mu_mean*.9 + self._mu*.1
			 self.sigma_mean = self.sigma_mean*.9 + self._sigma*.1
			 self._input_norm = self._normalize(input, self._mu, self._sigma)
			 self.output = self.gamma*self._input_norm + self.beta
		 else:
			 self._input_norm = self._normalize(input, self.mu_mean, self.sigma_mean)
			 self.output = self.gamma*self._input_norm + self.beta
		 return self.output

 def backward(self, input, grad_output):
		 if self._train:
			 m = input.shape[0]
			 input_minus_mu = (input - self._mu)
			 dinput_norm = grad_output * self.gamma
			 dsigma = np.sum(dinput_norm*input_minus_mu*(-.5)*self.std_inv**3, axis=0)
			 dmu = np.sum(dinput_norm * (-self.std_inv), axis=0) \
				 + dsigma * np.mean(-2 * input_minus_mu, axis=0)
			 self.grad_gamma = np.sum(grad_output * self._input_norm, axis=0)
			 self.grad_beta = np.sum(grad_output, axis=0)
			 grad_input = dinput_norm*self.std_inv + dsigma*input_minus_mu/m + dmu/m
		 else:
			 self.grad_gamma = np.sum(grad_output * self._input_norm, axis=0)
			 self.grad_beta = np.sum(grad_output, axis=0)
			 grad_input = grad_output * self.gamma * self.std_inv
		return grad_input

	def parameters(self):
		 return [self.gamma, self.beta]

	 def grad_parameters(self):
		 return [self.grad_gamma, self.grad_beta]

	 def _normalize(self, input, mu, sigma):
		 self.std_inv = 1/np.sqrt(sigma + self.eps)
		 return (input - mu)*self.std_inv
```

## Batch-Normalized Convolution Networks
%%Перепроверить%%
Нормализируем также по каждому значенею матрицы feature maps, но обучаем $\gamma, \beta$ для каждого feature maps, а не для каждого его значения. 
