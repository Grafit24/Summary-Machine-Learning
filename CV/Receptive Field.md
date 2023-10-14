#CV 
## Кратко
Упрощая Receptive field некоторого feature map это зона на исходном изображение которая после применнения конволюций сжимается до фичи этого feature map. То есть по своей сути receptive field это область обзора фичи CNN.

>Formally, Receptive field is the region in the input space that a particular CNN’s feature is affected by.

![[Pasted image 20230214193911.png|500]]
На примере видно что каждый пиксель на втором слое имеет receptive field равынй квадрату 3x3, а единственный пиксель на третьем слое имеет receptive field равный 5x5.

## Как можно увелечить Receptive Field
1. Больше conv layers
2. Добавить pooling layers или высокие stride (sub-sampling)
3. Использовать [[Dilated Convolution]]
4. [[Depth-wise Сonvolution]]

![[Pasted image 20230215215233.png]]

### Пометки
- Efficient RF (ERF) - это апостериорный RF. 
- Используя последовательность dilated convolutions RF растёт экспоненциально, пока число параметров растёт линейно.
-  Pooling operations and dilated convolutions turn out to be effective ways to increase the receptive field size quickly.
-  Skip-connections may provide more paths, but tend to make the **effective receptive field** smaller.
- The effective receptive field is increased after training

## Как вычислять?
**Вычисление размера receptive field.**
![[Pasted image 20230214195239.png]]

- $f_l$ - это выход $l$-го слоя FCN (fully-convolutional network)
- $k_l$ - kernel size.
- $r_l$ - receptive field на входном слое нейросети, выхода нейросети.
- $p_l$ - padding
- $s_l$ - stride

Тогда посчитать $r_{0}$ можно рекурсивно
$$r_{l-1}=s_l \times r_l + (k_l-s_l)$$
$$r_0=\sum^L_{l=1}((k_l-1)\prod_{i=1}^{l-1}s_i) + 1$$
![[Pasted image 20230214200740.png|500]]

**Вычисления начального и конечного индекса Receptive Field**:
![[Pasted image 20230214200949.png|500]]
![[Pasted image 20230214200933.png]]


### References:
1. [How to Calculate Receptive Field Size in CNN](https://www.baeldung.com/cs/cnn-receptive-field-size)
2. [Computing Receptive Fields of Convolutional Neural Networks](https://distill.pub/2019/computing-receptive-fields). Здесь также представлена библиотека на tensorflow для вычисления.
3. [Understanding the receptive field of deep convolutional networks](https://theaisummer.com/receptive-field/)