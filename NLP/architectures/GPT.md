---
tags:
  - NLP
  - transformer
  - language-modeling
---
[Source](https://lena-voita.github.io/nlp_course/transfer_learning.html#word_embeddings)
## Generative Pre-Training for Language Understanding

GPT is a Transformer-based left-to-right language model. The architecture is a 12-layer Transformer decoder (without decoder-encoder attention). Training on the [[Language Modeling]] task.

## Using GPT for Downstream Tasks
The fine-tuning loss consists of the task-specific loss, as well as the language modeling loss:
$$L = L_{xent} + \lambda \cdot L_{task}.$$
![[Pasted image 20240118002308.png]]

## Models
- GPT-1: [Improving Language Understanding by Generative Pre-Training](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)
- GPT-2: [Language Models are Unsupervised Multitask Learners](https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)
- GPT-3: [Language Models are Few-Shot Learners](https://arxiv.org/pdf/2005.14165.pdf)

These models are different mostly in the amount of training data and the number of parameters
