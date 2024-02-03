[Source](https://lena-voita.github.io/nlp_course/transfer_learning.html#word_embeddings) [Paper](https://arxiv.org/abs/1907.11692)
## Bidirectional Encoder Representations from Transformers
BERT's model architecture is **Transformer's encoder**. What is new, is the training objectives and the way BERT is used for downstream tasks.

### Training Input: Pairs of Sentences with Special Tokens
На вход модели подаётся последовательность с двумя специальными токенами:
- \[CLS\] — так-как encoder bidirectional надо откуда-то брать эмбденг содержащий информацию о двух предложения для решения задачи NSP на которой обучается BERT.
- \[SEP\] — разделитель обозначающий конец предложения.

![[Pasted image 20240118003703.png]]

Помимо этого для того чтобы модели было проще разделить предложения в дополнение к [[Transformer#Positional Encoding|Positional Embeddings]] добавляются **Segment Embeddings**, которые различаются для токенов разных предложений (При файтюнинге, например на задачу классификации, обычно передаются segment embeddings только для одного предложения). 

![[Pasted image 20240118004016.png]]

## NSP: Next Sentence Prediction Objective
The Next Sentence Prediction (NSP) objective is a binary classification task. From the final-layer representation of the special token \[CLS] , the model predicts whether the two sentences are consecutive sentences (последовательные предложения) in some text or not. Note that in training, 50% of examples contain consecutive sentences extracted from training texts and another 50% - a random pair of sentences.

## MLM: Masked Language Modeling Objective
1. select some tokens  (each token is selected with the probability of 15%)
2. replace these selected tokens  
    - with the special token \[MASK] - with p=80%, 
    - with a random token - with p=10%, 
    - with the original token (remain unchanged) - with p=10%)
3. predict original tokens (compute loss).

[Example](https://lena-voita.github.io/nlp_course/transfer_learning.html#word_embeddings)

MLM is still language modeling: the goal is to predict some tokens in a sentence/text based on some part of this text.

![[Pasted image 20240118005815.png]]

[Fine-tuning for downstream tasks](https://lena-voita.github.io/nlp_course/transfer_learning.html#word_embeddings)