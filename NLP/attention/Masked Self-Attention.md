#NLP #attention 
[NLP Course](https://lena-voita.github.io/nlp_course/seq2seq_and_attention.html)
## "Don't look ahead" for the Decoder
Masked Self-Attention скрывает будущие токены (которые ещё предстоит сгенерировать) в энкодере. Это не является проблемой во время инференса, но во время трейна мы не хотим показывать токены, которые только предстоит сгенерировать.

Главное причиной существования Masked Self-Attention является вычислительная эффективность, ведь мы можем вычислять сразу всю последовательность, ведь нету рекурсии, как в [[RNN]]. 

> For recurrent models, one training step requires O(len(source) + len(target)) steps, but for Transformer, it's O(1), i.e. constant.

![[masked_self_attn.mp4]]