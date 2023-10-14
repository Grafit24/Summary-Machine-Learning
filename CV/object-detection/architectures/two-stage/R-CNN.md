#CV #object-detection #architecture #two-stage-detector
## Кратко
**R-CNN** это старая архитектура, которая сегодня не используется. Её идея в том, что мы с помощью [[Selective Search|selective search]] создаём ~2000 предполагаемых bboxов и после этого кропим+ресайзим их и отправляем в CNN и после в $N$ бинарных классификаторов [[SVM]] (очевидно почему от этой архитектуры в дальнейшем отказались).

Также важно отметить, что SVMы обучалась независимо от CNN. 

> [[Selective Search]]:  
> 1. Generate initial sub-segmentation, we generate many candidate regions  
> 2. Use greedy algorithm to recursively combine similar regions into larger ones  
> 3. Use the generated regions to produce the final candidate region proposals

![[Pasted image 20230220200437.png]]