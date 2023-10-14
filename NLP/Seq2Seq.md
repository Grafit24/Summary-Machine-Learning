#NLP #attention #seq2seq #language-modeling 
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
## Seq2Seq Basics
Самая типичная задача seq2seq это машинный перевод. Идея заключается в том, что человек интуитивно беря предложение на изначальном языке переводит его в предложение на другом, беря наиболее вероятное предложение. Мы хотим чтобы наша модель умела также. 

![[Pasted image 20230322193715.png]]

### Modeling - Encoder-Decoder Framework

![[Pasted image 20230322194013.png]]
- **Encoder** - принимает на вход изначальную последовательноть и строит его представление, которые дальше передаёт Decoder'у.
- **Decoder** - принимает на вход представление предложения и генерирует новую последовательность на его основе (на интересующем нас языке).

#### Conditional Language Models
По своей сути seq2seq модель это [[Language Modeling|language model]] с условием $x$, то есть нашей исходной последовательностью (но в общем случае это может быть что угодно, например изображение).

![[Pasted image 20230322200548.png|500]]

Decoder в данном случае и есть наша LM с условием в виде sourse representation vector, который в случае RNN передается как последний hidden state Encoder'а.

![[Pasted image 20230322201247.png]]
1. feed source and previously generated target words into a network;
2. get vector representation of context (both source and previous target) from the networks decoder;
3. from this vector representation, predict a probability distribution for the next token.

**Простейшая модель с двумя RNN**:
![[Pasted image 20230322201815.png]]

### Learning - [[Cross Entropy]]
На кажом этапе мы максимизируем вероятность правильного токена, при условии переданных модели правильных пердыдущих токенов целевой последовательности.

![[Pasted image 20230322202121.png]]

![[seq2seq_training_with_target.mp4]]

### Search - Inference
- Greedy Search - брать наиболее вероятный токен на каждом шаге.
	- Проблема в том, что выбор наиболее вероятных токенов на каждом этапе не гантирует, что вероятность всего предложения в целом будет максимальная. ![[Pasted image 20230322202732.png]]
- [[Beam Search]] - параллельно генерируем beam_size ветвлений и на каждом этапе берём суммарно beam_size наиболее вероятных вариантов. В конце считаем произведение вероятностей кадого из получившихся последовательностей (веток) и выбираем наибольшее.  
![[beam_search.mp4]]

## [[Attention]] with RNN 
Главной проблемой классического seq2seq подхода заключается в том что мы пытаемся сжать целое предложение в один вектор из-за чего образуется узкое горлышко.
Идея механизма внимания заключается, в то что мы хотим обращать внимание на разные слова в предложение при генерации каждого нового члена последовательности.

![[Pasted image 20230411192608.png|500]]

### Bahdanau Model
- encoder: bidirectional
- attention score: multi-layer perceptron
- attention applied: between decoder steps
![[Pasted image 20230411200022.png]]

### Luong Model
- encoder: unidirectional (simple)
- attention score: bilinear function
- attention applied: between decoder RNN state t and prediction for this step
![[Pasted image 20230411200030.png]]

## [[Transformer]]

![[Pasted image 20230411201327.png]]

![[Pasted image 20230412185652.png]]

## Subword Segmentation: [[BPE]]
BPE разбивает слова так, чтобы символы которые наиболее часто встречаются вместе, энкодились как один токен. Изначально это способ сжатия данных.

## [[Multi-Head Attention]] interpretability

> While the rare tokens head surely looks fun, don't overestimate it - most probably, this is a sign of overfitting. By looking at the least frequent tokens, a model tries to hang on to these rare "clues".

> In addition to confirming that the specialized heads are the most important (because the model keeps them intact and prunes the other ones), the authors find that most of the heads can be removed without significant loss in quality.

