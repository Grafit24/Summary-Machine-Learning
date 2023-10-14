#NLP #attention 
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
## Independently Focus on Different Things

> Intuitive: MHA позволяет модели фокусироваться на разных аспектах. 

Так слово влияняет на предложения по разному (например: согласованность рода, времени). Поэтому вместо того, чтобы иметь один механизм внимания, мы используем мн-во независимых голов, которые обращают внимание на различные аспекты.

![[multi_head.mp4]]

[[Multi-Head Attention]] не увеличивает размер модели (не считая линейный слой в конце), ведь он разбивает вектора $q, k, v$ на $n$ частей (голов). Также после конкатенации применяется линейный слой.
$$\mbox{MultiHead}(Q, K, V) = \mbox{Concat}(\mbox{head}_1, \dots, \mbox{head}_n)W_o,$$
$$\mbox{head}_i=\mbox{Attention}(QW_Q^i, KW_K^i, VW_V^i)$$

![[Pasted image 20230412203827.png|450]]