---
tags:
  - NLP
  - augmentation
---
## How to get more data in text domain?
- word dropout
	- Dropout around 10% of words and replace it (randomly or UNK)![[Pasted image 20230914151342.png]]
	- Similar in #CV domain is masking![[Pasted image 20230914151909.png]]
- use external resources
	- replace some words by synonymous![[Pasted image 20230914151510.png]]
- use separate models
	- for example double translation [[Seq2Seq]] (from src to src with intermediate language)![[Pasted image 20230914151713.png]]
	- Similar to CV domain is geometric transformations![[Pasted image 20230914151734.png]]