---
layout: default
title: OPC
parent: Robot Operation
grand_parent: Physical Robot
nav_order: 1
has_toc: false
---

# 🖥️ OPC (Operator PC)
{:.no_toc}

## Launch Core Software

This section details how to run the core software on the physical robot and how to visualize it on the Operator PC, which is your host computer.

To launch the core software on the robot, run the following command in the terminal of the SMB:

```bash
# In the terminal of the SMB
roslaunch smb smb.launch

# If you see the message "First IMU Received",
# everything started without any problem
```


You can test the sensors by displaying the published topics.

```bash
# In a terminal of host PC

# Display the list of available topics
rostopic list

# Example: Display the measured wheelspeeds
rostopic echo /wheelSpeeds
```


To visualize the sensor readings via Rviz:

```bash
# In the terminal of host PC
roslaunch smb_opc opc.launch

# You should see the robot model in Rviz
```


You might need to restart the _SMB base_ if the robot does not respond to software commands.
{: .note }

Once the core software (`smb.launch`) is started on the robot, you have several options:

1. Control the robot using the RC transmitter. The signals from the RC transmitter are read by the onboard computer and sent to the motor controller.
2. Use a Joystick to generate control signals (twist messages). In order to control the SMB with the joystick, you should keep pressing the L1 button while driving and use the left stick to control the robot.
3. Run the autonomous software stack as outlined in the following section.
