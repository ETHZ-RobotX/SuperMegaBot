---
layout: default
title: Navigation
parent: Robot Operation
grand_parent: Physical Robot
nav_order: 3
has_toc: false
---

# 🧭 Autonomous Navigation
{: .no_toc}

* Table of contents
{:toc}

The steps are very similar to the [simulation task](../../simulation/tasks/navigation.md). Please refer to that for details. 

## Running the core software on the robot

To launch the core software on the robot, run the following command.

```bash
# In the terminal of the SMB
roslaunch smb smb.launch

# If you see the message "First IMU Received",
# everything started without any problem
```

In another terminal, launch the localization and mapping:
```bash
# In the host PC
roslaunch smb_msf_graph smb_msf_graph.launch
```

## Local Planner
In the third terminal, launch the local path planner:
```bash
# In the host PC
roslaunch smb_navigation navigate2d_cmu.launch use_msf:=true global_frame:=world_graph_msf state_estimation_topic:=/transformed_odom launch_far_planner:=false
```

Now you can set the waypoint for the robot to navigate to using the Waypoint plugin in rviz just like in the simulation.
The robot should navigate to the waypoint while avoiding the obstacles autonomously.

## Point Goal Navigation with FAR Planner
Launch the local planner with FAR planner, simply set the launch_far_planner argument to true:
```bash
# In the host PC
roslaunch smb_navigation navigate2d_cmu.launch use_msf:=true global_frame:=world_graph_msf state_estimation_topic:=/transformed_odom 
```
Now you can set the goalpoint using the Goalpoint plugin in rviz like in the simulation.
You should see the robot navigating to the goal point while avoiding the obstacles autonomously.


## 📋 Other Methods

### 1️⃣ Running with Tracking Camera

```bash
# In the SMB terminal 
roslaunch smb_navigation navigate2d_ompl.launch global_frame:=tracking_camera_odom

# If you see the message "odom received",
# everything started without any problem
```


### 2️⃣ Running with Online SLAM + MSF Graph

Launch MSF Graph + Open3D SLAM:

```bash
# in the SMB terminal - launch the state estimator with online SLAM
roslaunch smb_msf_graph smb_msf_graph.launch
```

Launch OMPL planner:

```bash
# in the SMB second terminal - launch the autonomous navigation
roslaunch smb_navigation navigate2d_ompl.launch global_frame:=world_graph_msf odom_topic:=/graph_msf/est_odometry_odom_imu

# If you see the message "odom received",
# everything started without any problem
```

To save the map, use the following ROS service:

```bash
# in the SMB third terminal
rosservice call /mapping/save_map
```

The point cloud will be saved to `src/core/smb_slam/data/maps/map.pcd`.


### 3️⃣ Running with Localization SLAM + MSF Graph

If an existing global map is available, it can be used for planning.

In the next step, the state estimator needs to be launched:

```bash
# in the first SMB terminal - launch the state estimator with online SLAM
# this will automatically fetch the map saved in smb_slam/data/maps/map.pcd which can be configured in param_rs16_localization.lua
roslaunch smb_slam localization.launch
```

Before running anything else, you need to first localize the robot in the map. This can be done in Rviz using `2D Pose Estimate` from the top toolbar. The localization is successful if the data from the LiDAR and the points from the map align. Once this is done, you can run the state estimation and autonomous planning as follows:

```bash
# in the second SMB terminal - launch the state estimator
roslaunch smb_msf_graph smb_msf_graph.launch launch_o3d_slam:=false
```

```bash
# in the third SMB terminal - launch the autonomous navigation
roslaunch smb_navigation navigate2d_ompl.launch global_frame:=world_graph_msf odom_topic:=/graph_msf/est_odometry_odom_imu

# If you see the message "odom received",
# everything started without any problem
```

Once the autonomous navigation is running, you can use the Rviz `2D Navigation Goal` tool.
