#activation 
[Источник 1](https://en.wikipedia.org/wiki/Softmax_function), [Источник 2](https://sgugger.github.io/a-simple-neural-net-in-numpy.html)
## Softmax
**Softmax** также известна, как **softargmax** или **normalized exponential function**. Softmax преобразует вектор из $K$ вещественных чисел в вероятностное распределение $K$ возможных исходов. Чаще всего softmax встречается, как активация на последнем слое в задачах многоклассовой классификации.
$$\sigma(z)_i=\frac{e^{z_i}}{\sum^{K}_{j=1}{e^{z_j}}} \quad,i=1,\dots,K$$
$$\sigma:\mathbb{R}^K \to (0,1)^K$$
Сумма элементов выходного вектор равна 1.  Softmax является аппроксимацией функции argmax.

### Backward
Если мы хотим продифференциировать $\sigma_i$ , то мы можем продифференцировать её по $K$ переменным. Пусть $p_i=\sigma(z)_i$
$$\frac{ \partial p_i}{\partial z_i}=\frac{e^{z_i}\sum^K_{j=1}{e^{z_j}} - e^{2z_i}}{(\sum^K_{j=1}{e^{z_j}})^2}=\frac{e^{z_i}}{\sum^K_{j=1}{e^{z_j}}}-\frac{e^{2z_i}}{(\sum^{K}_{j=1}{e^{z_j}})^2}=p_i(1-p_i)$$
для всех $i\neq j$, то:
$$\frac{\partial p_i}{\partial z_j}=-\frac{e^{z_i}e^{z_j}}{(\sum^{K}_{j=1}{e^{z_j}})^2}=-\frac{e^{z_i}}{\sum^{K}_{j=1}{e^{z_j}}}*\frac{e^{z_j}}{\sum^{K}_{j=1}{e^{z_j}}}=-p_ip_j$$
Пусть $l$ - некоторая функция, принимающая на вход выход softmax (например функция потерь). Тогда используя правило дифференцирование сложной функции (chain rule) получаем:
$$\frac{\partial l}{\partial z_i}=\sum_{j=1}^{K}\frac{\partial l}{\partial p_j}\frac{\partial p_j}{\partial z_i}=p_i(1-p_i)\frac{\partial l}{\partial p_i} - \sum_{i \neq j}p_ip_j\frac{\partial l}{\partial p_j}=$$
$$=p_i\frac{\partial l}{\partial p_i}-\sum_{j=1}^{K}{p_ip_j\frac{\partial l}{\partial p_j}}$$

### Temperature
Меняя температуру $\tau$ мы можем менять распределение вероятностей, а именно их соотношение, 
- при $\tau \rightarrow 0$, вероятность всех исходов кроме максимального уменьшается.
	- ![[Pasted image 20230311211009.png]]
- при $\tau \rightarrow \inf$, распределение стремится к равномерному (uniform)
	- ![[Pasted image 20230311211021.png]]

![[Pasted image 20230311210112.png]]

- diversity - разнообразие; 
- coherence - осмысленность (или согласованность)![[Pasted image 20230311210632.png|400]]

> Примечаение. [Визуализация](https://lena-voita.github.io/nlp_course/language_modeling.html#evaluation:~:text=Sampling%20with%20temperature).

### Code
```python
class Softmax(Module):
    def forward(self, input):
        self.output = self.softmax = self._softmax(input)
        return self.output

    def backward(self, input, grad_output):
        p = self.softmax
        grad_input = p * ( grad_output - (grad_output * p).sum(axis=1)[:, None] )
        return grad_input

    def _softmax(self, x):
        x = np.subtract(x, x.max(axis=1, keepdims=True))
        e_m = np.exp(x)
        sum_e = np.repeat(np.sum(e_m, axis=1), x.shape[-1]).reshape(*e_m.shape)
        return e_m/sum_e
```