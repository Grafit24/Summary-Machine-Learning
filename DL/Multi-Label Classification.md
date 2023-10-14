---
tags:
  - CV
  - NLP
  - classification
  - "#loss"
---
## Кратко
**Multi-label classification** - классификация на $K$ классов, при этом классы совместные (как теги).

![[Pasted image 20230914143925.png]]

## Model
Интутитивно об ней можно думать, как об создание $K$ независимых бинарных классификаторов. Вместо [[Softmax]] мы используем $K$ [[Sigmoid]].

![[Pasted image 20230914144046.png]]

## Loss
[[Cross Entropy|Binary Cross Enropy]] для каждого класса.
![[Pasted image 20230914144241.png]]