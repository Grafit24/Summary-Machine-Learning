#CV #loss #segmentation 
[PapersWithCode](https://paperswithcode.com/method/focal-loss) [Implementation](https://github.com/qubvel/segmentation_models.pytorch/blob/8523324c116dcf7be6bddb73bf4eb1779ef6e611/segmentation_models_pytorch/losses/focal.py#L48)
## Описание

>down weights easy examples

Focal Loss это модификация [[Cross Entropy|Binary Cross Entropy]] целью которой является решение пробелемы extremly imbalanced classes. FL создавался так чтобы занижать вес лёгких примеров и фокусировать внимание модели на сложных. Он динамически маштабирует (scale) [[Cross Entropy]], так чтобы чем больше модель уверена в правильном классе тем ближе был коэффицент маштабирования $(1-p_t)^\gamma$ к нулю. 
Обобщение на [[Classification|Multi-class]] происходит через стратегию [[Classification|OneVsAll]].
$$p_t = \left\{\begin{matrix}p \quad \space if \space y=1 
 \\ 1-p \quad otherwise
\end{matrix}\right.$$
$$\text{FL}(y, p)=\text{FL}(p_t)=-\alpha_t(1-p_t)^\gamma \log{p_t}$$

![[Pasted image 20230213201003.png|500]]