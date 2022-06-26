---
layout: default
title: State Estimation Tutorial
parent: Summer School Tutorials
nav_order: 1
---

# Preparations for State Estimation Tutorial
To prepare for the Tutorial on State Estimation, first set up and install the [SMB core software](../core-software/installation_core.md).

The only required additional packages needed for the state estimation tutorial are [glog_catkin](https://github.com/ethz-asl/glog_catkin.git) and [msf](https://github.com/ethz-asl/ethzasl_msf). 
Both of these packages are also included in the `smb.repos`-vcs file, and automatically cloned to `se/msf` and `se/glog_catkin`.

## Download files
In order to follow the tutorial you will need the following rosbag.
  - [First mission rosbag filtered](https://drive.google.com/file/d/1XovmdpOW9vCzG81Ajre9_1AxS0UCFhmh/view?usp=sharing)

Download the rosbag into a folder of your choice. In the tutorial this location will be denoted as `<path_to_bag>`.

## Compile The C++ Code
To compile the required packages, simply run
```bash
catkin build smb_msf
```
These instructions are also provided in the [SLAM and Navigation](../core-software/autonomy_software.md) instructions.

### Check The Compiled Code
You can test the success of the compilation by running the code.

```bash
# In Terminal 1
$ roslaunch smb_msf smb_msf.launch
```
If everything launches without any error messages, your C++ software is ready for the tutorial.

## Checking the Python Code
For visualization purposes we also provide a Python node inside smb_msf.
Make sure that you have all packages required for running the node:
* numpy
* matplotlib
* rospy

Try to run the visualizer node, using the following command:
```bash
# In Terminal 2
roslaunch smb_msf plotting.launch
```
If no import error occurs, you are ready for the summer school tutorial.

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
