---
tags:
  - NLP
  - architecture
  - rnn
---
[Blog](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)
## Long Short Term Memory networks
Это особый случай [[RNN]], спобный учиться long-term dependecies by design.
LSTM похоже на конвейр - она передаёт cell state $C$, который движется через все состояния блока, как долгосрочная память.

![[Pasted image 20230320212429.png]]
![[Pasted image 20230320212436.png]]

Она также имеет структуры, назывваемые gates (вентили), которые отвечают за умения забывать информацию. Состоят они из [[Sigmoid]] network layer (Sigmoid(Linear + Linear)) и операции поэлементного умножения. Он выдаёт числа в пределах от 0 до 1, где 0 означает полностью избавиться от информации, а 1 оставить полностью. 
![[Pasted image 20230320214952.png]]

1. **Forget gate**. Решаем какую информацию следуют выбросить из cell state (то есть нашей долгострочной памяти).
![[Pasted image 20230320212737.png]]

2. Решаем какую информацию следует добавить в cell state.
	* $\tilde{C}$ - это значения кандидаты, которые мы планируем добавить в cell state
	* $i$ - это **input gate** layer, в которым мы решаем какие имеено значения мы добавим
![[Pasted image 20230320213031.png]]

3. Применяем эти операции к cell state
![[Pasted image 20230320213053.png]]

4. Решаем, что войдёт в выход, для этого мы фильтруем cell state с помощью "output gate" и приводим его к диапозону (-1;1).
![[Pasted image 20230320213243.png]]

**Примечание**. Хочу ещё отметить, что мы передаём и hidden state, как в классической [[RNN]], что напоминает краткосрочную память.

### Вариации LSTM
- One popular LSTM variant, introduced by [Gers & Schmidhuber (2000)](ftp://ftp.idsia.ch/pub/juergen/TimeCount-IJCNN2000.pdf), is adding “peephole connections.” This means that we let the gate layers look at the cell state.
![[Pasted image 20230320220519.png]]

- Another variation is to use coupled forget and input gates. Instead of separately deciding what to forget and what we should add new information to, we make those decisions together. We only forget when we’re going to input something in its place. We only input new values to the state when we forget something older.
![[Pasted image 20230320220532.png]]

- [[GRU]]
![[Pasted image 20230320220555.png]]