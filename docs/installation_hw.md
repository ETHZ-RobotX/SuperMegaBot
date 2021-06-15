---
nav_exclude: true
---

# Setting Up The Hardware Related Software
In the following, the steps required to use all the hardware installed on the SuperMegaBot are described.

> This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors into user's pc. 

> Hardware installation should be on top of the software installation. 

## Table of Contents
- [Setting Up The Hardware Related Software](#setting-up-the-hardware-related-software)
  - [Table of Contents](#table-of-contents)
  - [ROS packages](#ros-packages)
  - [Driver installations:](#driver-installations)
    - [Motor Controller](#motor-controller)
    - [RealSense](#realsense)
    - [Robosense](#robosense)
    - [Spinnaker Camera Driver](#spinnaker-camera-driver)
    - [Versavis](#versavis)
    

## ROS packages
To download the SMB packages by using vcs tool run the following terminal commands in order. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
<<<<<<< HEAD
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb_hw.repos?token=AIDKBDU4PBIOTTL4DIPL6R3A2JQ66 .
=======
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb_hw.repos?token=AIDKBDRWKPPOBGOC4HJ2DZ3AZRNF4 .
>>>>>>> f4dd4a002fe188cda94e8d58118499b683bbefb1

# Magic of rosdep
# Install dependencies
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y

# Add user in dialout group
sudo adduser $USER dialout

```
## Driver installations: 


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
