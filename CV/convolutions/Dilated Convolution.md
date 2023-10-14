#CV 
[Источник](https://www.inference.vc/dilated-convolutions-and-kronecker-factorisation/)
## Dilated (atrous) convolution
Обычные конволюции страдают от проблемы интегрирования глобального контекста, в частности проблемой этого является [[Receptive Field]]. Для решение этой проблемы в частности и используется Dilated conv, которая позволяет увеличивать RF экспоненциально, при линейном увелчение параметров (В случае классической конволюции RF растёт линейно вместе с кол-вом параметров). Также применение DC позволяет сохранить сохранить св-во translation equivariant (в отличие от [[Spatial Pyramid Pooling|spatial pooling]]).

У CNN есть проблема на краях изображения, где conv needs to be padded. Ну так вот у DC всё ещё хуже.

![[dilation.gif]]
No padding, no stride, dilation=2

![[Pasted image 20230216182334.png]]
