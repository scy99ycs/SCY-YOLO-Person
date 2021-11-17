# SCY-yolo3

this sour code is from keras-yolo3
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LICENSE)

## Introduction

A Keras implementation of YOLOv3 (Tensorflow backend) inspired by [allanzelener/YAD2K](https://github.com/allanzelener/YAD2K).


---

## Training step

1. Pre-training weights:
yolov3.weights 
Download : https://pjreddie.com/media/files/yolov3.weights

2. Data set:
yolov3 training data: VOCdevkit


3. Modify yolo.cfg:
Modify classes to 1 (3 places)
Filters=255 is modified to filters=18 (3 places), the value formula is (classes+5)*3
Modify voc_annotation.py:
Modify classes to classes = ["person"]

4. Modify coco_class.txt and voc_class.txt in the model_data folder
Leave only the person

5. Generate training, verification, and test files
Run python voc_annotation.py
See that three files are generated: 2007_train.txt, 2007_test.txt, 2007_val.txt
Rename the three files separately and remove the prefix 2007_

6. Convert pre-training weights to .h5
python convert.py -w yolov3.cfg yolov3.weights model_data/yolo_weights.h5

7. Training
python train.py
The situation of val_loss: nan will appear during the training process, the solution:
Increase epoch (modify train.py), start to decrease after 50 generations
Increase batch size (modify yolov3.cfg)
After the training is completed, the weight.h5 file is placed in logs/000

8. Change weight
Move logs/000/trained_weights_stage_1.h5 to model_data
Modify the default weight path "model_path" in yolo.py to trained_weights_stage_1.h5

## Training step
Test
Feel free to find an mp4 with people to put in to test
python yolo_video.py --input 1.mp4
Save the results locally
python yolo_video.py --input test.mp4 --output test1.mp4
