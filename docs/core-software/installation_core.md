---
layout: default
title: Software Setup
parent: SMB Core Software
nav_order: 1
---

# Setting up the SMB Core Software
{:.no_toc} 

Please [create an issue](https://github.com/ETHZ-RobotX/SuperMegaBot/issues/new) for any missing library, package, driver, error or any kind of unclear instruction.
{: .smb-mention }

Documentation of the SuperMegaBot (SMB) for the ETHZ Robotic Summer School.


* Table of contents
{:toc}

## Remark

The SMB software consists of two parts: core and hardware related.

If you want to use the system on a real SMB robot with real sensors and actuators, the [hardware related part](../robot-operation/installation_hw_packages.md) should be installed **on top of the core part**. This document contains the instructions about SMB core software, which also contains the simulation environment.


## Prerequisites
- ROS Noetic

Note that, the system has been developed in Ubuntu 20.04.
{: .smb-info }

To see if the system has the correct ROS distribution please use the following terminal command. 

```bash
echo $ROS_DISTRO
# output: noetic
```
If you do not see the correct output, please refer to the [official ROS website](http://wiki.ros.org/noetic/Installation/Ubuntu) to install **ROS Noetic Desktop**. 

After installation, please ensure that environment variables like ROS_ROOT and ROS_PACKAGE_PATH are set. Please verify the installation by running the following terminal command.

```bash
printenv | grep ROS
```

## Software Installation

### Catkin Workspace and all Packages

Create a new catkin workspace.

```bash
# create the directories
# Do not forget to change <...> parts
mkdir -p <directory_to_ws>/<catkin_ws_name>/src
cd <directory_to_ws>/<catkin_ws_name>/

# initilize the catkin workspace
catkin init
catkin config --extend /opt/ros/noetic
catkin config -DCMAKE_BUILD_TYPE=Release
```


If there is an error of "catkin: command not found" 
```bash
sudo apt install python3-catkin-lint python3-pip
pip3 install osrf-pycommon
```


```bash
# Example directory to ws and catkin workspace name
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
# Example ends
```


To download the SMB packages, the vcs command-line tools will be used. For more information about the tool you can check the [link](http://wiki.ros.org/vcstool).
{: .smb-mention }

To install ***vcstool*** run the following terminal command.

```bash
sudo apt install python3-vcstool 
```
To download the SMB packages by using vcs tool run the following terminal commands in order. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .
```

### Installing Dependencies

To install the dependencies, rosdep package will be used.For more information about the package you can check the [link](https://docs.ros.org/en/independent/api/rosdep/html/)
{: .smb-mention }


To install ***rosdep*** package run the following terminal commands in order, unless you did not do in the ROS installation step.

```bash
sudo apt-get install python3-rosdep
sudo rosdep init
rosdep update
```

To download the SMB dependencies by using rosdep package run the following terminal commands in order. 
```bash
# Navigate to the directory of workspace
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Magic of rosdep
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
```

Installing all the dependency may take a while. 

Note that, rosdep might not be able to install all dependencies.
Example : ros-noetic-gazebo-plugins
```bash
# Install example missing package even after resdep
sudo apt install ros-noetic-gazebo-plugins
```
{: .smb-info }

### Finalization
Since every SMB package and dependency is installed, you can build the project.
```bash
# Navigate to the directory of workspace
cd <directory_to_ws>/<catkin_ws_name>/

# Build it
catkin build smb_gazebo

# Source it
source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash
```

You should see that every package is built.
After you built the packages, you can add the source file into .bashrc so that you do not have to source it everytime you log in a new terminal. 

```bash
# Do not forget to change <...> parts
echo "source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash" >> ~/.bashrc
```

## Running the simulation
Refer to the [How To Run Software Documentation](HowToRunSoftware.md) to learn on how to run the simulation.


## Hardware related software
To get everything running on the real robot, you also need to follow the steps described in the [documentation of the hardware related ROS packages](../robot-operation/installation_hw_packages.md).
