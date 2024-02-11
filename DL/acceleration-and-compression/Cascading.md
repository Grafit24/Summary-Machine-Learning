---
tags:
  - acceleration
  - NLP
  - CV
  - --draft
---
## Description
Cascading aims to speed up inference by using a prediction probability from an internal hidden layer. If the model's confidence in its prediction meets the predetermined threshold, we stop the process. If not, it moves on to the next layer. This approach helps save computational resources and time.

![[Pasted image 20240210013715.png]]

While training for every prediction hidden layer we set prediction head, and sum loss from every such head.
## Adaptive Computation Time
We introduce an additional layer on top of each existing layer to estimate a halting score. In a standard training pipeline, we would only stop at the last layer, where precision is typically highest. To encourage earlier stopping and enhance efficiency, we introduce regularization. This penalizes layers that stop too late in the process, thereby pushing the model to make confident predictions sooner.

![[Pasted image 20240210014505.png]]

#TODO Uncertainty estimation to get layer when we need to stop. Isotonic regression, calibration.