# EfficientNet
[Explained Video](https://www.youtube.com/watch?v=3svIm5UC94I&t=123s)
[Источник](https://arxiv.org/pdf/1905.11946.pdf)
#CV #непонял  #architecture 
## Как я понял
Идея заключается в том, чтобы подобрать такие коэффиценты $w$-width,  $r$ - resolution, $d$-depth так, чтобы модель увеличивалась эффективнее. Мы берём baseline модель и подбираем ей эти коэффиценты увеличивающие соответсвующую часть нейросети.

![[efficientnet1.png]]
![[efficientnet2.png]]