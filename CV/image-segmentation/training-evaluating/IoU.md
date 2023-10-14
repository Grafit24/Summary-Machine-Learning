#CV #metric #loss #segmentation 
## Intersection over union, Jaccard Index 
Пусть $P$ - это предсказанная маска, а $G$ - это ground truth.
$$\text{IoU}=\frac{|P \cap G|}{|P \cup G|}$$
Если классов много, то усредняем по классам.

![[Pasted image 20230211211118.png]]

![[Pasted image 20230211211138.png]]

**Примечание**: можно использовать как $\text{loss} = 1 - \text{IoU} \rightarrow min$. Преимуществом над [[Cross Entropy]] является лучшая работа с imbalanced classes ([Ссылка на источник](https://stats.stackexchange.com/questions/321460/dice-coefficient-loss-function-vs-cross-entropy)) правда градиенты считаются сложнее чем [[Cross Entropy]], поэтому автор заметки предпочитают использовать именно её с весами на недопредставленные классы.