---
layout: default
title: Trajectory Optimization Tutorial
parent: Summer School Tutorials
nav_order: 2
---

# Preparations for Trajectory Optimization Tutorial
To prepare for the Tutorial on Trajectory Optimization, only the [SMB core software](../core-software/installation_core.md) must be set up and installed. 

Furthermore, you can already build the current state of the `smb_mpc` package. In the catkin workspace, run:
```bash
catkin build smb_mpc
```

The MPC is not operational in it's current state though, as it is missing some code that will be completed by you during the tutorial.

## Check software installation
To test if the installation is working correctly, source the workspace where the software is installed.

Then, check if the SMB Gazebo simulation is running properly.
```bash
roslaunch smb_gazebo sim.launch
```
You should now see the SMB in RViz.


If everything runs, then the software is working and ready for the tutorial.


