---
layout: default
title: Path Planning Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 4
nav_exclude: false
---

# Preparations for Path Planning Tutorial

To prepare for the Tutorial on Path Planning, only the [SMB core software](../../core-software/installation_core.md) and the [SMB path planner](../../core-software/autonomy_software.md#path-planning) has to be set up and installed.
{: .smb-info }

## Check software installation

To test if the installation is working correctly, source the workspace where the softare is installed; then, the following needs to be checked:

1. The SMB Gazebo simulation is running properly (`$ roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true`)
   * You should see the SMB in RViz
   * `launch_gazebo_gui:=true` is used for creating a gazebo and visualizing it
2. The Path Planner can be launched (`$ roslaunch smb_navigation navigate2d_ompl.launch sim:=true global_frame:=tracking_camera_odom`)
   * You should see the occupancy map in RViz
3. Place a goal using the `2D Nav Goal` in RViz
   * A global and a local paths have to be generated
   * The SMB should move while tracking the local path

If everything runs, then the software is working and ready for the tutorial.

## Tutorial Slides

The slides for the tutorial are available [here](https://docs.google.com/presentation/d/1wrH-gTAJQq2iququ-cOHDCa6Z_HXRueYX-B6Pd9Bt50/edit?usp=sharing) (pdf version available [here](https://github.com/ETHZ-RobotX/smb_path_planner/blob/master/docs/Path%20Planning%20Tutorial%20-%20Summer%20School%202021.pdf)).
