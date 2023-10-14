#CV #object-detection #segmentation  #architecture #two-stage-detector #feature-extractor #-raw
[Medium]()
## FPN
> Feature Pyramid Network (**FPN**) is a feature extractor designed for such pyramid concept with accuracy and speed in mind. It replaces the feature extractor of detectors like Faster R-CNN and generates multiple feature map layers (**multi-scale feature maps**) with better quality information than the regular feature pyramid for object detection.

> FPN provides a top-down pathway to construct higher resolution layers from a semantic rich layer.

![[Pasted image 20230302221244.png]]

![[Pasted image 20230302220736.png]]

## FPN with [[Region Proposal Network|RPN]]
> FPN is not an object detector by itself. It is a feature extractor that works with object detectors.

![[Pasted image 20230302221039.png]]

> The same head is applied to all different scale levels of feature maps.

## FPN with [[Faster-RCNN]]

> In FPN, we generate a pyramid of feature maps. We apply the RPN (described in the previous section) to generate ROIs. Based on the size of the ROI, we select the feature map layer in the most proper scale to extract the feature patches.

![[Pasted image 20230302221451.png]]

## FPN with [[Mask-RCNN]]
%%Сам не очень понимаю, как это работает%%

> Just like Mask R-CNN, FPN is also good at extracting masks for image segmentation. Using MLP, a 5 × 5 window is slide over the feature maps to generate an object segment of dimension 14 × 14 segments. Later, we merge masks at a different scale to form our final mask predictions.

![[Pasted image 20230302221814.png]]