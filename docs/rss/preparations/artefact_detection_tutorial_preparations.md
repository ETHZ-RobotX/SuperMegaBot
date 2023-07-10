---
layout: default
title: Artefact Detection Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 5
nav_exclude: false
---

# Preparations for Object Detection Tutorial

## Preparing software
Build object detection; the repository should be cloned by default.

The following instructions are for running the object detection on your machine:

- Navigate to the repository: `cd <ws_path>/src/object_detection`
- Install python dependencies: `pip install -r requirements.txt`
  - If you are using a conda environment, install the dependencies inside your environment.
    Follow the instructions for installing conda at: [Conda User Guide](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
- Build object_detection: `catkin build object_detection`
- Download the YOLO model weights from [here](https://github.com/ultralytics/yolov5/releases/download/v6.1/yolov5l6.pt).
  - After downloading the weights, place them in the `/usr/share/yolo/models` folder
 
**Note:** On the robot dependencies are already installed and the weights are placed on the Jetson GPU in the desired folder '/usr/share/yolo/models'.

## Computer vision algorithms jupyter notebook
This notebook will be used during tutorial. Please download it beforehand if possible.

- [Vision Notebook](https://polybox.ethz.ch/index.php/s/NIWeZP1pn6DiI31)

In order to use the notebook, you may use two approaches:

- local installation within conda
- docker

**Local installation with conda:**

- You may find the **env_vision_notebook.yml** file under the link above. Navigate to the folder where you downloaded the file.
Run `conda env create -f environment.yml`
- Activate your conda environment `conda activate rss_vision_notebook`
- Navigate to the base folder where you copied our vision_notebook folder and run `jupyter notebook`
- The previous command has opened your browser. Navigate to and open `ETH Robotics Summer School - Computer Vision Algorithms.ipynb`
- You are ready to follow the instructions and run the notebook.

**Docker:**

- Navigate to the vision_notebook folder
- You may find there the docker-compose.yaml, open it 
- Find the line **network_mode: host** for each service 
  - if you are using Ubuntu leave these lines **uncommneted**
  - if you are using Mac or Windows **comment these lines**
- Pull the docker image `docker compose pull notebook`
- Once the image is pulled, we may run the image with command `docker compose run notebook`
- Access the notebook in the browser by following of of the specified URLs. Navigate to and open `./notebook/ETH Robotics Summer School - Computer Vision Algorithms.ipynb`

Run `conda env create -f environment.yml`
- Activate your conda environment `conda activate rss_vision_notebook`
- Navigate to the base folder where you copied our vision_notebook folder and run `jupyter notebook`
- The previous command has opend your browser. Navigate to and open `ETH Robotics Summer School - Computer Vision Algorithms.ipynb`
- You are ready to follow the instructions and run the notebook.
  
## Testing data
These rosbags and yaml files will be used during tutorial. Please download them beforehand if possible.

- [Test Rosbag 1](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-32-34_smb263.bag)
- [Test Yaml 1](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-32-34.yaml)
- [Test Rosbag 2](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-37-44_smb263.bag)
- [Test Yaml 2](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-37-44.yaml)
