---
tags:
  - NLP
  - CV
  - acceleration
  - compression
---
## Description
1. Take best model that you can - **Teacher**
2. Using predictions of **Teacher** train small model - **Student**
	- Using [[KL Divergence]] as objective, trying to aproximate **Teacher** prediction
	- [[MSE]] for regression
	- Note: Distilation can be learned on unlabled data

![[Pasted image 20240210003717.png]]

### Student Architecture
Student architecture choices: 
- **Naïve**: same but smaller, less layers / hidden units 
- **Factorized**: product of smaller matrices or tensors (like [[LoRA]])
- **Sparse**: only a small (random) subset of weights are nonzero
	- only store random seed and nonzero weights
	- compute is sparse matrix multiply

### Tricks
- [Ensemble distillation](https://arxiv.org/abs/1702.01802) 
- [Dropout distillation](http://proceedings.mlr.press/v48/bulo16.pdf)
- [Co-distillation](https://arxiv.org/abs/1804.03235)
