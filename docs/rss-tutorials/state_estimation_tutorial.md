---
layout: default
title: State Estimation Tutorial
parent: Summer School Tutorials
nav_exclude: true
---

# State Estimation Tutorial
Before starting the tutorial, follow the [Preparation Instructions](./rss-tutorials/state_estimation_tutorial_preparations.md) and compile the needed code.

## 0.0 Uncertainty in State Estimation
### 0.1 Quick Introduction to IMU

### 0.2 IMU Covariance Computation
Follow the instructions on the slide and compuute the noise and bias covariances.

## 1.0 First Run
### 1.1 Launching the Code
As a first step, run the code on your computer and make sure, that everything runs without dying:
```bash
# In Terminal 1
$ roslaunch smb_msf smb_msf.launch use_sim_time:=true
```
And make sure that nothing dies. Next, play the attached rosbag, and see what is happening.
```bash
# In Terminal 2
$ rosbag play <path_to_bag>/2021_wangen_compslam_odometry.bag --clock 
```

### 1.2 Investigation
Investigate the given rosbag, identify the 6DoF pose messages, and adapt the launch file `smb_msf.launch` in the `smb_msf` package accordingly.

Relaunch the rosbag, until you see the odometry message displayed.

## 2.0 Parameter Tuning and Visualization
### 2.1 Visualization Script
Launch the code from above. Now, before playing the rosbag, also launch the plotting node.
```bash
roslaunch smb_msf plotting.launch
```
What do you encounter? What could be the problem?
Discuss with your fellow students.

### Tuning
Have a look at the file in `smb_msf/param/smb_msf_params.yaml` and play around with the values.
What do you encounter?

## 3.0 Outlook
Outlook to SLAM tutorial.