## Описание
**Линейнейный слой** (linear layer) или **полносвясный** (full connected layer) производит линейное преобразование над входными данными $x\rightarrow xW+b$, где $W \in \mathbb{R}^{m\times n}$ – матрица весов, $b \in \mathbb{R}^{n}$ – смещение или bias, $x \in \mathbb{R}^{m}$ – входные данные. 
$$z(x)=xW+b$$
То есть в случае подачи входного батча данных размера $k \times m$ сначало он домножается на матрицу весов $W$ размера $m \times n$ и получается матрица размера $k \times n$  к каждой строке которой прибавляется вектор-столбец $b$ и на выходе получается выходной батч размера $k \times n$.

Веса и баес инициализируются согласно [[Xavier Initialization|инициализации Xavier]].

## Backward
Рассмотрим случай батча размера $k=1$. Пусть есть линейная функция $z(x)=xW+b$ и некоторая гладкая функция $g(x)$, представляющая из себя все последующие за линейным слоём преобразования $g(z(x))$, дифиринцируя её по входным значениям:
$$\frac{\partial g}{\partial x_i}=\sum_{j=1}^{n}\frac{\partial g}{\partial z_j}\frac{\partial z_j}{\partial x_i}=\sum_{j=1}^{n}{\frac{\partial g}{\partial z_j}w_{ij}},\space \space \space i=1,2,...,m$$
Дифференцируем её по весам:
$$\frac{\partial g}{\partial w_{ij}}=\frac{\partial g}{\partial z_j}\frac{\partial z_j}{\partial w_{ij}}=\frac{\partial g}{\partial z_j}x_i,\space \space \space i=1,2,...,m; \space j=1, 2, ..., n$$
Дифференцируем её по смещению:
$$\frac{\partial g}{\partial b_{j}}=\frac{\partial g}{\partial z_j}\frac{\partial z_j}{\partial b_{j}}=\frac{\partial g}{\partial z_j}$$
Запишем в виде градиентов:
$$\nabla_{x}{g}=\nabla_{z}{g} \cdot W^T$$
$$\nabla_{W}{g}=x^T \cdot \nabla_{z}{g}$$
$$\nabla_b{g}=\nabla_z{g}$$
### Code
```python
class Linear(Module):
    """Classic linear layer - y=wx+b."""
    def __init__(self, dim_in, dim_out, bias=True):
        super().__init__()
        self._bias = bias
        # Xavier initialization
        stdv = 1/np.sqrt(dim_in)
        self.W = np.random.uniform(-stdv, stdv, size=(dim_in, dim_out))
        if self._bias:
            self.b = np.random.uniform(-stdv, stdv, size=dim_out)

    def forward(self, input):
        self.output = np.dot(input, self.W)
        self.output += self.b if self._bias else 0
        return self.output

    def backward(self, input, grad_output):
        self.grad_W = np.dot(input.T, grad_output)
        grad_input = np.dot(grad_output, self.W.T)
        if self._bias:
            self.grad_b = np.mean(grad_output, axis=0)
        return grad_input

    def parameters(self):
        return [self.W, self.b] if self._bias else [self.W]

    def grad_parameters(self):
        return [self.grad_W, self.grad_b] if self._bias else [self.grad_W]
```