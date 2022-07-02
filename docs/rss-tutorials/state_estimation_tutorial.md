---
layout: default
title: State Estimation Tutorial
parent: Summer School Tutorials
nav_exclude: true
---

# State Estimation Tutorial
Before starting the tutorial, follow the [Preparation Instructions](state_estimation_tutorial_preparations.md) and compile the required code.

## 0 IMU in State Estimation
### 0.1 IMU State Space Model and MSF
Quick overview of the used framework. We will do this all together on the projector.

### 0.2 Quick Introduction to Noise Parameters
Uncertainty for pose and imu measurements. All together.

### 0.3 IMU Covariance Computation
Quick overview of how the required noise parameters can be computed in practice.
For details, refer to [kalibr](https://github.com/ethz-asl/kalibr/wiki/IMU-Noise-Model).

## 1.0 Running the MSF Framework
### 1.1 Preparations
As a first step, run the code on your computer and make sure that everything runs.
```bash
# In Terminal 1
$ roslaunch smb_msf smb_msf.launch use_sim_time:=true
```
Next, play the attached rosbag, and verify that only the point cloud localization (red arrows and path) is shown, hence, the state estimate (yellow arrows and path) is not yet published.
```bash
# In Terminal 2
$ rosbag play <path_to_bagfile>/2021_wangen_open3d_slam_odometry.bag --clock 
```

### 1.2 Run the framework
Now provide the correct paramters to the smb_msf.launch file.
MSF requires standard messages, i.e. `sensor_msgs/Imu` for the IMU topic, and `geometry_msgs/TransformStamped` for our given use-case. Relaunch the rosbag, until you see the odometry message displayed.

Note that the trajectory is fairly unsteady and misaligned with the IMU frame.

### 1.3 Extrinsics
While trying to find out what is wrong, you notice that the extrinsics calibration between the IMU and the LiDAR at the bottom of `smb_msf/param/smb_msf_params.yaml` are still set to the default values, and hence incorrect.

To correct for this, imagine you have access to an URDF model of the robot. However, it only provides the transformation $T_{LI}$.

$_{L}t_{LI}=(-0.024,-0.251,-0.255)^T$, $q_{LI}=(q_x,q_y,q_z,q_w)^T=(0,0,-0.707,0.707)^T$.

Convert it to $T_{IL}$ and correct the default parameters.

**Hint:** You can use the ros tf package with `rosrun tf static_transform_publisher x y z q_x q_y q_z q_w frame_1 frame_2 100` and `rosrun tf tf_echo frame_1 frame_2`.

## 2.0 Performance Analysis
### 2.1 Visualization Script
Launch the modified configuration for `smb_msf` from above. Now, before playing the rosbag, also launch the plotting node and enter the name `1_default` or similar when being prompted.
We recommend starting an external roscore in a 4th window, such that all nodes can safely communicate with each other.
```bash
# In Terminal 1
roscore
# In Terminal 2
roslaunch smb_msf smb_msf.launch use_sim_time:=true ... # TOPIC PARAMETERS MISSING
# In Terminal 3
roslaunch smb_msf plotting.launch # enter "1_default" or similar after bing prompted
# In Terminal 4
rosbag play <path_to_bagfile>/2021_wangen_open3d_slam_odometry.bag --clock 
```
While msf is running, the plotting script should print out messages in the terminal *"Received state message."*. If not, please check that the topic `/msf_core/state_out` is indeed published.
(e.g. by `rostopic hz /msf_core/state_out`).

If everything is running, wait for a minute or so, and then kill `plotting.launch`. Investigate the generated plots in your home directory in `$HOME/rss_plots/` with respect to their performance and smoothness.

### 2.2 Biased IMU
In this subtask, we will investigate the performance of the IMU if a strong bias of **0.8 m/s^2** is present along the z-axis of the imu. In the current default configuration the bias estimation is disabled.
Run the following:
```bash
# Terminal 1
roslaunch smb_msf plotting.launch noisify_imu:=true # enter "2_imu_noisified" or similar
# Terminal 2
roslaunch smb_msf smb_msf.launch use_sim_time:=true imu_topic:=/versavis/imu_noisified pose_topic:=/mapping_node/scan2map_transform # Note the "noisified" in the name
# Terminal 3
rosbag play <path_to_bagfile>/2021_wangen_open3d_slam_odometry.bag --clock
```
Investigate the trajectory in RVIZ. Is the yellow IMU trajectory at the correct location? After the robot moved a bit, kill the plotting.launch and look at the plot `2_imu_noisified_position-z.png`. What do you notice with respect to smoothness?

Next, disable the `core/core_fixed_bias` flag (set it to false) in `smb_msf/param/smb_msf_params.yaml`, and repeat the experiment (call it "3_bias_estimation" or similar). What changes? In particular also look at `3_bias_estimation-bias-z.png`.

### 2.3 (Optional) Noisy Pose Estimates
In this (optional) task, we simulate a noisy pose estimate (gaussian noise with std-dev of 0.1 for x,y,z), which can occur in challenging environments. For this task, run:
```bash
# Terminal 1
roslaunch smb_msf plotting.launch noisify_imu:=true # enter "4_position_noisified" or similar
# Terminal 2
roslaunch smb_msf smb_msf.launch use_sim_time:=true imu_topic:=/versavis/imu pose_topic:=/mapping_node/scan2map_transform_noisified # Note the "noisified" in the name
# Terminal 3
rosbag play <path_to_bagfile>/2021_wangen_open3d_slam_odometry.bag --clock
```
Have a look at the trajectory in rviz. (Note that the red trajectory is the original one BEFORE applying any noise.) What do you find with respect to the yellow curve?

Now spend some time to tune the parameter `pose_sensor/pose_noise_meas_p` in `smb_msf/param/smb_msf_params.yaml` and re-run the evaluation. In which range do you find the best noise value?

## 3.0 Outlook and Wrap-Up
Outlook to the SLAM tutorial and Wrapping-up.
