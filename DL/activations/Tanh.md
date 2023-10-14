#activation 
[Источник](https://academy.yandex.ru/handbook/ml/article/pervoe-znakomstvo-s-polnosvyaznymi-nejrosetyami)
## **Tanh**, гиперболический тангенс
Tanh решает проблему несимметричности [[Sigmoid]] и также может быть записан через неё $tanh(x)=2 \times \alpha(2x)-1$.
$$\tanh(x) = \frac{\exp(x) - \exp(-x)}{\exp(x) + \exp(-x)}$$
$$\tanh: \mathbb{R} \to (-1, 1)$$
![[Pasted image 20230120005053.png]]

Плюсы:
\+ Имеет симметричную область значений относительно нуля (в отличие от сигмоиды)
\+ Имеет ограниченную область (-1, 1)

Минусы:
\- Проблема затухания градиентов на концах функции (близи значений -1 и 1), там производная почти равна 0
\- требуется вычисление exp, что вычислительно дорого

### Backward
$$\tanh(x)=\frac{\sinh(x)}{\cosh(x)}$$
$$\tanh^{'}(x)=\frac{1}{\cosh^2(x)}$$
Из [основного тождества](https://ru.wikipedia.org/wiki/Гиперболические_функции) $\cosh^2(x)-\sinh^2(x)=1$ имеем:
$$1-tanh^2(x)=\frac{1}{\cosh^2(x)}$$

### Code
```python
class Tanh(Module):
    def forward(self, input):
        self.output = np.tanh(input)
        return self.output

    def backward(self, input, grad_output):
        th = self.output
        grad_input = np.multiply(grad_output, (1 - th*th))
        return grad_input
```
