---
tags:
  - NLP
  - language-modeling
  - n-gram
---
[Paper](http://www-i6.informatik.rwth-aachen.de/publications/download/951/Kneser-ICASSP-1995.pdf) [Course](https://lena-voita.github.io/nlp_course/language_modeling.html#papers_smoothings) [Wiki](https://en.wikipedia.org/wiki/Kneser–Ney_smoothing)
## Kneser-Ney Smoothing
Чтобы решить проблему Back-off (переход к моделе более низкого порядка) в виде того что он может дать неоправданную частоту юниграме такой как San Francisco, где самого выражение встречается часто, но Francisco само по себе встречается редко.
![[Pasted image 20230321210501.png|200]]
## Stupid Back-off vs Kneser-Ney
![[Pasted image 20230321210707.png]]
Формула для n = 1:
$$p_{KN}(w_i) = \frac { |\{ w' : 0 < c(w',w_i)     \} | } 
                    { |\{ (w',w'') : 0 < c(w',w'') \} | }$$
Вместо простого подсчёта unigram мы считаем кол-во уникальных слов за которыми может следовать $w_i$. Это число мы делим на число всех уникальных пар слов.

Рекурсивная формула для n > 1:
$$p_{KN}(w_i|w_{i-n+1}^{i-1}) = \frac{\max(c(w_{i-n+1}^{i-1},w_{i}) - \delta,0)}{\sum_{w'} c(w_{i-n+1}^{i-1},w')} + \delta \frac{| \{ w' : 0 < c(w_{i-n+1}^{i-1},w') \} |}{\sum_{w'} c(w_{i-n+1}^{i-1},w')} p_{KN}(w_i|w_{i-n+2}^{i-1})$$

Объяснение рекурсивной формулы:
![[Pasted image 20231201212710.png]]