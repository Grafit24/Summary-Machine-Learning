#CV #loss #segmentation 
[Medium](https://towardsdatascience.com/dealing-with-class-imbalanced-image-datasets-1cbd17de76b5) [Paper](https://arxiv.org/abs/1706.05721)
## Tversky Loss – [[Dice|Dice Loss]] Generalization
Tvesky Index - это обощение [[IoU|Jaccard index (IoU)]] и [[Dice|dice coefficient]].
Пусть $P$ - это предсказанная маска, а $G$ - это ground truth.
$$\text{TI}=\frac{TP}{TP+\alpha FP + \beta FN}, \quad \alpha+\beta=1$$
$\text{TI}$ упрощается до [[IoU|Jaccard index (IoU)]] при $\alpha=\beta=1$.
$\text{TI}$ упрощается до [[Dice|Dice coefficient]] при $\alpha=\beta=0.5$.

$\text{TI}$ позволяет выбирать между тем чтобы наказывать больше за высокий $FN$ или $FP$.

>By setting the value of α > 𝜷, you can penalise false negatives more. This becomes useful in highly imbalanced datasets where the additional level of control over the loss function yields better small scale segmentations than the normal dice coefficient.

Tversky Loss:
$$\text{TverskyLoss}=1-\text{TI} \rightarrow min$$

![[Pasted image 20230213214718.png|200]]
![[Pasted image 20230213214726.png|300]]
![[Pasted image 20230213214746.png|]]
