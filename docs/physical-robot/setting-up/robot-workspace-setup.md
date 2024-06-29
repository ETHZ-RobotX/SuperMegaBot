---
layout: default
title: Setup Robot Workspace
parent: Setting Up
grand_parent: Physical Robot
nav_order: 3
has_toc: false
---

# Robot Workspace Setup
{: .no_toc}

* Table of contents
{:toc}

## Hardware Driver Installation

In the following, the steps required to install the system-level drivers of the sensors are described.

This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors into user's pc.
{: .note }

The system-level software usually needs to be installed once and is already taken care of.
{: .note }

Hardware installation should be on top of the software installation. 
{: .note }

### Motor Controller 
The USB rules for the motor controller driver should be copied to rules.d .
```bash
# Copy the USB rule
# Dont forget to change <>
sudo cp <catkin_ws_dir>/src/smb_common/smb_lowlevel_controller/smb_driver/udev/55-smb.rules /etc/udev/rules.d/
```

### RealSense 
```bash
# Installing necessary libraries for RealSense.
sudo apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE

sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main"

sudo apt update
sudo apt install librealsense2-dev librealsense2-dkms librealsense2-utils

sudo apt install ros-noetic-ddynamic-reconfigure
```

### Robosense
```bash
# Installing necessary libraries for RoboSense.
sudo apt-get install -y libyaml-cpp-dev libpcap-dev libprotobuf-dev protobuf-compiler git
```

### Spinnaker Camera Driver
Download [the spinnaker driver](https://drive.google.com/file/d/1wVK0dAH4mre1Prsr-Wsaowz0_OAmWe2f/view?usp=sharing).
```bash
# Installing necessary libraries for camera driver.
sudo apt install ros-noetic-roslint

cd <Directory_to_download>/

tar -xvf spinnaker-2.4.0.143-Ubuntu20.04-amd64-pkg.tar.gz 
rm spinnaker-2.4.0.143-Ubuntu20.04-amd64-pkg.tar.gz 
cd spinnaker-2.4.0.143-amd64/
sudo dpkg -i libgentl_2.4.0.143_amd64.deb libspinnaker_2.4.0.143_amd64.deb libspinnaker-dev_2.4.0.143_amd64.deb libspinnaker-c_2.4.0.143_amd64.deb libspinnaker-c-dev_2.4.0.143_amd64.deb

# Setting up FLIR driver (libspinnaker). Enter username when asked!
sudo ./configure_gentl_paths.sh 64
sudo ./configure_usbfs.sh
sudo ./configure_spinnaker.sh
sudo ./configure_spinnaker_paths.sh
```

After the installation you can remove the tar.gz file and also the content of it. 

## Setting Up The Hardware Related ROS packages

In this section, the steps required to install the ROS packages related to the SMB hardware are described.

This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors on a personal computer. 
{: .note }

The installation of the hardware related ROS packages should be on in addition to the SMB core software installation. 
{: .note }


* Table of contents
{:toc}

### Download ROS packages
To clone the HW related repositories by using the vcs tool run the following terminal commands sequentially. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb_hw.repos .

# Magic of rosdep
# Install dependencies
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y

```

#### Versavis 
```bash
# Installing necessary libraries for Versavis.
cd <directory_to_catkin_ws>/src/versavis
git submodule update --init

## dependency of rosserial
sudo apt install python3-serial

## install udev rules for versavis
sudo cp <directory_to_catkin_ws>/src/versavis/firmware/98-versa-vis.rules /etc/udev/rules.d/
sudo udevadm control --reload
```

After every installation to build the packages
```bash
# Build it
catkin build smb

# Source it
source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash
```

## Simplify access to SMB

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

The `connect-smb` command doesn't work on Docker running on Mac and Windows, there you can set an allias for exporting the `ROS_MASTER_URI` and manually find the `ROS_IP` of the host using `ifconfig` (e.g: 10.0.X.Y)
{: .warning}

```bash
# For mac/windows docker environment
alias connect-smb261="export ROS_MASTER_URI=http://10.0.1.5:11311 ; export ROS_IP=10.0.1.Y" # replace the Y with the ip of the host computer (outside docker)

# You can define similar commands for other robots
```