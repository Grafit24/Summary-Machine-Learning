#activation
[Источник](https://academy.yandex.ru/handbook/ml/article/pervoe-znakomstvo-s-polnosvyaznymi-nejrosetyami)
## **ReLU**, Rectified linear unit
ReLU представляет собой простую кусочно-линейную функцию. Одна из наиболее популярных функций активации. В нуле производная доопределяется нулевым значением.
$$\text{ReLU}(x)=\max(0, x)$$
$$\text{ReLU}: \mathbb{R} \to [0, +\infty)$$

![[Pasted image 20230119230234.png]]

Плюсы:
\+ сходится быстро (относительно sigmoid из-за отсутсвие проблемы с затуханием градиентов)
\+ вычислительная простота активции и производной (Прирост в скорости относительно сигмойды в 4-6 раз)
\+ не saturated nonlinear

Минусы:
\- для отрицательных значений производная равна нулю, что может привести к затуханию градиента;
\- область значений является смещённой относительно нуля.

### Backward
Пусть $f(x)=\text{ReLU}(x)$, тогда
$$\frac{df}{dx}=\left\{\begin{matrix}
0, \quad x \leqslant  0
 \\ 1, \quad x > 0
\end{matrix}\right.$$

### Code
```python
class ReLU(Module):
	"""Rectified linear unit. Activation function."""
	
    def forward(self, input):
        self.output = np.maximum(input, 0)
        return self.output

    def backward(self, input, grad_output):
        grad_input = np.multiply(grad_output, input > 0)
        return grad_input
```

### Про скорость ReLU
![[Pasted image 20230209181122.png]]
Рисунок взята из статьи [[AlexNet]].