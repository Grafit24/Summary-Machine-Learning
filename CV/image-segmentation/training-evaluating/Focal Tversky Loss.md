#CV #loss #segmentation 
[Medium](https://towardsdatascience.com/dealing-with-class-imbalanced-image-datasets-1cbd17de76b5)
## [[Focal Loss]] + [[Tversky Loss]]
$$\text{FTL}=(1-\text{TI})^\gamma$$
Нелинейность данного лосса даёт контроль над тем как себя будет лосс при различных зн-ях $\text{TI}$.

>In the case of class imbalance, the FTL becomes useful when γ > 1. This results in a higher loss gradient for examples where TI < 0.5. This forces the model to focus on harder examples, especially small scale segmentations which usually receive low TI scores.

![[Pasted image 20230213223620.png]]