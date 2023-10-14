#metric #classification #object-detection 

**Recall** (Полнота) - это соотношение определённых (предсказанных моделью) сэмлов класса positive среди всех сэмлов данного класса в датасете. То есть то насколько полно определенны сэмплы класса positive (модель может какие-то пропустить). 
Про обозначения читать в [[Classification]].
$$\text{Recall}=\frac{\text{TP}}{\text{TP}+\text{FN}}$$
- Если 0, то не был предсказан (как positive) не один реальный positive.
- Если 1, то были предсказаны все positive в датасете, как positive.

![[precision_recall.png|300]]

%%Логически так решил%%
> В случае multi-class мы считаем Recall по каждому классу и усредняем ([StackExchange](https://stats.stackexchange.com/questions/51296/how-do-you-calculate-precision-and-recall-for-multiclass-classification-using-co)). 

**Примечание**. Полнота не является достаточной метрикой т.к. если модель предскажет все сэмплы как positive то Recall будет 1, поэтому необходима метрика [[Precision]].