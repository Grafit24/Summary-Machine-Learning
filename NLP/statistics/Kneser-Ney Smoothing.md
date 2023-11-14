---
tags:
  - NLP
  - language-modeling
  - n-gram
---
[Paper](http://www-i6.informatik.rwth-aachen.de/publications/download/951/Kneser-ICASSP-1995.pdf) [Course](https://lena-voita.github.io/nlp_course/language_modeling.html#papers_smoothings)
## Kneser-Ney Smoothing
Чтобы решить проблему Back-off в виде того что он может дать неоправданную частоту юниграме такой как San Francisco, где самого выражение встречается часто, но Francisco само по себе встречается редко.
![[Pasted image 20230321210501.png|200]]
## Stupid Back-off vs Kneser-Ney

![[Pasted image 20230321210707.png]]
