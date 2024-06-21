---
layout: default
title: State Estimation Tutorial
parent: Tutorials
grand_parent: Robotics Summer School
nav_order: 1
# nav_exclude: true
math: mathjax3
---

# State Estimation Tutorial
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Before starting the tutorial, follow the [Preparation Instructions](../preparations/state_estimation_tutorial_preparations.md) and compile the required code.

The first part of this tutorial - Section 0 - will be given as a presentation. The second part - `Sections 1-3` - will then be more interactive. 

## 0 - Introduction to Robotic State Estimation (Presentation)
As a first part of this tutorial, we will look at IMUs and its characteristics in more detail.

### 0.1 - IMU State Space Model
Starting off, we look at the equations and the most common model used for IMUs. **All together.**

### 0.2 - Quick Introduction to IMU Noise Parameters
In a second step, we will look at the IMU noise parameters, and how they can be computed. **All together.**

### 0.3 - Quick Introduction to GraphMSF
As a third part, a quick overview of the GraphMSF software framework is given. **All together.**

## 1.0 - Sensor Fusion (Interactive Session)
In this part, we will now investigate the sensor fusion performance using various inputs. The whole tutorial will be guided on the projector, with short breaks to run the code on the PCs.

### 1.1 - Pure IMU Integration
In a first step, pure IMU integration and its limitations are investigated.

For this, run the following launch file on your computer and make sure that everything runs without an issue.
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_1.launch
```
In this terminal, it will also ask you for an experiment name for logging of the data. Simply enter `"1.1"` (without ""). 
Next, play the first 30s of the [attached rosbag](https://drive.google.com/file/d/1x985YCBIAnq5tmPYuo4YW-cagiTV3ud4/view?usp=drive_link)].
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/outdoor_2023-06-16-11-39-50_smb263.bag --clock -u 30 
```
The corresponding plots are then saved on your computer in `~/rss_plots/`.

* What can you observe here?
    * In particular, pay attention to the lateral velocity after 30s. Does this makes sense?

### 1.2 - Adding Wheel Odometry
In a next step, we will add wheel odometry to the estimation. For this, go to the config file `smb_msf_graph/tutorial/config/1/smb_graph_params.yaml` 
* and enable the wheel odometry. 

Same as before, the scripts can be started by doing:
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_1.launch
```
Enter the name `"1.2"`. This time we play the entire bag, hence remove the `-u 30`:
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/outdoor_2023-06-16-11-39-50_smb263.bag --clock 
```
* What do you observe this time?
* How is the performance with respect to local and global drift?
* How does it compare to wheel odometry alone? This can be seen by the red arrow, and in the corresponding plot.

### 1.3 - Adding LiDAR Mapping
In a next step, we will add LiDAR mapping. Again, go to `smb_msf_graph/tutorial/config/1/smb_graph_params.yaml`. This time
* enable the LiDAR mapping, 
* and disable the wheel odometry again.

Then run
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_1.launch
```
Enter the name `"1.3"`.
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/outdoor_2023-06-16-11-39-50_smb263.bag --clock 
```
* How is the performance with respect to Wheel Odometry?
* How does the trajectory's smoothness relate to the LiDAR Mapping path (green trajectory)?

## 2.0 - Biased Accelerometer (Interactive Session)
In the second task, we will now look at the scenario of a biased accelerometer. The bias is in the form of a sine wave with period time of 20s, and an amplitude of 0.1m/s^2.

### 2.1 - Non-tuned Configuration
In the first step, we will run the non-tuned configuration.
For this, run the following and inspect the behavior:
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_2.launch
```
Enter the name `"2.1"`. Then play the first 30s of the bag:
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/outdoor_2023-06-16-11-39-50_smb263.bag --clock -u 30
```
Given the plots,
* What can you observe?
* How does the trajectory in z direction look like?

### 2.2 - Tuning the Bias Behavior
In a next step, go to `smb_msf_graph/tutorial/config/2/core_graph_params.yaml` and 
* tune the acceleration random walk. 

Think about whether it should be larger or smaller, and increase/decrease it by a factor of 10 and 100. Then run
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_2.launch
```
Enter the name `"2.2"`. Then play the first 30s of the bag:
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/outdoor_2023-06-16-11-39-50_smb263.bag --clock -u 30
```
* How does the trajecotry in the z direction look now?
* How does the bias estimate capture the true bias?

## 3.0 - Correct Handling of Coordinate Frames (OPTIONAL, Interactive Session)
In this task, we will investigate the importance of optimizing over T_M_W. For this, we provide [another dataset](https://drive.google.com/file/d/1K6pWN2gXvhLavim5858fO0xwuG4O-ECR/view?usp=sharing) where the map (M) and gravity-aligned world (W) frames are strongly misaligned.

### 3.1 - Without Optimizing T_M_W
Run the following script, which will not optimize over this frame displacement.
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_3.launch
```
Enter the name `"3.1"`. Then play the first 30s of the NEW bag:
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/indoor_tilted_2023-06-29-17-32-42_smb.bag --clock -u 30
```
* What can you observe here?
* How does the z position and z bias behave?

### 3.2 - With Optimizing T_M_W
In a last step, go to `smb_msf_graph/tutorial/config/3/core_graph_params.yaml` and 
* enable the frame optimization. 

Then run the same again:
```bash
# In Terminal 1
$ roslaunch smb_msf_graph tutorial_3.launch
```
Enter the name `"3.2"`. Then play the first 30s of this bag:
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/indoor_tilted_2023-06-29-17-32-42_smb.bag --clock -u 30
```
* Why do you think is the situation now becoming better, and the overall estimate smoother?