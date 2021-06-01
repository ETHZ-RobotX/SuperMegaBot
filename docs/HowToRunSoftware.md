# How to Run SMB Software? 
> This documentation explains the basic steps about how to run SMB software . The documentation might lack of of some information since the updated SMB software is still work in progress!  

> Please inform oilter@ethz.ch for any missing or unclear instruction.

> ToDo Add test phases, Warnings

## Remark
This document does not explain the full capability of the robot. It gives basic information related to software and how to run it. For more information please check the packages. 

In the document there are two terminal types:
1) Terminal of host PC: The terminal that has access to host pc system.
2) Terminal of SSH: The terminal that has SSH connection to the SMB, therefore has access to the SMB system.

To use the software correctly please be sure that you followed the [HowToUseSMB Document](./HowToUseSMB.md) until the part **ShutDown Procedure**.

### Use Basic Functionality

You can run the software in two mode: 
1. Manuel Mode
2. Autonomous Mode

In both mode all sensor values, odometry and robot state can be reached and visualized. In autonomous mode, you can give goal position for the robot to navigate autonomously via Rviz Interface. 


#### Manuel Mode
>If you want to switch between modes make sure that you killed the other process. 


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


#### Autonomous Mode
>If you want to switch between modes make sure that you killed the other process. 

```bash
# In the terminal of SSH
roslaunch smb smb.launch run_twist_scaling_node:=true

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