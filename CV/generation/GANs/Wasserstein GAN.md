#CV #generation #architecture #gan #-future-return
[WGAN](https://arxiv.org/pdf/1701.07875.pdf?ref=paperspace-blog) [WGAN-GP](https://arxiv.org/pdf/1704.00028.pdf?ref=paperspace-blog) [PaperWithCode](https://paperswithcode.com/method/wgan) [Implementation](https://blog.paperspace.com/wgans/#understanding-wgans) [Medium](https://jonathan-hui.medium.com/gan-wasserstein-gan-wgan-gp-6a1a2aa1b490)
## WGAN
Мотивация к созданию WGAN была проблема [[GAN|GAN'а]], а именно unstable learning, вызванный сильной дисперсией градиентов при альтернативном способе задания лосса генератора, который призван решить проблему исчезающих градиентов
- ![[Pasted image 20230307162754.png]]
- ![[Pasted image 20230307162759.png]]

Вместо этого WGAN меняет лосс, как видно она имеет более гладкие граденты везде.
![[Pasted image 20230306192907.png|500]]

Проблемы которые частично решает WGAN (то есть улучшается стабильность обучения):
- mode collapse. Модель не может производить уникальные изображения и повторяется, в патернах и в качестве.
- convergence failure. Модель не может производить оптимальных или хороших результатов.
- Генератор может продолжать обучаться, даже когда критик хорошо работает

Для решения данных проблем в частности и применяется WGAN и Wasserstein-1 distance или Earth-Mover (EM) distance. EM distance интуитивно представляет из себя цену самого дешёвого способа транспортировки "массы", для трансформации $\mathbb{P}_g$ в $\mathbb{P}_r$.

![[Pasted image 20230307161402.png]]
inf = infimum (**и́нфимумом**) - самый низкий из мн-ва
$\prod$ содержит в себе все возможные транспортные планы $\gamma$.
$\gamma(x, y)$ - это joint distibution.


![[Pasted image 20230306193525.png|300]]

Лосс функция на EM основе:

![[Pasted image 20230306184522.png]]
$\mathcal{D}$ - это мн-во 1-Lipschitz функций. $\mathbb{P}_r$ - реальное распределнние  $\mathbb{P}_g$ - распределение модели, косвенно определённое $\tilde{x}=G(z)$.

Дискриминатор $\rightarrow$ критик (critic). Это следует из того, что дискриминатор теперь производит не дискретный выход, а выдаёт оценку, то есть непрерывный выход.

Задачей критика является максимизация расстояние между распределением реальных изображения и сгенерированных и делает он это как бы максимизируя разность между их оценками.
Задачей же генератора является минимизровать это расстояние.

![[Pasted image 20230306183934.png]]

1-Lipschitz constrint:
![[Pasted image 20230307163133.png]]

Чтобы наложить Lipschitz constraint на критика предлаегается использовать [[weight clipping]] для того, что веса лежали в compact space $[-c, c]$. Мн-во функций удовлетворяющих этому ограничению это подмножество k-Lipschitz функций для некоторого k, который зависит от $c$ и архитектуры критика. Этот метод имеет ряд проблем в частности он сильно зависит от выбора $c$, поэтому используется Gradient Penalty

GAN:
![[Pasted image 20230307163203.png]]

WGAN:
![[Pasted image 20230307163156.png]]

![[Pasted image 20230307163212.png]]

## WGAN-GP (Gradient Penalty)

Использование [[weight clipping]] приводит к тому что архитекстура нейронной сети пытается достичь максимальной норма градинета $k$ в конечном итоге освоивают простые  функции.
![[Pasted image 20230306185834.png]]
> We observe that the WGAN optimization process is difficult because of interactions between the weight constraint and the cost function, which result in either vanishing or exploding gradients without careful tuning of the clipping threshold c.

>Weight clipping is a clearly terrible way to enforce a Lipschitz constraint. If the clipping parameter is large, then it can take a long time for any weights to reach their limit, thereby making it harder to train the critic till optimality. If the clipping is small, this can easily lead to vanishing gradients when the number of layers is big, or batch normalization is not used (such as in RNNs) … and we stuck with weight clipping due to its simplicity and already good performance.

Одно из желательных св-в для $f^*$ (оптимальный критик) это иметь норму градиента 1 почти везде в пределах  $\mathbb{P}_r$ и $\mathbb{P}_g$.

> A differentiable function is 1-Lipschtiz if and only if it has gradients with norm at most 1 everywhere, so we consider directly constraining the gradient norm of the critic’s output with respect to its input.

![[Pasted image 20230306191033.png]]

**Sampling distribution**. $\hat{x}=\epsilon x + (1-\epsilon)\tilde{x}$,    $\epsilon$ ~ $U[0, 1]$. 

**Penalty coefficient**. $\lambda = 10$ оптимальный.

**No critic batch normalization**. BN меняет форму проблемы дискриминатор дискриминатор с отбражения 1 к 1 в отбражения batch в batch. GP не валидно в таком сетапе, потому что он регулиризирует норму critic grdient по отношению к каждому входному сигналу, а не к батчу.

> Our method works with normalization schemes which don’t introduce correlations between examples. In particular, we recommend layer normalization as a drop-in replacement for batch normalization

> **Two-sided penalty**. We encourage the norm of the gradient to go towards 1 (two-sided penalty) instead of just staying below 1 (one-sided penalty). Empirically this seems not to constrain the critic too much, likely because the optimal WGAN critic anyway has gradients with norm 1 almost everywhere under Pr and Pg and in large portions of the region in between.

![[Pasted image 20230306181017.png]]
