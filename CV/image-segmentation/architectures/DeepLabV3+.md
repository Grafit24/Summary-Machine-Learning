#CV #segmentation #architecture 
[Guide](https://learnopencv.com/deeplabv3-ultimate-guide/) [Paper](https://arxiv.org/pdf/1802.02611v3.pdf)
### Main ideas (upgrade [[DeepLabV3]]):
- Add decoder part similiar to UNet
- ResNet -> Aligned [[Xception]]
- [[Xception]] change poolings to atrous depth-wise separable convolutions.

### Architecture:
- **Backbone**: Aligned [[Xception]]
- **Encoder**: [[DeepLabV3]]
- **Decoder**: Concat + [[Bilinear Interpolation]] + [[Convolution]]

![[Pasted image 20230216215958.png]]

![[Pasted image 20230227223905.png]]