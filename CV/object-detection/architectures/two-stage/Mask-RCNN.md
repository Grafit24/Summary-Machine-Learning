#CV #object-detection #segmentation #architecture #two-stage-detector 
[Medium](https://medium.com/codex/a-guide-to-two-stage-object-detection-r-cnn-fpn-mask-r-cnn-and-more-54c2e168438c)
## Mask-RCNN
Mask-RCNN - это модификация [[Faster-RCNN]] с дополнительными конволюциями к классификации для [[Instance Segmentation]]. То есть для каждого proposal (на 2 этапе) теперь три выход - bbox, class, mask.
- [[ROI Pooling]] $\rightarrow$ [[ROI Align]]: [[Bilinear Interpolation]]

![[Pasted image 20230220202327.png]]

> A fully convolutional network (FCN) is used to draw m × m mask from each RoI.