#activation 
[Источник](https://academy.yandex.ru/handbook/ml/article/pervoe-znakomstvo-s-polnosvyaznymi-nejrosetyami)
## Leaky ReLU
Модификация [[ReLU]] устраняющая проблему смерти градиентов при $x < 0$, тем самым меньше провоцируя затуханием градинета. Гиперпараметр $α$ обеспечивает небольшой уклон слева от нуля, что позволяет получить более симметричную относительно нуля область значений (чаще всего $\alpha = 0.01$).
$$\text{LReLU}(x) = \max(\alpha x, x), \quad  0 < \alpha \ll 1$$
$$\text{LReLU}: \mathbb{R} \to (-\infty, +\infty)$$
![[Pasted image 20230120002919.png]]

### Backward
Пусть $f(x)=\text{LReLU}(x)$, тогда
$$\frac{df}{dx}=\left\{\begin{matrix}
    \alpha, \quad x \leqslant  0
 \\ 1, \quad x > 0
\end{matrix}\right.$$

### Code
```python
class LeakyReLU(Module):

    def __init__(self, slope=0.01):
        super().__init__()
        self.slope = slope

    def forward(self, input):
        self.output = (input > 0)*input + (input <= 0)*self.slope*input
        return self.output

    def backward(self, input, grad_output):
        grad_input = np.multiply(
	        grad_output, (input > 0) + (input <= 0)*self.slope
	        )
        return grad_input
```