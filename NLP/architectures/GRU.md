---
tags:
  - "#NLP"
  - architecture
  - rnn
---
[StackExchange](https://ai.stackexchange.com/questions/21361/whats-the-difference-between-lstm-and-gru) [Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) [StackExchange 2](https://datascience.stackexchange.com/questions/14581/when-to-use-gru-over-lstm)
## Gated Recurrent Unit
Используя меньше параметров чем [[LSTM]] имеет похожий perfomance. 
В отличие от [[LSTM]] вместо forget и input gates имеет единый "**update gate**" (правый). Также он объеденяет cell state и hidden state. Второй gate - это "**reset gate**" (левый).

![[Pasted image 20230320220555.png]]

На практике, чтобы понять [[GRU]] лучше или [[LSTM]] требуется их сравнение на конкретной задаче.

> According to a study comparing LSTM and GRU on symbolic sequences of different complexity, GRUs outperform LSTM networks on low-complexity sequences while on high-complexity sequences LSTMs perform better. In another study, GRUs train faster and perform better than LSTMs on less training data if you are doing language modeling.

