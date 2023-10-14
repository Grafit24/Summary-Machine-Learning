---
tags:
  - NLP
  - ML
  - CV
  - classification
---
## Подзадачи классификации

![[Pasted image 20230226191318.png|600]]

- **Binary classification** - бинарная классификация на два класса (1/0; true/false), при этом классы несовместны.
- **Multi-class classification** - классификация на $N$ классов, при этом классы несовместны (то есть можно предсказать только один класс).
- **Multi-label classification** - классификация на $N$ классов, при этом классы совместные (как теги).

## Metrics

![[precision_recall.png|300]]

Пусть есть задача бинарной классификации на два класса positive и negative, тогда результаты классификации моделью можно разбить на четыре типа: 
- TP - true positives, кол-во правильных предсказаний класса positive;
- FP - false positives, кол-во не правильных предсказаний класса positive;
- TN - true negatives, кол-во правильных предсказаний класса negative;
- FN - false negatives, кол-во не правильных предсказаний класса negative.

- [[Precision]] $=\frac{\text{TP}}{\text{TP}+\text{FP}}$
- [[Recall]] $=\frac{\text{TP}}{\text{TP}+\text{FN}}$
- [[F-score]]
- [[ROC-AUC]]

## Losses
- [[Cross Entropy|BCE]]
- [[MSE]]
