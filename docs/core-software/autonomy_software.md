---
layout: default
title: SLAM and Navigation
parent: SMB Core Software
nav_order: 3
---

# Setting up the SMB Software for Autonomous Navigation
{:.no_toc} 


Please [create an issue](https://github.com/ETHZ-RobotX/SuperMegaBot/issues/new) for any missing library, package, driver, error or any kind of unclear instruction.
{: .smb-mention }


* Table of contents
{:toc}

## Remark
{:.no_toc} 

Please follow the steps described in the [installation documentation](installation_core.md) of the SMB core software before, in order to have the required dependencies for the SLAM and navigation related software.

If you want to use the system on a real SMB robot with real sensors and actuators, the [hardware related part](../robot-operation/installation_hw_packages.md) should be installed **on top of the core part**. This document contains the instructions about SMB core software, which also contains the simulation environment.



## Path Planning
Once you've installed the [SMB core software](installation_core.md), you can directly follow the [documentation](https://github.com/ETHZ-RobotX/smb_path_planner/wiki) in the repository of the SMB Path Planner.

All the relevant repositories should already have been cloned into your catkin workspace when installing the core software.

Run the following command in the catkin workspace to build all the packages related to the path planner:
``` bash
catkin build smb_path_planner
```

## Mapping and Localization (SLAM)
The mapping and localization packages have only be tested on the real robot and on recorded datasets and has not been tested in the simulation environment.
{: .smb-mention }

As for the path planning software packages, also the mapping and localization related packages are already downloaded when you [cloned the list of repositories](../core-software/installation_core.html#catkin-workspace-and-all-packages) contained in `smb.repos` and [installed all the dependencies using the rosdep tool](installation_core.md#installing-dependencies). 

Just run the following command in the catkin workspace to build all the SLAM related packages:
``` bash
catkin build smb_slam
```

## State Estimation
As an alternative to the camera-based state estimation provided by RealSense, you can run a custom extended Kalman filter and fuse lidar-localization measurements with IMU measurements.

Same as for the other two packages, MSF and ICP localization are already included in the [core repositories](../core-software/installation_core.html#catkin-workspace-and-all-packages) contained in `smb.repos`.

First clone the following package into your workspace:
```bash
git clone https://github.com/ethz-asl/glog_catkin.git
```
Then just run the following command in the catkin workspace to build all related packages:
```bash
catkin build smb_msf
```
