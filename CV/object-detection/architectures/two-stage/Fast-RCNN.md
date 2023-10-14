#CV #object-detection #architecture #two-stage-detector 
## Кратко
**Fast-RCNN** это как очевидно более быстрая [[R-CNN]] (без SVM) ведь теперь всё изображение сначало проходит через некоторый backbone (DeepConvNet), а после bbox'ы (полученные с помощью [[Selective Search|selective search]]) с помощью [[RoI Projection]] проецируются на feature map в конце backbone. После чего передаётся [[RoI Pooling]] для решейпа к fixed-size. 

![[Pasted image 20230220200655.png]]
FCs - fully connected

**Примечение**. [[ROI Pooling]] по сути Вытаскивание фичу в нужном размере.