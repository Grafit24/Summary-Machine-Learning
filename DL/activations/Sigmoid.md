#activation 
[Источник](https://academy.yandex.ru/handbook/ml/article/pervoe-znakomstvo-s-polnosvyaznymi-nejrosetyami)
## Sigmoid
Исторически одна из первых функций активации. Рассматривалась в том числе и как гладкая аппроксимация порогового правила, эмулирующая активацию естественного нейрона.
$$\sigma(x)=\frac{1}{1+e^{-x}}$$
$$\sigma: \mathbb{R} \to (0, 1)$$
![[Pasted image 20230119232238.png]]
На практике редко используется внутри сетей, чаще всего в случаях, когда внутри модели решается задача бинарной классификации.

Проблемы:
- На концах функции (значения рядом с 0 и 1) производная практически равна 0, что приводит к затуханию градиентов.
- область значений смещена относительно нуля;
- exp вычислительно дорогая операция ([[ReLU]] быстрее в 4-6 раз)

### Backward
$$\frac{d\sigma}{dx}=\frac{exp(-x)}{(1+exp(-x))^2}=\frac{1-1+exp(-x)}{(1+exp(-x))^2}=$$
$$=\frac{1}{1+exp(-x)} - (\frac{1}{1+exp(-x)})^2=\sigma(1-\sigma)$$

### Code
```python
class Sigmoid(Module):
    def forward(self, input):
        self.output = self.__class__._sigmoid(input)
        return self.output

    def backward(self, input, grad_output):
        sigma = self.output
        grad_input = np.multiply(grad_output, sigma*(1 - sigma))
        return grad_input
        
    @staticmethod
    def _sigmoid(x):
        return 1/(1 + np.exp(-x))
```

%%
- saturated regime
- linear regime
%%