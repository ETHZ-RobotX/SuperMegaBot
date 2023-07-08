---
layout: default
title: Path Planning Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 4
nav_exclude: false
---

# Preparations for Path Planning Tutorial

To prepare for the Tutorial on Path Planning, only the [SMB core software](../../core-software/installation_core.md) and the [SMB path planner](../../core-software/autonomy_software.md#path-planning) have to be set up and installed.
{: .smb-info }

## Check software installation

To test if the installation is working correctly, source the workspace where the software is installed; then, the following needs to be checked:

1. The simulation is running properly (`$ roslaunch smb_gazebo sim.launch tracking_camera:=true launch_gazebo_gui:=true`)
   * You should see the SMB in RViz and Gazebo
   * `tracking_camera:=true` is necessary as we want to use the tracking camera odometry
   * `launch_gazebo_gui:=true` is used for activating the visualization in gazebo
2. The Path Planner can be launched (`$ roslaunch smb_navigation navigate2d_ompl.launch sim:=true global_frame:=tracking_camera_odom`)
   * You should see the occupancy map in RViz
3. Place a goal using the `2D Nav Goal` from the top toolbar in RViz
   * Make sure to give the goal in the `tracking_camera_odom` frame. This can be changed in the Displays panel.
   * Both a global and a local path have to be generated (global: green line, local: red arrows)
   * The SMB should move while tracking the local path

If everything runs, then the software is working and ready for the tutorial.
