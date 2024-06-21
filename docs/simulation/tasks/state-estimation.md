---
layout: default
title: State Estimation
parent: Simulation
nav_order: 2
has_toc: false
---

# ❓ State Estimation
{: .no_toc}

* Table of contents
{:toc}

The state of the SMB can be estimated in multiple ways: using the tracking camera, fusing LiDAR + IMU using Graph MSF. Then, launch the simulation environment in `planner_tutorial.world`:

## Using Tracking Camera

The SMB robot is equipped with an Intel Realsense T265 tracking camera, which can output the odometry using visual-inertial odometry. To open the simulation with the tracking camera, run the following command:

```bash
# In the host PC
roslaunch smb_gazebo sim.launch tracking_camera:=true launch_gazebo_gui:=true keyboard_teleop:=true
```

This will open up Gazebo and RViz. In RViz, change the fixed frame to `tracking_camera_odom`, then drive the robot with [keyboard controls](visualisation.md#teleoperation) and see how the robot is moving in RViz respective to the odom frame.

## Using LiDAR + IMU

The SMB robot is equipped with LiDAR and IMU. For state estimation, these data can be fused using the method Graph-MSF: Graph-based Multi-sensor Fusion for Consistent Localization and State Estimation. To learn more, [link](https://github.com/leggedrobotics/graph_msf/).

To build MSF Graph, 

```bash
catkin build -c smb_msf_graph
```

To run the MSF Graph,

```bash
# in one terminal - launch Gazebo and RViz
roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true keyboard_teleop:=true
```

```bash
# in second terminal - launch msf graph 
roslaunch smb_msf_graph smb_msf_graph.launch use_sim_time:=true
```

If successful, you can see `GMsf ...graph is initialized.` message in the second terminal.

In RViz, select `world_graph_msf` as the global frame. Then drive the robot with [keyboard controls](visualisation.md#teleoperation) and see how the robot is moving in RViz respective to the world frame.
