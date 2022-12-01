# Trafic signs detection using YOLOv7

1. Dataset 

For this project was used dataset from site https://www.vicos.si/resources/dfg/. This annotated dataset consists of 199 traffic sign categories captured in Slovenian roads. There are both ordinary photos of roads and augmented images. Additional augmentation dataset was created by inserting cropped instances of traffic signs. Due to the large amount of data and technical limitations, it was not possible to use all of them.
 
2. Сhoosing a model 

I chose model YOLOv7 my project. It is the fastest and most accurate real-time object detection model for computer vision tasks. The official paper demonstrates how this improved architecture surpasses all previous YOLO versions — as well as all other object detection models — in terms of both speed and accuracy on the MS COCO dataset. 

<img width="675" alt="Снимок экрана 2022-12-01 в 12 05 59" src="https://user-images.githubusercontent.com/111921768/205037219-7b5e0f60-2c8f-46dc-9ca6-c67e95bc68b9.png">

3. Prepearing data 

As annotation of aforementioned dataset is in COCO .json format, it is necessary to change the data in accordance with the requirements of the Yolov7 model. YOLO and related models require that the data used for training has each of the desired classifications accurately labeled, usually by hand. YOLOv7 expects annotations for each image in form of a .txt file where each line of the text file describes a bounding box (x, y, width, height). I chose to use RoboFlow for this purpose. The tool is free to use online, quick, can perform augmentations and transformations on uploaded data to diversify the dataset, and can even freely triple the amount of training data based on the input augmentations. 

<img width="1338" alt="Снимок экрана 2022-12-01 в 12 48 42" src="https://user-images.githubusercontent.com/111921768/205045339-b1d889f6-42d4-493b-9caa-2efe11a353a5.png">

I uploaded more then 8k images and used RoboFlow capabilities to rename all classes and and expanded the dataset using built-in augmentation to thw over 20 k images. Entire dataset was splited to train/test/validate sets. All these prepared data were used to train YOLOv7 model using Gogle Colab. 





