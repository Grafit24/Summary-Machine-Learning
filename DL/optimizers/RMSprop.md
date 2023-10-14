#optimizer  #adaptive-lr 
[Источник](https://ruder.io/optimizing-gradient-descent/)
## Описание
Метод пытается решить проблему колебаний, как и [[Momentum]], но заходя с другой стороны RMSprop вычисляет learning rate для каждого параметра отдельно, как [[Adagrad]].
1. Метод позволяющий решить проблему [[Adagrad]] с радикально уменьшающимися learning rates;
2. Реализация [[Rprop]] для mini-batch.

$$E[g^2]_t = 0.9E[g^2]_{t-1} + 0.1g_t^2$$
$$\theta_t = \theta_{t-1} - \frac{\eta}{\sqrt{E[g^2]_t + \epsilon}}g_t$$
