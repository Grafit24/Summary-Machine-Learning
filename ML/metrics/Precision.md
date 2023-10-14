#metric #classification #object-detection

**Precision** (Точность) - это отношение точно предсказанных сэмплов класса positive ко всем предсказанниям моделья этого класса (в том число и ложных positive) среди всех сэмплов. Насколько предсказанния модели точны и в реальности соответствуют истинному классу positive. 
Про обозначения читать в [[Classification]].
$$\text{Precision}=\frac{\text{TP}}{\text{TP}+\text{FP}}$$
- Если 0, то не один из предсказанных классов сэмплов не является реально positive.
- Если 1, то все предсказанные positve классы соответсвуют реальным.

![[precision_recall.png|300]]

%%Логически так решил%%
> В случае multi-class мы считаем Precision по каждому классу и усредняем ([StackExchange](https://stats.stackexchange.com/questions/51296/how-do-you-calculate-precision-and-recall-for-multiclass-classification-using-co)). 

**Примечание**. Проблема Precision состоит в том что, даже если предсказывать все классы как negative, то он будет 1, то есть он отвечает только за **точность**, но этого мало поэтому вместе с ним всегда используется [[Recall]].


