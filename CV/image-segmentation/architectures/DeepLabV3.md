#CV #segmentation #architecture 
[Paper](https://arxiv.org/pdf/1706.05587.pdf)
**Main ideas**:
- [[Dilated Convolution]]
	- [[Receptive Field]]
- [[Spatial Pyramid Pooling]] (Atrous SPP / ASPP)

![[Pasted image 20230220190540.png]]

1. В backbone (В статье в качестве backbone используется [[ResNet]]) мы меняем output stride с помощью [[Dilated Convolution|dilated convolutions]] так чтобы увеличить spatial resolution на последних слоях backbone и сделать [[Receptive Field|receptive field]] на последнем слое шире.

> The motivation behind this model is that the introduced striding makes it easy to capture long range information in the deeper blocks.


2. Используется ASPP для того чтобы собирать контекст на различных маштабах feature map. Так как при слишком большом rate [[Dilated Convolution|dilated convolution]] деградируется до свертки 1x1 испольуется [[Global Average Pooling]]. (См. fig. 4)

>However, we discover that as the sampling rate becomes larger, the number of valid filter weights (i.e., the weights that are applied to the valid feature region, instead of padded zeros) becomes smaller.

4. После ASPP идёт concat и свёртка 1 на 1 для приведения к нужному кол-во каналов. После этого всего используется [[Bilinear Interpolation|bilinear interpolation]] приводящая предсказанную маску к исходному разрешению изображения.

>**output stride** - это отноешние input image spatial resolution к final output resolution.