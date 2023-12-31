# Cycle GAN
#CV #gan #generation #NST  
[Источник](https://www.youtube.com/watch?v=N2u9lRXXRac)
## Описание
![[Pasted image 20220430010440.png|700]]
Когда для задачи отсутвуют пары input-target, как в [[Neural Style Transform|задаче переноса стиля]], можно использовать Cycle GAN чья идея и заключается в том, чтобы циклично переводить изображение из разных домейнов туда и обратно.
Так в задаче переноса стиля, обучая одновременно перевод из разных домейнов позволяет нам сохранять структуру картинки, но при этом менять её стиль.
## Модель
![[Pasted image 20220430004842.png]]
- $D_x$, $D_y$  — дискриминаторы множества $X$ и $Y$ соответсвенно.
- $G$, $F$  — генераторы $X$->$Y$ и $Y$->$X$ соответсвенно.
- Благодрая $D_y$ модель учится переводить изображение в $Y$, а $D_x$ обратно.  

![[Pasted image 20220430005935.png]]

**Loss**
![[Pasted image 20220430005959.png]]
- Состязательные функции потерь — это обычные фун-ии потерь [[GAN]]'ов, для соответсвующих домейнов.(см. 2-3 изображения архитектуры)
- Циклическая функция потерь — это функция сравнивающая разницу обратных преобразований, насколько они отошли от исходного изображения. (см. 2-3 изображения архитектуры)

**Identity loss**
![[Pasted image 20220430010534.png]]
Задача лосса состоит в сохранение цветовой палитры исходного изображения, что как видно он и делает сравнивая разницу исходного с генерированным.

![[Pasted image 20220430010810.png|500]]


