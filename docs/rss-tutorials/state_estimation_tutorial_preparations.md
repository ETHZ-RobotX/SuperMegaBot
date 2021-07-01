---
layout: default
title: State Estimation Tutorial
parent: Summer School Tutorials
---

# Preparations for State Estimation Tutorial
For the tutorial you need the following packages:
 - [ethzasl_msf](https://github.com/ethz-asl/ethzasl_msf)
 - [compslam](https://bitbucket.org/leggedrobotics/compslam_rss/src/master/)

You can test it on your own computer by running it with a rosbag provided [bellow](#Download files).

## Installation
Download the repositories in the same directory where ```smb_common``` is and build them:

```bash
cd ~/catkin_ws/src/
git clone https://github.com/ethz-asl/ethzasl_msf.git
git clone https://github.com/ethz-asl/glog_catkin.git
git clone https://github.com/catkin/catkin_simple.git
catkin build loam
catkin build ethzasl_msf
catkin build smb_msf
source ~/catkin_ws/devel/setup.bashrc
```
If there is some issues when building the packages, see trouble shooting [below](#Trouble shooting).

## Running on your own PC with rosbag

```bash
# In Terminal 1
$ roslaunch loam loam_smb.launch use_sim_time:=true publish_map_frame:=true

# In Terminal 2
$ roslaunch smb_msf smb_msf.launch  

# In Terminal 3
$ mkdir -p ~/catkin_ws/src/smb_common/smb_msf/rviz
# Download the rviz file linked below and put it here to make life easier
$ cd ~/catkin_ws/src/smb_common/smb_msf/rviz
$ rviz

# In Terminal 4
$ mkdir -p ~/catkin_ws/src/smb_common/smb_msf/data
# Download the rosbag and put it here
$ cd ~/catkin_ws/src/smb_common/smb_msf/data
$ rosbag play First_mission_wangen_FILTERED.bag --clock 
```
## Running on smb

```bash
# In Terminal 1 on smb
$ roslaunch smb smb.launch
# wait until you see Received first IMU message

# In Terminal 2 on smb
$ roslaunch loam loam_smb.launch 

# In Terminal 3 on smb
$ roslaunch smb_msf smb_msf.launch

# In Terminal 4 on host PC
$ roslaunch rviz
# and change the fixed frame (in global options) to odom
```

## Download files
In order to follow the tutorial you will need the following rosbag and rviz file:
  - [First mission rosbag filtered](https://drive.google.com/file/d/19WjL00NeCvQNPJggVUAQXgWmGNlgPgVX/view?usp=sharing)
  - [Rviz file](https://drive.google.com/drive/folders/1SvpEzsq67P0i6gEAY6Q_5qGgTa0NeC3r)

Download this rosbags into the folder ```~/catkin_ws/src/smb_common/smb_msf/data```

Download this rviz profile into the folder ```~/catkin_ws/src/smb_common/smb_msf/rviz```

## Trouble shooting

1. If you get an error like this when building:

   ```bash
   cc1plus: error: bad value (‘tigerlake’) for ‘-march=’ switch
   ```

   It could be that you need to switch to gcc-10 and g++-10.

   ```bash
   # Install multiple C and C++ compiler versions
   sudo apt -y install gcc-10 g++-10
   # Use the update-alternatives tool to create list of multiple GCC and G++ compiler alternatives
   sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
   sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
   sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 10
   sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10 10
   # Check the available C and C++ compilers list on your Ubuntu 20.04 system and select desired version by entering relevant selection number
   sudo update-alternatives --config gcc
   ```

2. If you are running on a VM and get this error when building:

   ```bash
   c++: fatal error: Killed signal terminated program cc1plus
   ```

   This means that the memory of your VM is not enough, just increase your VM memory and rebuild the packages.
