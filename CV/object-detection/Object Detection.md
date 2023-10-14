#object-detection #CV 
[Презентация DL Adv](https://algocode.ru/files/course_dladvspring23/ObjectDetection.pdf) [Запись лекции](https://www.youtube.com/watch?v=_mOjD29vLE4)
## Object detection task

![[Pasted image 20230220190844.png]]

**Object detection** - это instance localization + classification task.

**Metrics**:
- [[Precision]]
- [[Recall]]
- [[F-score]]
- [[mAP]]

**Classical Approach - Sliding window**
![[Pasted image 20230228235436.png|500]]
- Градиент для картинке это то насколько картика быстро меняется. Например переход между черным и белым высокий.
- Sliding window + Feature Extractor : [[HOG]] + Classifier : [[SVM]]

**Non-maximum supression** methods
- Фильтрация лишних предсказаний.
- [[NMS]]: это алгоритм, который используется для выбора небольшого кол-ва bbox'ов из мн-ва предсказанных, которые лучшим образом (по мнению модели) локализуют предсказанные им объекты.
- [[Soft-NMS]]: имеет целью тоже самоее, что и [[NMS]], но с тем отличием, что Soft-NMS вместо того, чтобы отбрасывать только понижает confidence с помощью непрерывной функции по [[IoU]].

**[[Anchors]]**:
- Шаблонные bbox примерно подходящий на ground truth bboxes.
- Как посчитать anchor bboxes? С помощью kmeans на всем датасете.

## Архитектуры нейронных сетей

**Two-stage detectors**:
- [[R-CNN]]
- [[Fast-RCNN]]
- [[Faster-RCNN]]
- [[Mask-RCNN]]

**One-stage detectors**:
- [[YOLO]]
- [[SSD]]
- [[RetinaNet]]

**[[Anchors]] free detectors**:
- [[YOLO]]
- [[FCOS]]

## Обучение нейронных сетей

**Augmentations**:
- Mixup, Cutout, Cutmix![[Pasted image 20230220205306.png]]

**Losses**:
- [[GIoU]] - призвана быстро стягивать ground truth bbox с предсказанным.
- [[DIoU]] - точна такая же идея, только используется центры
- [[CIoU]] - модификация [[DIoU]]