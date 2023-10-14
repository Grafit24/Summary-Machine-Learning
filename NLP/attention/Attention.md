#NLP #attention 
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)

> Attention: На разных шагах генерации модель фокусируется на разных частях входа.

> Main idea: Нейросеть может выучить, какие части входа наиболее важны на кадом шаге.

## Attention: A High-Level View

![[Pasted image 20230411193828.png]]

На каждом этапе attention:
- получает $h_t$ состояние декодера на шаге $t$ и состояния энкодера $s_1,s_2,...,s_m$
- computes attention scores: $\text{score}(h_t, s_k)$ для каждого состояния энкодера.
- computes attention weights: вероятностное распределение полученное применением [[Softmax]] к attention scores.
- computes attention output: weighted sum of encoder states and attention weights.

![[Pasted image 20230411194531.png]]

## Attentin score

![[Pasted image 20230411195110.png]]