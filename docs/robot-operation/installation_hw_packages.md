---
layout: default
title: Hardware ROS packages
parent: Operating the SMB
nav_order: 3
---

# Setting Up The Hardware Related ROS packages
{: .no-toc}
In this document, the steps required to install the ROS packages related to the SMB hardware are described.

This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors on a personal computer. 
{: .smb-mention }

The installation of the hardware related ROS packages should be on in addition to the SMB core software installation. 
{: .smb-info }

## Table of Contents
* Table of contents
{: .toc}

## Download ROS packages
To clone the HW related repositories by using the vcs tool run the following terminal commands sequentially. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb_hw.repos?token=AIDKBDU4PBIOTTL4DIPL6R3A2JQ66 .

# Magic of rosdep
# Install dependencies
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y

```

### Versavis 
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
