---
layout: default
title: State Estimation
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 1
nav_exclude: false
---

# Preparations for State Estimation Tutorial
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .important }
> To prepare for the Tutorial on State Estimation, make sure [SMB simulation environment](../../simulation/setting-up/index.md) is set up and running.

## Download files
In order to follow the tutorial you will need the rosbag files located in the following folder:
  - [Rosbag folder](https://drive.google.com/drive/folders/1wOOfgYPC7JieQTXkpSQL0dHi8cU4xAJL?usp=sharing)

Download the rosbag(s) into a folder of your choice. In the tutorial this location will be denoted as `<path_to_bagfile>`.

---

## Compile gtsam_catkin

To compile the required packages, simply run
```bash
catkin build gtsam_catkin
```
This will build gtsam in you workspace and could take up to 5 minutes depending on your CPU.

{: .note}
The very first build of `gtsam_catkin` usually takes longer than subsequent build. Even after cleaning the build result with `catkin clean`, it will still be much faster, as the compiled binaries are preserved in the `lib/gtsam_catkin` folder in the source space.

---

## Build smb_msf_graph
To build `smb_msf_graph` run
```bash
catkin build smb_msf_graph
```
This will compile all dependencies present in the workspace, including [open3d_slam](#).

---

## Check the compiled code
You can test the success of the compilation by running the following code (from the root directory of the workspace).

```bash
source devel/setup.bash    # or `wssetup` if you are using rss_workspace
roslaunch smb_msf_graph smb_msf_graph.launch
```
If everything launches without any error messages, your C++ software is ready for the tutorial.

---

## (Optional, but recommended) System Installs
* terminator, because multiple terminals will be needed during the tutorial.

```bash
sudo apt-get install terminator
```

{: .note}
If you are using [rss_workspace](../../simulation/setting-up/rss-workspace.md), js_rviz_plugins is already installed.

* jsk_rviz_plugins, for visualizing TF-paths in RVIZ.


```bash
sudo apt-get install ros-noetic-jsk-rviz-plugins
```

