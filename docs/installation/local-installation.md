---
layout: default
title: Local Installation
parent: Installation
nav_order: 3
has_toc: false
---

# 🖥️ Local Installation
{:.no_toc}

Please [create an issue](https://github.com/ETHZ-RobotX/SuperMegaBot/issues/new) for any missing library, package, driver, error, or any kind of unclear instruction.
{: .important }

* Table of contents
{:toc}

## 💡 Remarks
{:.no_toc}

The SMB software is split into two parts: non-hardware and hardware related. 
If you want to use the system on a real SMB robot with real sensors and actuators, the [hardware-related part](../../physical-robot/setting-up/robot-workspace-setup.md) should be installed **on top of the non-hardware part**. This document contains the instructions for SMB non-hardware related software, which also includes the simulation environment.

## 📋 Prerequisites

Note that the system has been developed on Ubuntu 20.04 and tested with [ROS Noetic](http://wiki.ros.org/noetic). Also works if you have a virtual environment with Ubuntu 20.04.
{: .note }

* To check if the system has the correct ROS distribution, please use the following terminal command:

    ```bash
    echo $ROS_DISTRO
    # output: noetic
    ```

* If you do not see the correct output, please refer to the [official ROS website](http://wiki.ros.org/noetic/Installation/Ubuntu) to install **ROS Noetic Desktop**.

    After installation, please ensure that environment variables like ROS_ROOT and ROS_PACKAGE_PATH are set. Verify the installation by running the following terminal command:

    ```bash
    printenv | grep ROS
    ```

## 🔧 Software Installation

### Installing Command-Line Tools

> This section contains scripts to download tools for catkin, dependencies, and repository management.

```bash
# Tool for repo management
sudo apt install python3-vcstool
# Tool for catkin packages
sudo apt install python3-catkin-tools python3-catkin-lint python3-pip
# Tool for installing dependencies
sudo apt install python3-rosdep
# Miscellaneous libraries/tools
python3 -m pip install osrf-pycommon
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
{: .note }

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
{: .note }

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
    {: .note }

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
{: .note }

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

## ▶️ Running the simulation

Refer to the [link](../tasks/visualisation.md) to learn on how to run the simulation.

## ⚡️ (Optional) Setting aliases for quick connection with SMB 

When connecting to a remote computer using ssh, you can simplify the process by the following hints.

### Setup `~/.ssh/config`

If it doesn't exist yet, create the file `~/.ssh/config` and add the following lines using team5 and SMB263 as an example (remember to adjust to your team and distributed SMB).

```
# mostly used for executing commands on SMB
Host smb-263
  Hostname 10.0.3.5
  User team5

# may be used for object detection task on SMB
Host smb-263-gpu
  Hostname 10.0.3.7
  User team5
```

You may now connect as user team5 to smb-263 on `10.0.3.5` by just executing `ssh smb-263`.

### SSH Public Key Authentication

This section assumes, that you haven't set up multiple key files yet.
{: .note }

Instead of typing the password everytime you connect to the robot, you may also copy your public ssh key to the robot.

In a nutshell, follow the steps below:

```bash
test ! -e ~/.ssh/id_rsa.pub && ssh-keygen  # generate ssh keys if they don't exist yet
ssh-copy-id team2@10.0.1.5   # adjust username and robot IP address!
```

Combined with setting up the robot in `~/.ssh/config` this allows connecting to the robot without the need to type the password.

More details can be found in the [official documentation of ssh-copy-id](https://www.ssh.com/academy/ssh/copy-id).
{: .note }

### Setting ROS_MASTER_URI and ROS_IP

Setting the environment variables `ROS_MASTER_URI` and `ROS_IP` properly is the best strategy to avoid any communication issues in the ROS network.

A convinient way to set the variables is to **adjust the following code to match your robot** and add it to the file `~/.bash_aliases` (or `~/.bashrc`):

```bash
alias connect-smb="export ROS_MASTER_URI=http://\$(ip route show default | grep -oP 'via \K\d+\.\d+\.\d+').5:11311 ; export ROS_IP=\$(ip route get 8.8.8.8 | grep -oP '(?<=src )\S+') ; echo 'ROS_MASTER_URI and ROS_IP set to ' ; printenv ROS_MASTER_URI ; printenv ROS_IP"
```

Then (for any newly openend terminal), you can execute `connect-smb` to set the correct environment variables for your robot.


## 🔂 Updating the SMB Core Software

The repositories containing the SMB Core software will most likely be updated. It is recommended to update the software from time to time.
{: .note}

### Downloading updates
To download the most recent software, execute the following commands.
```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Add the new repositories
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .

# Pull the latest changes
vcs pull

# Update dependencies with rosdep
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
```

### Build updated packages
While pulling the repositories you might see this message
```bash
Updating <old_commit>..<new_commit>
```

If this is the case you need to build the packages in the respective repository again.

### Troubleshooting

#### Path already exists
If you import the repositories you might encounter this error:

```bash
Path already exists and contains a different repository
```

This means that the repository on your host is outdated and the URL of the new one is changed. In this case just delete the folder and execute again the import command.

```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Delete outdated repository
rm -rf <outdated_repository>

# Add the new repositories
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb.repos .

# Pull the latest changes
vcs pull
```

#### Build failed
Sometimes the name of the repository could change, and if you try to build again than you will receive the following error:

```bash
CMake Error: The source directory "/path/to/directory" does not exist.
```

In this case just clean the your builds and build again.
```bash
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/

# Clean
catkin clean <package_name>

# Build
catkin build <package_name>
```