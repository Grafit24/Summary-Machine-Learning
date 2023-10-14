---
tags:
  - ML
  - NLP
  - classification
  - classic
---
## Кратко
![[Pasted image 20230911223333.png]]
[[Naïve Bayes]] это [[Generative Models|генеративная модель]].
![[Pasted image 20230911223345.png]]

## Подробнее
$P(y=k)$ может быть определён просто, как число документов класса $k$ на общее число документов.  
$$P(y=k)=\frac{N(y=k)}{\sum\limits_{i}N(y=i)},$$
$P(x|y=k)$ мы делаем "наивные" предположения, что:
- [[Bag of Words]] assumption: порядок слов не важен,
- Conditional Independence assumption: фичи (слова) независимы от класса.
Интуитивно мы отбрасываем контекст и предполагаем, что будет достаточно информации о появление слов в документе. Например в случае *положительных*/*отрицательных* ревью такие слова как **awful**, **bad**, **boring** могут указывать на *отрицательное* ревью, а **good, awesome, great** на *положительное*.
$$P(x| y=k)=P(x_1, \dots, x_n|y=k)=\prod\limits_{t=1}^nP(x_t|y=k)$$
$P(x_i|y=k)$ в этом случае считается, как появление слова $x_i$ в документах класса $k$ делённое на общее число слов появлявшихся в документах класса $k$.
$$P(x_i|y=k)=\frac{N(x_i, y=k)}{\sum\limits_{t=1}^{|V|}N(x_t, y=k)}$$
### Проблема $N(x_i, y=k)=0$
Решается добавлением малого $\delta$, который может быть выбран с помощью [[Cross Validation]].
$$P(x_i|y=k)=\frac{\color{red}{\delta} +\color{white} N(x_i, y=k)
    }{\sum\limits_{t=1}^{|V|}(\color{red}{\delta} +\color{white}N(x_t, y=k))} =
    \frac{\color{red}{\delta} +\color{white} N(x_i, y=k)
    }{\color{red}{\delta\cdot |V|}\color{white}  + \sum\limits_{t=1}^{|V|}\color{white}N(x_t, y=k)}
$$

## Предсказание
Для $k$ классов вычисляется совместная вероятность и выбирается класс с наибольшой совместной вероятностью.  
$$y^{\ast} = \arg \max\limits_{k}P(x, y=k) = \arg \max\limits_{k} P(y=k)\cdot P(x|y=k).$$

![[Pasted image 20230911225726.png]]

## Tips
- Use log-probs: $\log P(x, y=k)=\log P(y=k) + \sum\limits_{t=1}^n\log P(x_t|y=k)$
- General View of [[Naïve Bayes]]![[Pasted image 20230911230038.png]]