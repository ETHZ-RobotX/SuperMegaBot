---
layout: default
title: Mapping Tutorial
parent: Summer School Tutorials
nav_order: 3
---

# Preparations for Mapping Tutorial
For the tutorial you need the following packages:
 - cartographer_ros
 - cartographer_rviz

## Installation
Install build tools:
```bash
sudo apt-get update
sudo apt-get install -y python3-wstool python3-rosdep ninja-build stow
```
Download repository and install dependencies **(~ 5 minutes)**
```bash
cd catkin_ws
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
sudo rosdep init
rosdep update
cd src
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
cartographer/scripts/install_abseil.sh
```
Build the packages **(~ 10 minutes)**
```bash
catkin build cartographer_ros
catkin build cartographer_rviz
catkin build smb_slam
```

## Download rosbags
In order to follow the tutorial you will need the following rosbags:
  - [First mission rosbag](https://drive.google.com/file/d/114OGae0iBZkDrRcX-PqhLf18mXBWTfG4/view?usp=sharing)
  - [Second mission rosbag](https://drive.google.com/file/d/18zWR21lLWrrMPrmI8C0SQgeFUcclFMV8/view?usp=sharing)
  - [Challenge site rosbag](https://drive.google.com/file/d/1uO-xsfpAop41QRdv2RUGNn1P85fWY0L4/view?usp=sharing)

Download this rosbags in to the folder ```~/catkin_ws/src/smb_common/smb_slam/data```

## Download maps
Maps for the localization
 - [Complete map wangen](https://drive.google.com/file/d/1u_4aOgHkeTTHCsqtAqP-cz3Jaqd6LFqo/view?usp=sharing)
 - [Challenge site](https://drive.google.com/file/d/10nhsMKLtLBDk-LJa7HmNCf9P40ncXv2c/view?usp=sharing)

Download this rosbags in to the folder ```~/catkin_ws/src/smb_common/smb_slam/maps```
