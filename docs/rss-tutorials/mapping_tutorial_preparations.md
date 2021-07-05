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
 - [Fist mission rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/first_mission_wangen.bag)
 - [Second mission rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/second_mission_wangen.bag)
 - [Challende site rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/challenge_site.bag)

Download this rosbags in to the folder ```~/catkin_ws/src/smb_common/smb_slam/data```

## Download maps
Maps for the localization
 - [Complete map Wangen](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/wangen_map_decimated.pcd)
 - [Challenge site map](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/challenge_decimated.pcd)

Download this rosbags in to the folder ```~/catkin_ws/src/smb_common/smb_slam/maps```

## The tutorial
Tutorial slides are [here](https://docs.google.com/presentation/d/11D1X3MY6VR8wBW-JjmiB09uwNbryShT9Ahid3iY3HFk/edit#slide=id.ge38e786417_1_5)
