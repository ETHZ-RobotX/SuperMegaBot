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



## Setting up Path Planning

Once you've installed the [SMB core software](installation_core.md), you can directly follow the [documentation](https://github.com/ETHZ-RobotX/smb_path_planner/wiki) in the repository of the SMB Path Planner.

All the relevant repositories should already have been cloned into your catkin workspace when installing the core software.

Run the following command in the catkin workspace to build all the packages related to the path planner:
``` bash
catkin build smb_path_planner
```

## Setting up Mapping and Localization (SLAM)

Follow the instructions given in the [readme of the smb_slam package](https://github.com/ETHZ-RobotX/smb_common/blob/master/smb_slam/README.md) to set up the SLAM software. 


## State Estimation
As an alternative to the visual-inertial odometry based state estimation provided by RealSense tracking camera, you can install a [graph based multi sensor fusion framework](https://github.com/leggedrobotics/graph_msf/).

Follow the instructions given in the [reamde of the smb_msf_graph package](https://github.com/ETHZ-RobotX/smb_common/blob/master/smb_msf_graph/README.md) to install the framework on your system.
