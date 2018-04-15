# Ampel-Pilot-Dataset
Pedestrian traffic light image dataset (Germany)

![Preview](https://github.com/patVlnta/Ampel-Pilot-Dataset/blob/master/preview/dataset_preview.jpg "Dataset Preview")

The dataset has been collected in a joint effort between the Hochschule Augsburg and the University of Tuebingen. Students were able to contribute
by sending their pictures of pedestrian traffic lights with the LightsCatcher application.

The dataset has been used to train an object detection algorithm which is used in the Ampel-Pilot mobile application for visually impaired mobile users. It can be used as guidance for determining the current phase of a pedestrian traffic light.

* [Ampel-Pilot (iOS)](https://github.com/patVlnta/Ampel-Pilot)
* [LightsCatcher (Android)](https://play.google.com/store/apps/details?id=com.hs_augsburg_example.lightscatcher&hl=en)
* [LightsCatcher (iOS)](https://itunes.apple.com/de/app/lightscatcher/id1227218052?mt=8)

### Stats

* 3696 Images
* 4311 Annotations (63% Red, 37% Green)


## Download

The dataset is split into 4 different parts:

* [Part 1 (664mb)](https://s3.eu-central-1.amazonaws.com/ampelpilot.data/downloads/ampelpilot_dataset.zip)
* [Part 2 (1gb)](https://s3.eu-central-1.amazonaws.com/ampelpilot.data/downloads/ampelpilot_dataset.z01)
* [Part 3 (1gb)](https://s3.eu-central-1.amazonaws.com/ampelpilot.data/downloads/ampelpilot_dataset.z02)
* [Part 4 (1gb)](https://s3.eu-central-1.amazonaws.com/ampelpilot.data/downloads/ampelpilot_dataset.z03)

## Database

A MySql database was used to store image information and image annotations. The dump file is provided in this repository.

### Images
Images are stored in the `images` database table. Metainformation like file name, file extension and image dimensions can be obtained from here.

### Annotations
Annotations are stored in the `objects` table. Information like related image, class label (Red, Green) and position of the bounding box within the image can be obtained from here.

**! IMPORTANT !**
* The bounding box dimensions are kept **relative** to the image dimensions.
* x,y is the **center** of the bounding box

### Installation (MySQL Workbench)

1. Connect to your (local) database server
2. Server -> Data Import
3. Select the checkbox `Import from Self-Contained File` and provide the path to the [SQL dump file](https://github.com/patVlnta/Ampel-Pilot-Dataset/blob/master/database/ampelpilot_data.sql)
4. Make sure that `Dump Structure and Data` option is selected on the bottom of the screen
5. Start Import

## Model

A YOLOv2 object detection model (tiny) was trained based on this dataset using `3062 Images` for training and `630 Images` for validation.

| Light Phase        | Recall           | Precision  | IoU  |
| ------------- |:-------------:| :-----:| :-----:|
| Red     | 0.796 | 0.739 | 0.602 |
| Green     | 0.734 | 0.688 | 0.601 |

The model including the config file can be found [here](https://github.com/patVlnta/Ampel-Pilot-Dataset/blob/master/model).

## Contributions

Contributions to the dataset are always very welcome. If you have any further questions, ideas or enquiries, feel free to get in contact either by opening an issue or email [valpaet@gmail.com](mailto:valpaet@gmail.com).

## Credits

* **pjreddie** and all contributors for [YOLO/darknet](https://github.com/pjreddie/darknet)
* Project team [@Hochschule Augsburg](https://www.hs-augsburg.de/Informatik/Ampel-Pilot.html)
* Dataset contribution [@University of Tuebingen](https://www.uni-tuebingen.de/en/university.html)

