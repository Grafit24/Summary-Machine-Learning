#CV #object-detection #metric 
[Medium](https://jonathan-hui.medium.com/map-mean-average-precision-for-object-detection-45c121a31173)
### Описание
**mAP (mean Average Precision)** используется для вычисления точности модели в задачи [[Object Detection]]. mAP считается как среднее AP по всем классам.

### Вычисление AP
Для вычисления AP используется [[Precision]], [[Recall]] и [[IoU]].

1. Все предсказания модели ранжируются по уверенности в соответсвующим предсказание
2. Определеяется correct или incorrect предсказание по threshold IoU между пресказанием и истинным bbox
3. Далее для каждого предсказания считается [[Precision]] и [[Recall]].
	- [[Precision]] = все верные предсказания рангом выше (conf выше) / все предсказания рангом выше
	- [[Recall]] = все верные предсказанися рангом выше / все правильные предсказания
4. Вычисление AP как площадь под precision-recall кривой $\text{AP}=\int_0^1 \text{Precision}(\text{Recall}) d(\text{Recall})$ 
	- Из-за сложности вычисления данного интеграла её нужно сгладить, делается это с помощью **AUC** метод или **Interpolated AP**. 

![[Pasted image 20230228220855.png]]
B - raw, C - smooth

**Пример**:
![[Pasted image 20230228220529.png]]
Рассмотрим вычисления 4 ранга Precision=0.5=2/4, Recall=0.4=2/5.

### Проблема
%%хз как описать%%
![[Pasted image 20230228221142.png]]
![[Pasted image 20230228221156.png]]