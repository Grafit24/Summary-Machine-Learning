#CV #object-detection 
[Source](https://learnopencv.com/histogram-of-oriented-gradients/)
## Histogram of Oriented Gradients
HOG is **feauture discriptor**. It is used in computer vision and image processing for the purpose of object detection. 

> The technique counts occurrences of gradient orientation in the localized portion of an image.

![[Pasted image 20230301165611.png]]

1. Get an image patch
![[Pasted image 20230301165800.png]]
2. Gamma-correction (Optional)
![[Pasted image 20230301165834.png]]
3. Compute gradients using convolution with x-derivate and y-derivate filters
	- Изображения переводится из RGB в GrayScale перед вычислением
![[Pasted image 20230301165908.png]]
4. Constuct the histogram using magnitude and direction of gradient
	- $\text{Direction}=g=\sqrt{g^2_x+g^2_y}$
	- $\text{Magnitude}=\theta=arctg\frac{g_y}{g_x}$
![[Pasted image 20230301192440.png]]
5. L2 Normalization of blocks
![[Pasted image 20230301193001.png]]
6. Concatenate vectors in one large vector