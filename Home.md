# Description
Deep Learning Detection Suite (dl-DetectionSuite) consists of a set of utilities oriented to simplify developing, training and testing solutions based on object detection.

# Utilities
## Sample Generator
## Dataset Generator
## Detection Evaluation
## Deployer
Deployer Tab can be used to run inferences on images using various frameworks (TensorFlow and Darknet are currently supported). Below are instructions for both the frameworks:

### Darknet
As an example you can use Pascal VOC dataset on darknet format using the following instructions to convert to the desired format:
```bash
wget https://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
wget https://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
wget https://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar xf VOCtrainval_11-May-2012.tar
tar xf VOCtrainval_06-Nov-2007.tar
tar xf VOCtest_06-Nov-2007.tar

wget https://pjreddie.com/media/files/voc_label.py
python voc_label.py
cat 2007_train.txt 2007_val.txt 2012_*.txt > train.txt
```

In order to use darknet to detect objects over the images you have to download the network configuration and the network weights [5] and [6]. Then set the corresponding paths into DeepLearningSuite/appConfig.txt. You have also to create a file with the corresponding name for each class detection for darknet, you can download the file directly from [7]

Once you have your custom appConfig.txt( see #creating-a-custom-appconfigtxt) you can run the DatasetEvaluationApp.


[1] https://pjreddie.com/media/files/yolo-voc.weights <br>
[2] https://github.com/pjreddie/darknet/blob/master/cfg/yolo-voc.cfg <br>
[3] https://github.com/pjreddie/darknet/blob/master/data/voc.names <br>

### TensorFlow
For using TensorFlow as you framework, you would need a TensorFlow Trained Network. Some sample Networks/models are available at [TensorFlow model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).

Download one of them and untar it and place it into the weights directory.

We will be using a COCO trained model for this example, but you can choose any model. Although you would have to create a class names file for that particular dataset written in a correct order.

Sample coco.names file for COCO dataset: [coco.names](coco.names).<br>
All it containes is a list of classes being used for this dataset in the correct order.
Place this file in the names directory.

Now create an empty foo.cfg file and place it in the cfg directory. It is empty because tensorflow doesn't require any cfg file, just the frozen inference graph.

All done! Now you are ready to go!

Sample video using TensorFlow Framework in DetectionSuite<br>
[Link to Video<br>![Detection Suite tensorflow inferencer](https://img.youtube.com/vi/HmruYxzy3P4/0.jpg)](https://www.youtube.com/watch?v=HmruYxzy3P4)

### Creating a Custom ```appConfig.txt```
It is recommended to create and assign a dedicated directory for storing all datasets, weights and config files, for easier access and a cleaner ```appConfig.txt``` file.

For Instance we will be using ```/opt/datasets/``` for demonstration purposes.

Create some directories in ```/opt/datasets/``` such as ```cfg```, ```names```, ```weights``` and ```eval```.

Again, these names are temporary and can be changed, but must also be changed in appConfig.txt.

```cfg```: This directory will store config files for various networks. For example, yolo-voc.cfg [2].
```names```: This directory will contain class names for various datasets. For example, voc.names [3].
```weights```: This directory will contain weights for various networks, such as yolo-voc.weights [1] for yolo or a frozen inference graph for tensorflow trained networks.
```eval```: Evaluations path

Once done, you can create you own custom appConfig.txt like the one mentioned below.

```
--datasetPath
/opt/datasets/

--evaluationsPath
/opt/datasets/eval

--weightsPath
/opt/datasets/weights

--netCfgPath
/opt/datasets/cfg

--namesPath
/opt/datasets/names

--inferencesPath
/opt/datasets

```

Place your weights in weights directory, config files in cfg directory, classname files in names. And you are ready to go.

# Requirements

# Installation process
