---
tags:
  - ML
  - math
---
**Kullback-Leibler Divergence** is a measure of how distribution, $Q$ different from distribuiton $P$. 

>**Intuitive**: KL divergence quantifies the amount of information loss when distribution Q is used to approximate distribution P. It essentially tells us the 'cost' of mistaking P for Q.

$\chi$ is sample space of discrete pdf $P$ and $Q$.

$$D_{\mathrm{KL}}(P\mid\mid Q)=\sum_{x \in \chi}{P(x)\log{\frac{P(x)}{Q(x)}}}$$

Key things:
- KL Divergence is not symmetric. In other words, the divergence of $P$ from $Q$ is not the same as the divergence of Q from P. $D_{\mathrm{KL}}(P\mid\mid Q)\neq D_{\mathrm{KL}}(Q\mid\mid P)$
- KL Divergence is always non-negative, which means it's zero if and only if $P$ and $Q$ are the same distribution.