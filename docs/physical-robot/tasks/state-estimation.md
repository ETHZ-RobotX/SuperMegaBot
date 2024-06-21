---
layout: default
title: State Estimation
parent: Robot Operation
grand_parent: Physical Robot
nav_order: 2
has_toc: false
---

# ❓ State Estimation
{: .no_toc}

* Table of contents
{:toc}

The steps are very similar to the [simulation task](../../simulation/tasks/state-estimation.md). Please refer to that for details. 

Here are the commands to run to available state estimation methods.

## Using Tracking Camera

```bash
# In the host PC
roslaunch smb_opc opc.launch
```

```bash
# In the SMB terminal 
roslaunch smb smb.launch
```

In RViz, change the fixed frame to `tracking_camera_odom`, then drive the robot with [RC transmitter](../../info/robot-hardware.md#-rc-transmitter) and see how the robot is moving in RViz respective to the odom frame. 


## Using LiDAR + IMU

```bash
# In the host PC
roslaunch smb_opc opc.launch
```

```bash
# In the SMB terminal - launch msf graph 
roslaunch smb_msf_graph smb_msf_graph.launch use_sim_time:=true
```

If successful, you can see `GMsf ...graph is initialized.` message in the SMB terminal.

In RViz, select `world_graph_msf` as the global frame. Then drive the robot with [RC transmitter](../../info/robot-hardware.md#-rc-transmitter) and see how the robot is moving in RViz respective to the world frame.