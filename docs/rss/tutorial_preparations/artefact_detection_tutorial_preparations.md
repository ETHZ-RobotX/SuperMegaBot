---
layout: default
title: Artefact Detection
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 5
nav_exclude: false
---

# Preparations for Object Detection Tutorial
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .important }
To prepare for the object detection tutorial, please make sure the [SMB software stack](../../installation/index.md) is installed and is running correctly.

## Prerequisites
If you are using [rss workspace](../../installation/rss-workspace.md) or [smb docker](../../installation/smb-docker.md), all the necessary dependencies are already installed. If you installed the SMB software stack locally on your machine, please follow the instructions below to install the necessary dependencies.

### Using rss workspace or smb docker (Recommended)
For most users, using the Docker container is the simplest option. The Docker container includes the model and dependencies pre-installed, and the weights are in the correct position. 

- The Docker version does not use PyTorch but runs the model with ONNX to keep the size of the Docker image smaller.

### Installing Dependencies locally (Only for [Local Installation](../../installation/local-installation.md))
To install the object detection package locally, follow these steps:

- Navigate to the repository: `cd <ws_path>/src/object_detection`
- Install Python dependencies: `pip install -r requirements.txt`
  - If you are using a conda environment, install the dependencies inside your environment.
    Follow the instructions for installing conda at: [Conda User Guide](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
- Build object_detection: catkin build object_detection
- Download the YOLO model weights from [here](https://github.com/ultralytics/yolov5/releases/download/v6.1/yolov5l6.pt).
  - After downloading the weights, place them in the `/usr/share/yolo/models` folder

**Note:** On the robot, dependencies are already installed, and the weights are placed on the Jetson GPU in the desired folder '/usr/share/yolo/models'.

---

## Computer vision algorithms jupyter notebook
This notebook will be used during the tutorial. Please download it before coming to the summer school as internet access is limited.

- [Vision Notebook](https://polybox.ethz.ch/index.php/s/lmVgBTqDYVTiVUI)
  
---

## Testing data
These rosbags and yaml files will be used during the tutorial. Please download them beforehand if possible.

- [Test Rosbag 1](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-32-34_smb263.bag)
- [Test Yaml 1](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-32-34.yaml)
- [Test Rosbag 2](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-37-44_smb263.bag)
- [Test Yaml 2](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-16-37-44.yaml)

---

## Running the ROS Bag File in Docker (Only for rss_workspace and smb_docker)

### Copying the ROS Bag File into the Docker Container

If you have downloaded the ROS bag files to your local machine and are using Mac or Windows, you can copy them into the Docker container using the docker cp command. Ensure the Docker container is running before performing these steps:

1. Find the name of the Docker container by running the following command (make sure your Docker container is running)

   ```bash
   docker ps
   ```

   The output will look like this if you are using the rss_workspace:
   ```
   CONTAINER ID   IMAGE                            COMMAND       CREATED         STATUS         NAMES
   1234567890ab   vsc-rss_workspace-123asd-uid     "/bin/bash"   5 minutes ago   Up 5 minutes   sad_hawking
   ```
   
   or like this if you are using the smb_docker:
   ```
   CONTAINER ID   IMAGE             COMMAND       CREATED         STATUS         NAMES
   1234567890ab   smb_docker        "/bin/bash"   5 minutes ago   Up 5 minutes   sad_hawking
   ```

   In this example, the name of the Docker container is `sad_hawking`.

2. Copy the ROS bag file into the Docker container, replacing `<NAME-OF-CONTAINER>` with the actual name of the Docker container and `/path/to/your/rosbag.bag` with the path to the ROS bag file on your local machine:

   ```bash
   docker cp /path/to/your/rosbag.bag <NAME-OF-CONTAINER>:/workspaces/rss_workspace/src/rosbags/
   ```

   {: .note}
   If you are using vscode, you can try to drag and drop the rosbag into the vscode file explorer to copy it into the container. But be aware that this might take longer than `docker cp`. For example, it might take a few minutes to copy a 1GB file.

3. Navigate to the directory containing the ROS bag file inside the container:

   ```bash
   cd /workspaces/rss_workspace/src/rosbags
   ```

4. Play the ROS bag file:

   ```bash
   rosbag play <rosbag_name>.bag
   ```

   {: .note }
   > If the bag file does not run and you see an error like:
   >
   > ```
   > [ERROR] [1718830710.056746147]: [registerPublisher] Failed to contact master at [localhost:11311]. Retrying...
   > ```
   > You might need to start the ROS master with the following command:
   > ```
   > roscore
   > ```

---

### YOLOv5 Supported Object Classes
For a comprehensive list of YOLOv5 supported object classes, please refer to the [YOLOv5 Object Classes](https://github.com/ultralytics/yolov5/blob/master/data/coco128.yaml).



