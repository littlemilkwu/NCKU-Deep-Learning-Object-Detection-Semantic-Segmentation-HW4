## Objective
The goal of this assignment is to design and implement a deep learning model capable of performing both object detection and semantic segmentation simultaneously, using two distinct datasets. Traditionally, instance or panoptic segmentation can be used to learn both object detection and segmentation tasks from the same image. However, unlike these traditional methods, this assignment requires the use of two separate datasets: one for object detection and another for semantic segmentation.

## Key Tasks
1. Design a network architecture that can produce both semantic segmentation and object detection results. Please note that the output should not be panoptic or instance segmentation results. If you are unsure of the difference, please consult with the teaching assistant.
2. Your network must be able to learn object detection and semantic segmentation capabilities from two different datasets respectively. Therefore, you will need to modify the dataloader to read and train from these two datasets separately. Be aware that during training for object detection, the weights learned for semantic segmentation might be forgotten. To tackle this, you could consider alternating learning (switching tasks every iteration), or first mastering one task before moving on to the next, using a relatively lower learning rate to avoid catastrophic forgetting, a known issue in deep learning.

## Hints:
1. To address the first task, you could consider starting with an existing instance or panoptic segmentation network, and removing the instance or panoptic head to meet the requirements. This approach would necessitate writing your own segmentation/detection loss. Alternatively, you could choose any state-of-the-art (SOTA) object detection network and add a new segmentation head (or even a neck) to it. This would only require the addition of a segmentation loss.
2. For training with different datasets, the simplest approach would be to use the same code but with two dataloaders, and alternate between them as needed. Each training session would start by reading the weights from the last checkpoint. Another tip is that once the training has yielded some results, you can freeze the parameters of the earlier layers (or set a very low learning rate) to prevent the model from forgetting previously learned weights.

## Dataset
1. Object Detection: VOC2007 (20 categories, 9,963 images) [https://drive.google.com/drive/folders/1TrJjsoIZ3QWecvOLGKCSa4NBk3qnObin?usp=share_link]
2. Semantic Segmentation: ADE20K (150 categories, 2,000 images) [https://drive.google.com/drive/folders/1hRy6am8KeUWW_6sgj46_Qk7_vbWDWhRT?usp=share_link]

### Duplicated Images
* AED_val_00001280, 81, 82, 83, 85 (1)

### ADE SceneParse150 list
[google sheet](https://docs.google.com/spreadsheets/d/1se8YEtb2detS7OuPE86fXGyD269pMycAWe2mtKUj2W8/edit#gid=0)

### Reference
[iterate over two dataloaders simultaneously](https://stackoverflow.com/questions/51444059/how-to-iterate-over-two-dataloaders-simultaneously-using-pytorch)
[YOLOv4 介紹-台灣人工智慧學校](https://aiacademy.tw/yolo-v4-intro/)