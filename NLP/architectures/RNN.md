---
tags:
  - NLP
  - architecture
  - rnn
---
[Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) [Pytorch](https://pytorch.org/docs/stable/generated/torch.nn.RNN.html)
## Recurrent Neural Networks
Рекуретные нейросети это сети, которые используют полученную информацию из предыдущих прогонов сети в последующих, то есть они способны обрабатывать последовательности, при чём не фиксированной длинны (в отличие от [[CNN]]). Например, если мы подаём в сеть текст, то мы будем подовать его по одному токену за раз и пройдясь по всему тексту мы сможем предсказать, например, его настроение.

![[Pasted image 20230318180227.png]]

## Standart RNN (Elman)
В стандартной архитектуре RNN, каждый слой нейросети представляет из себя блок на вход которого подаются фичи (эмбединг слова например), а на выходе получается hidden state, который является выходом слоя и при этом является памятью слоя, которую он передает в качестве входа вместе со следующим элементом последовательности.

> hidden state - это память слоя.

Как видно на рисунки представлен один слой Standart RNN, где hidden state $h_{t-1}$ вместе со входом $x_t$ домножаются на веса и складываются, после чего проходят через активацию $tanh$ и слой выдаёт это в качестве выхода и также передаёт этот выход, как hidden state $h_t$ в качетсве входа следующей итерации нейрона. 
![[Pasted image 20230318180536.png]]
В дальнейшем этот hidden state может использоваться как вход линейного классификатора, например. Hidden state с последнего слоя и на последней итерации явялется эмбденгом всей последовательности. 

$$h_t=tanh(x_tW^T+h_{t-1}U^T+b)$$
где 
- $W$ и $U$ это веса соответсвенно для входа слоя и для hidden state
- $b$  это сумма bias для hidden state и для входа
- $h_t$ - это hidden state слоя на $t$-ой итерации
- $x_t$ - это вход слоя на $t$-ой итерации

### Проблема
В теории Standart RNN должно уметь работать с долгострочными зависимостями (long-term dependencies), но на деле она не способна их выучить. Чем больше разрыв между токенами тем меньше информации в hidden state о нужном нам далёком токене.

Пример short-term: "“the clouds are in the _sky_" where the sky is gap to fill. Dependency is close.
![[Pasted image 20230318182039.png]]

Пример long-term: “I grew up in France… I speak fluent _French_.” where French is gap to fill. Dependency is far away.
![[Pasted image 20230318182045.png]]

Также подобные модели тяжело обучать из-за vanishing and exploding gradients.

Для решения проблемы long-term dependecies и vanishing gradients используются модификации стандратной рекуретной нейросети:
- [[LSTM]] - Long Short Term Memory
- [[GRU]] - Gated Residual Networks

## Bidirectional RNN
Для классической RNN существует проблема забывания, того что было в начале текста. Для решения этой проблемы мы воспользуемся двумя RNN: forwards которая читает с лева на право, и backward, которая читает наоборот. После этого мы возьмём последний state с каждой и сконкотенируем. 

![[Pasted image 20230914140737.png]]