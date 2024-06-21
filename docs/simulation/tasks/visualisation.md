---
layout: default
title: Visualisation and Teleop
parent: Simulation
nav_order: 1
has_toc: false
---

# 🔍 Visualisation and Teleop

* Table of contents
{:toc}

The goal of this section is to run the robot simulation using Gazebo, visualise the SMB robot in RViz, control the robot.

First of all, make sure the `smb_gazebo` has been already built successfully.

```bash
# In the host pc, build the smb_gazebo package if you haven't already
catkin build smb_gazebo
```

## 👀 Visualisation

Run the following commands in the host pc to visualise the robot.

```bash
# In the host pc
roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true world:=WaA
```

The simulation in `WaA.world` (stands for Test venue in Wangen an der Aare) runs on the host PC (your computer). To run the simulation you do not need a connection to SMB.

For more information about different simulation worlds, you could find details and test different worlds from [smb_common/smb_gazebo/worlds/](https://github.com/ETHZ-RobotX/smb_common/tree/master/smb_gazebo/worlds).
{: .note }

## 🎮 Teleoperation

Now you have two possibilities to drive with the robot.

1. You can drive the robot with the keyboard. If you want to drive the robot, make sure that the terminal where you launched the simulation (i.e. where the [`teleop_twist_keyboard`](http://wiki.ros.org/teleop_twist_keyboard) node is running) is selected while pressing the keys. To use the keyboard execute the following command:

    ```bash
    # In the host pc
    roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true keyboard_teleop:=true
    ```

    - Use the following keys to move:

        | u | i | o |
        | j | k | l |
        | m | , | . |

    - Use the following keys to control speed:

        - `q/z`: Increase/decrease max speeds by 10%
        - `w/x`: Increase/decrease only linear speed by 10%
        - `e/c`: Increase/decrease only angular speed by 10%

    - Use any other key to stop.

    Please refer to the [package documentation](http://wiki.ros.org/teleop_twist_keyboard#Controls) for more info.

2. If you have a joystick connect it to the laptop. You can see the button configuration [here](../../info/robot-hardware.md#-joystick).

    ```bash
    # In the host pc
    roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true
    ```

    The joystick mode might not work properly if you are using the **RSS Workspace** or **SMB Docker** image on Windows and MacOS environments.
    {: .smb-warning}
