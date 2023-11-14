---
tags:
  - CV
  - segmentation
  - foundation
  - transformer
---
[Demo](https://segment-anything.com/demo#) [Paper](https://scontent-ber1-1.xx.fbcdn.net/v/t39.2365-6/10000000_900554171201033_1602411987825904100_n.pdf?_nc_cat=100&ccb=1-7&_nc_sid=3c67a6&_nc_ohc=xR1OWwGm-aYAX8ciwij&_nc_ht=scontent-ber1-1.xx&oh=00_AfC1rLj9K5a1uEESVFHQailqYIgTZgjSvAz0ZT3lJ1nxew&oe=6557B3A7)
## Что умеет?
- Сегментировать интерактивно, по точкам, которая указывают что надо включить. Также можно указыватьс помощью bbox.
- Когда присутсвует не определённость в сегментации, SAM может предоставлять несколько вариантов масок.
- SAM способен определять маски для всех объектов на изображение автоматически, без дообучения.
- SAM может вычислять image embeddings и использовать их для сегментации в real-time.

##  Архитектура
![[Pasted image 20231114145229.png]]
- **Image encoder**. Pretrained [[ViT]] on [[Masked Auto-Encoder]] task.
- **Prompt encoder**. Two sets of prompts: sparse(points, boxes, text) and dense (mask)
	- **Sparse**. Represents points and boxes by positional encodings + learned embeddings for each prompt type. For text using [[CLIP]] embeddings.
	- **Dense**. Conv + Image embeddings (fig. 4)
- **Mask decoder**. Modification of a Transformer decoder block followed by a dynamic mask prediction head.
- **Resolving ambiguity.** 3 masks prediction. Backprop only for mask with minimum loss (mask predicted most accurately).
- **Losses**. Linear combination of [[Focal Loss]] and [[Dice|Dice Loss]]. 
- **Training**. We train for the promptable segmentation task using a mixture of geometric prompts like "segment the circular objects" or "find the rectangular shapes". Simulate an interactive setup by randomly sampling prompts in 11 rounds per mask, allowing SAM to integrate seamlessly into our data engine.