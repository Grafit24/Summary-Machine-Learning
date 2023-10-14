#optimizer #adaptive-lr 
[Источник](https://ruder.io/optimizing-gradient-descent/)
## Описание
Adaptive Moment Estimation - adaptive learning rate метод. В дополнение к сохранению экспоненциального среднего квадратов градиентов $v_t$ как [[Adadelta]] и [[RMSprop]], также сохраняет экспоненциальное среднее предыдущих градиентов $m_t$, как [[Momentum]].
$\large m_t = \beta_1m_{t-1} + (1-\beta_1)g_t$
$\large u_t = \beta_2u_{t-1} + (1-\beta_2)g_t^2$

$m_t$ и $u_t$ сдвинуты к нулю, чтобы продействовать этому вычисляют bias-corrected estimates:
$\large \hat{m}_t=\frac{m_t}{1-\beta_1^t}$
$\large \hat{u}_t=\frac{u_t}{1-\beta_2^t}$

$$\large \theta_t = \theta_{t-1} - \frac{\eta}{\sqrt{\hat{u}_t} + \epsilon} \hat{m}_t$$
## Интутивно
Если [[Momentum]] шар, то Adam это тяжёлый шар с сопротивлением, который будет предпочитать минимум на поверхности функции потерь.