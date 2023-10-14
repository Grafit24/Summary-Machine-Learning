#CV #metric #loss #segmentation 
## Dice Coefficent
Пусть $P$ - это предсказанная маска, а $G$ - это ground truth.
$$\text{Dice}=\frac{2|P \cap G|}{|P| + |G|}$$
Если классов много, то усредняем по классам.
Dice Coefficent учитывает imbalanced classes (то есть недопредставленные классы на изображение).

![[Pasted image 20230213180145.png]]

## Интерпретация Dice
Рассмотрим случай бинарной классификации где маска состоит из одного класса, тогда:
![[Pasted image 20230213183342.png]]
![[Pasted image 20230213183458.png]]
То есть Dice метрика это по своей сути F1 метрика для бинарной классификации.

## Dice Loss
Dice Coefficent можно использовать как $\text{loss} = 1 - \text{Dice} \rightarrow min$. Преимуществом над [[Cross Entropy]] является лучшая работа с imbalanced classes ([Ссылка на источник](https://stats.stackexchange.com/questions/321460/dice-coefficient-loss-function-vs-cross-entropy)) правда градиенты считаются сложнее чем [[Cross Entropy]], поэтому автор заметки предпочитают использовать именно её с весами на недопредставленные классы.
$$\text{DiceLoss(G, P)}=1-Dice(G, P)=1-\frac{2 \times \text{sum}(G \odot P)}{\text{sum}(G+P) + \epsilon}$$