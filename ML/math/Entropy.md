---
tags:
  - ML
  - math
---
## Surprice
"Surprice" is a measure of how surprised we are to observe a particular outcome. Outcomes that are more likely have lower surprice, while unlikely outcomes have higher surprice.. When we have r.v. $X$ with possible outcome $x$ with $p(x)=1$, it means that we aren't surpriced at all by this outcome!

$$\text{Surprice(x)}=log_2(\frac{1}{p(x)})$$
## Entropy
**Entropy** is the average of "surprice" of r.v. outcomes. 

$$\text{Entropy(X)}=H(X)=E[\text{Surprice}(X)]=\sum_{x \in X}\log_2{\frac{1}{p(x)}}p(x)=-\sum_{x \in X}p(x)\log_2{p(x)}$$
$$H(X)=-\sum_{x \in X}p(x)\log_2{p(x)}$$

**Continuous r.v.**:
$$\mathrm{H}(X)=\mathbb{E}[-\log f(X)]=-\int_{\mathbb{X}}f(x)\log f(x)\,\mathrm{d}x.$$