---
layout: default
title: Hardware Driver Installation
parent: Operating the SMB
nav_order: 2
---

# Installation of the hardware drivers
{:.no_toc}
In the following, the steps required to install the system-level drivers of the sensors are described.

This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors into user's pc.
{: .smb-mention }

The system-level software usually needs to be installed once and is already taken care of.
{: .smb-mention }

Hardware installation should be on top of the software installation. 
{: .smb-info }

## Table of Contents
* Table of contents
{: .toc }
    

### Motor Controller 
The USB rules for the motor controller driver should be copied to rules.d .
```bash
# Copy the USB rule
# Dont forget to change <>
sudo cp <catkin_ws_dir>/src/smb_lowlevel_controller/smb_driver/udev/55-smb.rules /etc/udev/rules.d/
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


