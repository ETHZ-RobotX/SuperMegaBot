---
layout: default
title: State Estimation Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 1
nav_exclude: false
---

# Preparations for State Estimation Tutorial
To prepare for the Tutorial on State Estimation, first set up and install the [SMB core software](../../core-software/installation_core.md).

The only required external packages needed for the state estimation tutorial are [gtsam_catkin](https://github.com/leggedrobotics/gtsam_catkin) and [graph_msf](https://bitbucket.org/nubertj/gmsf_robotics_summer_school/src/robotics_summer_school_2023/). 
Both of these packages are also included in the `smb.repos`-vcs file, and automatically cloned to `se/graph_msf` and `lib/gtsam_catkin`.

## Download files
In order to follow the tutorial you will need the rosbag files located in the following folder:
  - [Rosbag folder](https://drive.google.com/drive/folders/1wOOfgYPC7JieQTXkpSQL0dHi8cU4xAJL?usp=sharing)

Download the rosbag(s) into a folder of your choice. In the tutorial this location will be denoted as `<path_to_bagfile>`.

## Compile gtsam_catkin

To compile the required packages, simply run
```bash
catkin build gtsam_catkin
```
This will build gtsam in you workspace and could take up to 5 minutes depending on your CPU.

**NOTE:** It will only take that long the first time you build `gtsam_catkin` in this workspace. Even after cleaning your build with `catkin clean`, it will be much faster, as the compiled binaries are stored inside the `lib/gtsam_catkin` repository.

## Build smb_msf_graph
To build `smb_msf_graph` run
```bash
catkin build smb_msf_graph
```
This will compile all dependencies present in the workspace, including [open3d_slam](https://github.com/leggedrobotics/open3d_slam/tree/robotics_summer_school_2023).

## Check The Compiled Code
You can test the success of the compilation by running the following code (from the root directory of the workspace).

```bash
source devel/setup.bash
roslaunch smb_msf_graph smb_msf_graph.launch
```
If everything launches without any error messages, your C++ software is ready for the tutorial.

## Voluntarily (but recommended) System Installs
* terminator, because multiple terminals will be needed during the tutorial.
```bash
sudo apt install terminator
```
* jsk_rviz_plugins, for visualizing TF-paths in RVIZ.
```bash
sudo apt install ros-noetic-jsk-rviz-plugins
```

