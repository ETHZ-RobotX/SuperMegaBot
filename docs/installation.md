
# Setting up the SMB Simulation Software
> The updated SMB software is still work in progress! Thus, this documentation explains the steps to install SMB software. Installation process might lack of some dependencies. 

> Please inform oilter@ethz.ch for any missing library, package, driver, error or any kind of unclear instruction.

## Remark

SMB system consist of two part: simulation and hardware. If you want to use the system on a real SMB Robot with real sensors and actuators, hardware part should be installed **on top of the simulation part**. This document contains the instruction about SMB Simulation Software. To install SMB Simulation Hardware plaese refer to this [document](doc/installation_wh.md).

## Table of Contents
- [Setting up the SMB Simulation Software](#setting-up-the-smb-simulation-software)
  - [Remark](#remark)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Closed source packages](#closed-source-packages)
- [Software Installation](#software-installation)
  - [Catkin Workspace and all Packages](#catkin-workspace-and-all-packages)
  - [Installing Dependencies](#installing-dependencies)
  - [Finalization](#finalization)
- [Hardware Installation](#hardware-installation)
  - [Driver installations:](#driver-installations)
    - [RealSense](#realsense)
    - [Robosense](#robosense)
    - [Spinnaker Camera Driver](#spinnaker-camera-driver)
    - [Versavis](#versavis)

## Prerequisites
- ROS Noetic
> Note that, the system has been developed in Ubuntu 20.04.

To see if the system has the correct ROS distribution please use the following terminal command. 

```bash
echo $ROS_DISTRO
# output: noetic
```
If you do not see the output, please refer to the [official ROS website](http://wiki.ros.org/noetic/Installation/Ubuntu) to install **ROS Noetic Desktop**. 

After installation, please ensure that environment variables like ROS_ROOT and ROS_PACKAGE_PATH are set. In order to verify the installation by running the following terminal command.

```bash
printenv | grep ROS
```
***(TODO: Noetic Desktop or Desktop Full )***

## Closed source packages

Currently, for some of the core software packages, you'll need to be granted access by the [Robotic Systems Lab](https://rsl.ethz.ch/). These repositories are hosted on bitbucket, thus you'll need a bitbucket (Atlassian) account. 
Send your account details (username and associated email address) to [Johannes from RSL](https://rsl.ethz.ch/the-lab/people/person-detail.MjU0MDk1.TGlzdC8yNDQyLC0xNDI1MTk1NzM1.html) and ask for permission to access the RSS related SMB repositories.

# Software Installation

## Catkin Workspace and all Packages

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

<details><summary> Example: </summary>
<p>


```bash
# Example directory to ws and catkin workspace name
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
# Example ends
```

</p>
</details>



To download the SMB packages, the vcs command-line tools will be used. For more information about the tool you can check the [link](http://wiki.ros.org/vcstool).

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
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/smb.repos .
```

## Installing Dependencies

To install the dependencies, rosdep package will be used. For more information about the package you can check the [link](https://docs.ros.org/en/independent/api/rosdep/html/)

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

## Finalization
Since every SMB package and dependency is installed, you can build the project.
```bash
# Navigate to the directory of workspace
cd <directory_to_ws>/<catkin_ws_name>/

catkin build smb_gazebo
```

You should see that every package is built.
After you built the packages, you can add the source file into .bashrc so that you do not have to source it everytime you log in a new terminal. 

```bash
# Do not forget to change <...> parts
echo "source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash" >> ~/.bashrc
```

# Hardware Installation
> Hardware installation should be on top of the software installation. 

> This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors into user's pc. 


To download the SMB packages by using vcs tool run the following terminal commands in order. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/smb_hw.repos .

# Magic of rosdep
# Install dependencies
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
```
## Driver installations: 

> This part has not been tested fully !!!

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
Download [the driver](../drivers/spinnaker-2.4.0.143-Ubuntu20.04-amd64-pkg.tar.gz) from this repo.
```bash
# Installing necessary libraries for RoboSense.
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
catkin build smb
```
