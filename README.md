# Trafic signs detection using YOLOv7

## 1. Dataset 

For this project was used dataset from site https://www.vicos.si/resources/dfg/. This annotated dataset consists of 199 traffic sign categories captured in Slovenian roads. Each category has at least 20 instances. Only images containing at least one traffic sign were selected from the vast corpus of collected data for this dataset. Moreover, the selection was performed in such a way that there is usually a significant scene change between any pair of selected consecutive images. There are both ordinary photos of roads and augmented images. Additional augmentation dataset was created by inserting cropped instances of traffic signs. Due to the large amount of data and technical limitations, it was not possible to use all of them.

<img width="351" alt="Снимок экрана 2022-12-03 в 17 26 48" src="https://user-images.githubusercontent.com/111921768/205451116-2cfe2768-e2ad-4c07-a774-6569f835c530.png">

 
## 2. Model 

I have chosen YOLO model architecture (a single-stage real-time object detector), as one of the most popular architecture models, because of the following advantages:

- The computation and processing speed of YOLO is quite high, especially in real-time compared to most of the other training methods and object detection algorithms. 
- Apart from the fast computing speed, the YOLO algorithm also manages to provide an overall high accuracy with the reduction of background errors seen in other methods. 
- The architecture of YOLO allows the model to learn and develop an understanding of numerous objects more efficiently. 

YOLO has different versions. Firstly I used version YOLOv5 for my project, but finally I choosed last version. YOLOv7 was introduced to the YOLO family in July 2022. YOLOv7 is the fastest and most accurate real-time object detection model for computer vision tasks. The official paper demonstrates how this improved architecture surpasses all previous YOLO versions — as well as all other object detection models — in terms of both speed and accuracy on the MS COCO dataset; achieving this performance without utilizing any pretrained weights.

<img width="675" alt="Снимок экрана 2022-12-01 в 12 05 59" src="https://user-images.githubusercontent.com/111921768/205037219-7b5e0f60-2c8f-46dc-9ca6-c67e95bc68b9.png">

## 3. Prepearing data 

As annotation of aforementioned dataset is in COCO .json format, it is necessary to change the data in accordance with the requirements of the Yolov7 model. YOLO and related models require that the data used for training has each of the desired classifications accurately labeled, usually by hand. YOLOv7 expects annotations for each image in form of a .txt file where each line of the text file describes a bounding box (x, y, width, height). I chose to use RoboFlow for this purpose. The tool is free to use online, quick, can perform augmentations and transformations on uploaded data to diversify the dataset, and can even freely triple the amount of training data based on the input augmentations. 

<img width="1338" alt="Снимок экрана 2022-12-01 в 12 48 42" src="https://user-images.githubusercontent.com/111921768/205045339-b1d889f6-42d4-493b-9caa-2efe11a353a5.png">

I uploaded more then 8k images and used RoboFlow capabilities to rename all classes and and expanded the dataset using built-in augmentation to the over 20 k images. Entire dataset was splited to train/test/validate sets. All these prepared data were used to train YOLOv7 model using Gogle Colab. 

## 4. Training model

First training attempt was with YOLOv5. I've run 150 epochs, but scores haven't increased much over the past 50 epochs. 

<img width="696" alt="Снимок экрана 2022-12-03 в 19 40 24" src="https://user-images.githubusercontent.com/111921768/205456775-7e916499-71fb-4db3-bc1d-6e4976387307.png">

YOLOv7 is training match longer, but scores were slightly better. It was needed to split epoches in 10 to prevent interruptions.

## 5. Evaluation metric

To evaluate object detection models like YOLO, the mean average precision (mAP) is used. The mAP compares the ground-truth bounding box to the detected box and returns a score. The higher the score, the more accurate the model is in its detections. The mean of average precision(AP) values are calculated over recall values from 0 to 1.

mAP formula is based on the following sub metrics:

- Confusion Matrix,
- Intersection over Union(IoU),
- Recall, 
- Precision

To create a **confusion matrix**, we need four attributes: True Positives (TP) , True Negatives (TN), False Positives (FP), False Negatives (FN).

**Intersection over Union** indicates the overlap of the predicted bounding box coordinates to the ground truth box. Higher IoU indicates the predicted bounding box coordinates closely resembles the ground truth box coordinates.

**Precision** measures the proportion of predicted positives that are actually correct. If you are wondering how to calculate precision, it is simply the True Positives out of total detections. Mathematically, it’s defined as follows. P  =  TP/(TP + FP) 

**Recall** measures the proportion of actual positives that were predicted correctly. It is the True Positives out of all Ground Truths. Mathematically, it is defined as follows. R = TP / (TP + FN) 

## 6. Evaluating models 

mAP on validation set after training YOLAv5 model was **0.759** (mAP50-95 -- average precision for IoU from 0.5 to 0.95).

<img width="959" alt="Снимок экрана 2022-12-03 в 19 42 18" src="https://user-images.githubusercontent.com/111921768/205457897-b6a8e1ae-104c-468f-b8be-4236aa95ec52.png">

mAP on validation set after training YOLAv5 model was **0.822** (mAP50-95 -- average precision for IoU from 0.5 to 0.95).

<img width="956" alt="Снимок экрана 2022-12-05 в 23 02 00" src="https://user-images.githubusercontent.com/111921768/205760821-c3725912-f5fb-49d7-94d0-4af94e96a25c.png">

## 7. Conclusion

After my tries to train YOLOv7 model my best mAP on vatidation set was around 0.81. I think can be better and first of all I would work with dataset as  some instanses are over represented and others are under represented, it is worth to make the dataset more representative. 

<img width="929" alt="Снимок экрана 2022-12-04 в 14 15 13" src="https://user-images.githubusercontent.com/111921768/205492632-89bdf4d0-566f-429b-a7fc-17f4f85c4c83.png">

<img width="914" alt="Снимок экрана 2022-12-04 в 14 09 59" src="https://user-images.githubusercontent.com/111921768/205492440-b05a47dd-f630-4031-b14f-85d31739adca.png">

Also I think that model can be trained better, but for this more capabilities are needed, as I faced a lot of troubles with training this model. It took a lot of time and RAM. Every epoch takes aroun 17 minutes and to train model till mAP equal 0.8 around 30 epochs are needed. It is around 8.5 hours in total. 

## 8. Sources

1. [YOLOv7 GitHub](https://github.com/WongKinYiu/yolov7.git)
2. [Dataset](https://www.vicos.si/resources/dfg/)
3. [Robofrlow for annotation](https://roboflow.com/formats)


