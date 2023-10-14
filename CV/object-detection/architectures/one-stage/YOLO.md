#CV #architecture #object-detection #one-stage-detector
[Paper](https://arxiv.org/abs/1506.02640)
## Кратко
YOLO делит изображения сеткой $S \times S$ и для кадого патча сетки предсказывает  $B$ bbox'ов (то есть их координаты 4 числа) и confidence для каждого, а также вероятности $C$ классов. 

![[Pasted image 20230302222519.png]]

![[Pasted image 20230302222426.png]]
Для этого примера head'а: 
- $S = 7$
- $B=2$ то есть для каждого грида предсказывается два bbox'а
- $C=20$