---
tags:
  - NLP
  - LLM
  - fine-tuning
  - prompting
---
[Google Research](https://ai.googleblog.com/2022/02/guiding-frozen-language-models-with.html) [Paper](https://aclanthology.org/2021.emnlp-main.243/)
## What is soft prompt tuning?
Soft prompt tuning это метод дообучения не всей модели, а только её промпта. Мы к началу входной последовательности эмбеденгов добавляем последовательность векторов фиксированного размера Tunable soft prompt, который мы и будем оптимизировать. При этом веса самой модели заморожены.

> Soft prompt в ходе обучения извлекает данные о том, как выполнять поставленную задачу, как обычный дискретный промрт, только с тем отличием, что он не ограничен дискретностью.

![[Pasted image 20230418215913.png]]

**Плюсы**:
- Устойчива к domain shift
- Позволяет во время инференса использовать для одного батча разных тасков одну и ту же модель.
- Эффективнее и дешевле полного переобучения модели. Малое количество параметров для обучения.

![[Pasted image 20230418221151.png]]

**Результаты**:
![[Pasted image 20230418220806.png]]

>  **Intuitively**, the larger the pre-trained model, the less of a “push” it needs to perform a specific task, and the more capable it is of being adapted in a parameter-efficient way.