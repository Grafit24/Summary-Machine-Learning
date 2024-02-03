---
tags:
  - NLP
  - transformer
  - PEFT
  - fine-tuning
---
## What is "Transfer Learning"?
Под transfer learning понимается перенос знаний из одной задачи/модели к другой.
![[Pasted image 20240117170350.png]]

>Through **_insert_your_model_**, we "transfer" the knowledge of its training data to a task-specific model.

Taxonomy of Transfer Learning
![[Pasted image 20240117170424.png]]
## [[Word Embeddings|The Simplest Tranfer: Word Embeddings]]
Самый простой способ это взять предобученные эмбеденги слов
![[Pasted image 20240117170548.png]]

Обычно для target task у нас довольно маленькая размеченная выборка, но вот для source task, например [[Word2Vec]], могут быть не нужны размеченные данные (или много размеченных), при этом в процессе решения source task модель может выучить полезные знания для target task.
![[Pasted image 20240117170820.png]]
![[Pasted image 20240117171114.png]]
## ELMo: From Words to Words-in-Context 
![[ELMo]]

## Refuse From Task-Specific Models

> [[ELMo|CoVe/ELMo]] replace word embeddings, but [[GPT]]/[[BERT]] replace **entire models**.

![[GPT]]

![[BERT]]

![[PEFT]]

## Analysis and Interpretability
![[Transformer#FFNs as Key-Value Memories]]

## Benchmarks
- [[GLUE]]