#NLP #attention #transformer
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
## Transformer: Attention is All You Need

> Attention is All You Need, потому что мы используем attention и вместо encoder и вместо decoder

> Интуитивно: Transformer это последовательность этапов рассуждения (слоёв). На каждом этапе токены обмениваются между собой информацией и обновляют своё представление, пытаясь лучше понять друг друга в контексте. 

В отличие от [[RNN]] подхода Transformer обращает внимание сразу на всю последовательность, а не на отдельные токены. На гифке ниже видно, что сначало Transformer энкодит последовательность $N$ раз в этом время все токены между собой обмениваются информацией и обновляют соответственно своё представление. 
Аналагочиное происходит и во время декодинга, только генерируемый токен на текущем этапе смотрит на уже сгенерированные токены и на исходные токены (полученные во время энкодинга) и обновляет представление.

![[transformer_original.gif]]

![[Pasted image 20230411202436.png]]

## Model Architecture
Attentions:
![[Self-Attention]]
![[Masked Self-Attention]]
![[Multi-Head Attention]]

![[transformer_architecture.png]]
$N=6$ обычно.

### Feed-forward blocks
FFN используется, чтобы обработать информацию полученную с помощью механизмов внимания.

> **attention** - "look at other tokens and gather information"
> **FFN** - "take a moment to think and process this information"

Linear + Relu + Linear
![[Pasted image 20230413204542.png|300]]
$$FFN(x) = \max(0, xW_1+b_1)W_2+b_2.$$

### Residual connections
"Add&Norm" - Add это именно про Residual connections.

![[Pasted image 20230413204834.png|500]]

Просто напоминание: позволяет бороться с затуханием градиентов.

### Layer Normalization
![[Layer Normalization]]

### Positional Encoding
Так, как трансформер не имеет рекурсии или конволюций он не может определить последовательность входных токенов, поэтому для передачи этой информации существуют позиционные эмбденги, которые мы складываем с эмбеденгами слов получая - слова на позиции $pos$. 

![[Pasted image 20230413210138.png|500]]

Эти эмбеденги могут быть выучены, но авторы оригинальной статьи выяснили, что использование фиксированных эмбеденгов не сильно вредит качеству:
$$\mbox{PE}_{pos, 2i}=\sin(pos/10000^{2i/d_{model}})$$
$$\mbox{PE}_{pos, 2i+1}=\cos(pos/10000^{2i/d_{model}})$$
- $pos$ - позиция токена
- $i$ - элемент вектора эмбеденга
Каждое измерение полученного эмбеденга соответсвует синусойде и длины волн образуют геометрическую прогрессию от $2\pi$ до $10000\times 2\pi$.

## FFNs as Key-Value Memories
[Source](https://lena-voita.github.io/nlp_course/transfer_learning.html#word_embeddings)
A token representation evolves from the input token embedding to the final layer prediction. Residual connections, [[Attention|attention]] and [[Transformer#Feed-forward blocks|feed-forward blocks]] update the original representation by **adding new information**. This sequence of evolving representations for the same token is called the **residual stream**.

![[Pasted image 20240119001850.png]]

>Note 
>- while **attention** layers allow exchanging information **across tokens**, 
>- **FFNs** operate within the **same residual stream**.

In [this paper](https://arxiv.org/pdf/2012.14913.pdf), the authors propose to view feed-forward layers in transformer-based language models as key-value memories. In this view, the columns of the first FFN layer encode textual concepts and the rows of the second FFN layer encode distributions over vocabulary.

![[Pasted image 20240119001922.png]]