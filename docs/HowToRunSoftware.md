---
layout: default
title: Running the Software
nav_order: 4
---

# How to Run SMB Software? 
> This documentation explains the basic steps about how to run SMB software . The documentation might lack of of some information since the updated SMB software is still work in progress!  

> Please inform oilter@ethz.ch for any missing or unclear instruction.

> ToDo Add test phases, Warnings

## Remark
This document does not explain the full capability of the robot. It gives basic information related to software and how to run it. For more information please check the packages. 

In the document there are two terminal types:
1) Terminal of host PC: The terminal that has access to host pc system.
2) Terminal of SSH: The terminal that has SSH connection to the SMB, therefore has access to the SMB system.

To use the software correctly please be sure that you followed the [HowToUseSMB Document](HowToUseSMB.md) until the part **ShutDown Procedure**.

### Use Basic Functionality

You can run the software in two mode: 
1. Simulation Mode 
2. Manuel SMB Mode
3. Autonomous SMB Mode

In both mode all sensor values, odometry and robot state can be reached and visualized. In autonomous mode, you can give goal position for the robot to navigate autonomously via Rviz Interface. 

### Simulation Mode
>If you want to switch between modes make sure that you killed the previous mode.

Simulation runs on the host pc. To run the simulation you do not need connection to SMB

```bash
# In the host pc
roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true

```

#### Autonomous Navigation Simulation 

More information about the path planner can be found in the [path planner reposiotry](https://github.com/VIS4ROB-lab/smb_path_planner)

Since we have successfully set up the SMB software, one can launch the simulation and get the first experience with the OMPL path planner.
Make sure that the `smb_navigation` is built. If not, run:
```bash
# In the host pc
catkin build smb_navigation
```
then, launch the simulation environment:
```bash
# In the host pc
roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true run_twist_scaling_node:=true
```
Subsequently, in the second terminal window launch the OMPL path planner:
```bash
# In the host pc
roslaunch smb_navigation navigate2d_ompl.launch sim:=true global_frame:=tracking_camera_odom robot_base_frame:=base_link
```
In the RVIZ you should observe a grey-scaled map with SMB in the middle. Now, select `2d Navigation Goal` from the top toolbar and set the goal for the planner in the feasible region within the map.



### Manuel Mode
>If you want to switch between modes make sure that you killed the previous mode. 


```bash
# In the terminal of SSH
roslaunch smb smb.launch

# If you see the message "First IMU Received", 
# everything started without any problem
```

You can test the sensor by reading the published topics.

The Expected topic list as the following.
!!!! Add Expected Topic List !!! 

To visualize the sensor reading via Rviz
```bash
# In the terminal of host PC
roslaunch smb_opc opc.launch

# You should see the robot model in Rviz
```

> You might need to restart the base if the robot does not respond to the teleop control

In order to control the SMB with the joystick, you should keep presing the L1 button while driving and use the left stick to control the robot.

!!!! THIS WILL CHANGE !!!!!! 



### Autonomous Mode
>If you want to switch between modes make sure that you killed the other process. 

```bash
# In the terminal of SSH
roslaunch smb smb.launch

# If you see the message "First IMU Received", 
# everything started without any problem
```

To start the autonomous navigation please run the following terminal command in an other terminal window.
```bash
# In the terminal of SSH
roslaunch smb_navigation navigate2d_ompl.launch global_frame:=tracking_camera_odom robot_base_frame:=base_link

# If you see the message "odom received", 
# everything started without any problem
```

To visualize the sensor reading via Rviz
```bash
# In the terminal of host PC
roslaunch smb_opc opc.launch

# You should see the robot model in Rviz
```

After that you can use the Rviz 2D Navigation Goal tool 
