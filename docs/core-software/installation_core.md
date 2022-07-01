---
layout: default
title: Core Software Setup
parent: SMB Core Software
nav_order: 1
---

# Setting up the SMB Core Software
{:.no_toc}

Documentation of the SuperMegaBot (SMB) for the ETHZ Robotic Summer School.

Please [create an issue](https://github.com/ETHZ-RobotX/SuperMegaBot/issues/new) for any missing library, package, driver, error or any kind of unclear instruction.
{: .smb-mention }


* Table of contents
{:toc}

## Remark

{:.no_toc}

The SMB software consists of two parts: core and hardware related.

If you want to use the system on a real SMB robot with real sensors and actuators, the [hardware related part](../robot-operation/installation_hw_packages.md) should be installed **on top of the core part**. This document contains the instructions about SMB core software, which also contains the simulation environment.


## Prerequisites

Note that, the system has been developed in Ubuntu 20.04 and test with [ROS Noetic](http://wiki.ros.org/noetic).
{: .smb-info }

* To check if the system has the correct ROS distribution please use the following terminal command.

    ```bash
    echo $ROS_DISTRO
    # output: noetic
    ```

* If you do not see the correct output, please refer to the [official ROS website](http://wiki.ros.org/noetic/Installation/Ubuntu) to install **ROS Noetic Desktop**.

    After installation, please ensure that environment variables like ROS_ROOT and ROS_PACKAGE_PATH are set. Please verify the installation by running the following terminal command.

    ```bash
    printenv | grep ROS
    ```

## Software Installation

### Installing command-line tools

> this part contains scripts to download tools for catkin, deps, and repository management

<!-- If there is an error of "*catkin: command not found*" -->

```shell
# tool for repo management
sudo apt install python3-vcstool
# tool for catkin packages
sudo apt install python3-catkin-tools python3-catkin-lint python3-pip
# tool for install deps
sudo apt install python3-rosdep
# misc libs/tools
python -m pip install osrf-pycommon
```

### Creating catkin workspace

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

* example

    ```bash
    # Example directory to ws and catkin workspace name
    mkdir -p ~/smb_ws/src
    cd ~/smb_ws/
    catkin init
    catkin config --extend /opt/ros/noetic
    catkin config -DCMAKE_BUILD_TYPE=Release
    ```

### Downloading the SMB packages with vcstool

To download the SMB packages, the vcs command-line tools will be used. For more information about the tool you can check the [link](http://wiki.ros.org/vcstool).
{: .smb-mention }

To download the SMB packages by using vcs tool run the following terminal commands in order.

```bash
# Navigate to the directory of src in your <catkin_ws_name>
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import \
--recursive \
--input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .
```

### Installing dependencies with rosdep

To install the dependencies, rosdep package will be used.For more information about the package you can check the [link](https://docs.ros.org/en/independent/api/rosdep/html/)
{: .smb-mention }

* (optional) If you did not do in the ROS installation step, please install ***rosdep*** package run the following terminal commands in order.

    ```bash
    sudo apt-get install python3-rosdep
    sudo rosdep init
    rosdep update
    ```

* To download the SMB dependencies by using rosdep package run the following terminal commands in order.

    ```bash
    # Navigate to the directory of src in your <catkin_ws_name>
    cd <directory_to_ws>/<catkin_ws_name>/src

    # Magic of rosdep
    rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
    ```

    Installing all the dependency may take a while.

* Note that, rosdep might not be able to install all dependencies. Please check the message at the terminal.

    Example : ros-noetic-gazebo-plugins

    ```bash
    # Install example missing package even after resdep
    sudo apt install ros-noetic-gazebo-plugins
    ```

    {: .smb-info }

### (Optional) Installing conda environment

if you are using or want to use *conda* for managing python packages in virtual environments, there's a few missing dependencies you can install in this *optional* step:

```bash
# Create a conda environment for the robotics summer school (feel free to choose a different name than rss)
conda create --name rss

#Activate the conda environment
conda activate rss

# (Optional) activate this environment by default on a new terminal
echo 'conda activate rss' >> ~/.bashrc

# Install python dependencies
conda install -c conda-forge empy defusedxml rospkg numpy -y
```
{: .smb-info }


### Finalization
After all required SMB packages and dependencies are cloned and installed, you can build the project:
```bash
# Navigate to the directory of workspace
cd <directory_to_ws>/<catkin_ws_name>/

# Build it
catkin build smb_gazebo

# Source it
source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash
```

You should see that every package is succesfully built.
After you built the packages, you can add the source file into **~/.bashrc** so that you do not have to source it everytime you log in a new terminal.

```bash
# Do not forget to change <...> parts
echo "source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash" >> ~/.bashrc
```

## Aliases for quick connection with SMB

## Running the simulation

Refer to the [How To Run Software Documentation](HowToRunSoftware.md) to learn on how to run the simulation.


## Hardware related software

To get everything running on the real robot, you also need to follow the steps described in the [documentation of the hardware related ROS packages](../robot-operation/installation_hw_packages.md).
