---
layout: default
title: Trajectory Optimization
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 2
nav_exclude: false
---

# 🚀 Preparations for Trajectory Optimization Tutorial

To prepare for the Tutorial on Trajectory Optimization, only the [OCS2](https://leggedrobotics.github.io/ocs2/overview.html) toolbox must be set up. We provide the required packages in `lib/ocs2`. The only packages we will be using are `ocs2_legged_robot_ros` and `ocs2_legged_robot`, which contain all the code to run the tutorial.

You can already build the current state of the `ocs2_legged_robot_ros` package. In the catkin workspace, run:
```bash
catkin build ocs2_legged_robot_ros
```

The package is not operational in its current state, though, as it is missing some code that will be completed by you during the tutorial.

N.B. If the build fails on a Mac, add the CMake flag
```bash
set(TARGET GENERIC CACHE STRING "Set CPU architecture target" FORCE)
```
inside `lib/ocs2/ocs2_sqp/hpipm_catkin/CMakeLists.txt`.

## 🔧 Check Software Installation

After building the package, you can try to launch the node by running the following command in the catkin workspace:
```bash
roslaunch ocs2_legged_robot_ros legged_robot_ddp.launch
```
This should start up the automatic differentiation module and launch an RViz window with the robot visualization and three separate terminals. If everything runs, then the software is working and ready for the tutorial.

N.B. If you try to provide a command to the robot at this stage, it will not work and will throw out errors in the terminal window. This is because of the missing code that you will complete during the tutorial.

## 📚 Background

During the tutorial, we will work with our implementation of SLQ-MPC, a Nonlinear Model Predictive Control method, and apply it in the case of legged robot locomotion control. You can read up on the method in this paper:

M. Neunert et al., “Fast nonlinear Model Predictive Control for unified trajectory optimization and tracking,” in 2016 IEEE International Conference on Robotics and Automation (ICRA), May 2016, pp. 1398–1404. doi: 10.1109/ICRA.2016.7487274.

You won't have to implement the method, but we will give you our implementation in the [OCS2](https://github.com/leggedrobotics/ocs2) framework. OCS2 is software developed in our lab to bring MPC to real robots. It has been deployed on various systems, including walking robots, mobile manipulators, construction machines, and flying robots.
