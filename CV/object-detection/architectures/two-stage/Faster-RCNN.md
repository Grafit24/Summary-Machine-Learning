#CV #object-detection #architecture #two-stage-detector 
[Medium](https://towardsdatascience.com/r-cnn-fast-r-cnn-faster-r-cnn-yolo-object-detection-algorithms-36d53571365e)
## Faster-RCNN
Как [[Fast-RCNN]], но вместо [[Selective Search|selective search]] используется нейросеть, а именно [[Region Proposal Network]]. После получения proposals используется [[RoI Pooling]] для решейпа к fixed-size и передается в классификатор. 

![[Pasted image 20230220201934.png]]
![[Pasted image 20230302170955.png]]

### Region Proposal Network
Sliding window $k$ anchor boxes проходиться по feature map и для каждого предсказывается $2k$ scores ([[Anchors|anchor bbox]] содержит какой-нибудь объект или нет) и $4k$ coordinates.  

![[Pasted image 20230220202145.png]]
