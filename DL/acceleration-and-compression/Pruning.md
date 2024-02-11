---
tags:
  - NLP
  - CV
  - compression
---
[Arxiv](https://arxiv.org/abs/1712.01312)
[Head Pruning](https://lena-voita.github.io/posts/acl19_heads.html)
## Description
The core idea is determine not important weights and prune it without big drawdowns in quality.

![[Pasted image 20240210200748.png]]

## $L_0$ regularization or discrete choices inside neural network

>How should we chose what weight is need to switch off?

We use special trainable scalars for every weight $g_i$ - **gates**, but they are different to [[LSTM]] gates, because they are specific to weights and independent to input. 

We are want to apply $L_0$ norm to $g_i$ scalars that equals to a number of non-zero componets and would push model to swith off less important weights. Unfortunately, the $L_0$ norm is nondifferentiable, so we use a stochastic relaxation.

$g_i$ is random variable drawn independently from a weight-specific [Hard Concrete distribution](https://openreview.net/pdf?id=H1Y8hhg0b) with trainable parameter $\log{(α)}$. The distributions have non-zero probability mass at 0 and 1 ([Illustration](https://lena-voita.github.io/posts/acl19_heads.html)). 

We use the sum of probabilities of weights ($L_c$) being non-zero as a stochastic relaxation of the non-differentiable $L_0$ norm.

$L = L_{obj} + \lambda L_c$

When applying the regularizer, we start from the converged model trained without the $L_c$ penalty and then add the gates and continue training the full objective. By varying the coefficient λ in the optimized objective, we obtain models with **different numbers of retained weights**.

> **Note**: We can add $gate$ not only for weights, but for heads, layers and anything we want it method for trainable discrete choice.