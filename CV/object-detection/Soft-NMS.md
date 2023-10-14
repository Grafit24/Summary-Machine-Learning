#CV #object-detection 
[Paper](https://arxiv.org/abs/1704.04503) [PaperWithCode](https://paperswithcode.com/method/soft-nms)
## Soft-NMS
**Soft-NMS** имеет целью тоже самоее, что и [[NMS]], но с тем отличием, что Soft-NMS вместо того, чтобы отбрасывать только понижает confidence с помощью непрерывной функции по [[IoU]].

![[Pasted image 20230301221150.png|500]]
Мотивация использования Soft-NMS заключается в том, что рядом с друг другом могут находиться несколько объектов одного класса.

![[Pasted image 20230301222648.png|500]]

Алгоритм:
![[Pasted image 20230301222517.png|500]]