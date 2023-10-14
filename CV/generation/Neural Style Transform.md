#CV #generation #NST
[Источник](https://arxiv.org/abs/1508.06576)
[Notebook](https://colab.research.google.com/drive/17ryVEnQ7b61LMS0HwxItI7iOlKQPP1BA#scrollTo=WEaf6sefN0b9)

## Кратко
![[1_VAQs1KSfbysnloPah_fHGQ.gif|500]]
Метод совмещения стилей двух картинок путём использования features нейросети. 

Метод заключается в том, что мы задаём лосс, являющийся суммой Style Loss и Content Loss, которые считаются с импользованием Style Representation и Content Representation, с некоторыми коэффицентами(обычно соотношение content к style $10^{-6}$) и оптимизируем нашу входную картинку (шум) так, чтобы она их минимизировала. 

Style и Content representation это слои CNN (предобученной) на которых мы и берём признаки для совмещения стилей.

## Опыт
- [[Batch Normalization]] сильно сглаживает ход градиентов делая результат более сглаженным и приятным, великолепно переносит цвета, но на моих примерах плохо работал с текстурой(но это не точно);
- Без [[Batch Normalization]] в случае если нужна более чёткая картинка неплохо использовать дополнительные Content Representation слои. (добавить к conv_4 conv_5);
- В статье использовалась VGG19, советуют использовать [[AveragePool]] вместо [[MaxPool]], а также для Style Representation брать conv 1-5, а для Style Representation conv 4.