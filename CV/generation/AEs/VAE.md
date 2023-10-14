# Variational Autoencoder
#CV #generation #autoencoder
[Источник](https://www.youtube.com/watch?v=N2u9lRXXRac)
## Описание
Архитектура генеративной модели. Отличается от обычного AE предсказанием не латентный точек, а гиперсфер с сэмплированием, а также добавление KL расходимости.
![[Pasted image 20220428133705.png]]

**Проблемы обычного Autoencoder**
Латентное пространство получается разряженным из-за чего генерация в пустотах, где нет данных, работает плохо.
![[Pasted image 20220428123602.png|400]]
## Суть VAE
**Гиперсфера**
Мы накладываем некоторое ограничения на энкодер. Теперь мы предсказываем не координаты, а $\mu$  и $\sigma$ , то есть гиперсферу из которой мы сэмлируем(берём рандомное число) некоторое число, передоваемое в декодер. 
P.S. Проблема дифференцирования сэмплирования решается с помощью Representation Trick.
![[Pasted image 20220428124949.png]]
![[Pasted image 20220428125013.png]]

Но это всё же не решает проблему разряженности данных
![[Pasted image 20220428130041.png]]

**Kullback–Leibler расходимость**
Метрика схожести распределений, которую мы используем как loss вместе с Representation Loss (MAE как пример) и получаем:
![[Pasted image 20220428131316.png|500]]

**Representation Trick**
Но как деффиринцировать сэмплирование? Для этого мы воспользуемся трюком беря число из нормального распределения и домножать его на предсказанное отклонение и прибавлять мат. ожидания.
![[representation_trick.png]]
![[Pasted image 20220428133553.png]]
