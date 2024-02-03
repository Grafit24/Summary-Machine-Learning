---
tags:
  - NLP
  - embeddings
---
## General Idea

> Instead of representing individual words, we can learn to represent words **along with the context they are used in**.

![[Pasted image 20240117172736.png]]

Мы не просто берём хэш эмбеденгов слов, мы прогоняем всю последовательности слов через модель и получаем эмбеденги для каждого слова в контексте.
![[Pasted image 20240117220710.png]]

## ELMo: Embeddings from Language Models

На вход ELMo слова подаются по-символьно - то есть character-level. С помощью свёрток и хайвеев они обрабатываются и получается эмбеденг слова вне контекста, после чего этот эмбеденг подаётся в lstm и мы получаем эмбеденг слова в контексте. Как очевидно из заголовка модель обучалась на задаче [[Language Modeling]] то есть предсказания следующего токена.

![[Pasted image 20240117234513.png]]

### Weight Representations from Different Layers

![[Pasted image 20240117235559.png]]

Overall, ELMo representations have three layers:
- layer 0 (embeddings) - output of the character-level CNN;
- layer 1 - concatenated representations from layer 1 of both forward and backward LSTMs;
- layer 2 - concatenated representations from layer 2 of both forward and backward LSTMs.



