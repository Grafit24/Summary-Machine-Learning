#optimizer #adaptive-lr 
## Описание
Как Adam только, если Adam=[[Momentum]]+[[RMSprop]], то Nadam=[[NAG]]+[[RMSprop]].
$$\theta_{t+1} = \theta_t − \frac{\eta}{\sqrt{\hat{u}_t}+\epsilon}  (\beta_1 \hat{m}_t +\frac{(1−\beta_1)g_t}{1−\beta_1^t})$$