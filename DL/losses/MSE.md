#loss
[Источник](https://en.wikipedia.org/wiki/Mean_squared_error)
## Mean squared error
Среднеквадратичная ошибка - это [[Функция потерь|функция потерь]], часто используемая для задач регрессии. Пусть $N$ – это размер батча, $y$ – это целевое значение, а $p$ – это предсказание модели, тогда: 
$$MSE=\frac{1}{N}\sum_{i=1}^{N}(y_i-p_i)^2$$

### Backward
Пусть $l(y, p)=MSE(y, p)$, тогда:
$$\frac{\partial l}{\partial p}=\frac{2}{N}\sum_i(y_i-p_i)$$

### Code
```python
class MSE(Criterion):
    def forward(self, input, target):
        batch_size = input.shape[0]
        self.output = np.sum(np.power(input - target, 2)) / batch_size
        return self.output

    def backward(self, input, target):
        self.grad_output  = (input - target) * 2 / input.shape[0]
        return self.grad_output
```