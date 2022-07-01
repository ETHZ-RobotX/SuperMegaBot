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

The MPC is not operational in its current state though, as it is missing some code that will be completed by you during the tutorial.

## Check software installation
To test if the installation is working correctly, source the workspace where the software is installed.

Then, check if the SMB Gazebo simulation is running properly.
```bash
roslaunch smb_gazebo sim.launch
```
You should now see the SMB in RViz.


If everything runs, then the software is working and ready for the tutorial.

## Background
During the tutorial, we will work with our implementation of SLQ-MPC, a Nonlinear Model Predictive Control method.
You can read up on the method in this paper:

M. Neunert et al., “Fast nonlinear Model Predictive Control for unified trajectory optimization and tracking,” in 2016 IEEE International Conference on Robotics and Automation (ICRA), May 2016, pp. 1398–1404. doi: 10.1109/ICRA.2016.7487274.

You won't have to implement the method, but we will give you our implementation in the [OSC2](https://github.com/leggedrobotics/ocs2) framework.
OCS2 is a software developed in our lab to bring MPC to real robots. It has been deployed on various systems, including walking robots, mobile manipulators, construction machines, and flying robots.
