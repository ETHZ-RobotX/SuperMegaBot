---
layout: default
title: Path Planning Tutorial
parent: Summer School Tutorials
nav_order: 4
---

# Preparations for Path Planning Tutorial
To prepare for the Tutorial on Path Planning, only the [SMB core software](../core-software/installation_core.md) and the [SMB path planner](../core-software/autonomy_software.md#path-planning) has to be set up and installed.

# Check software installation
To test if the installation is working correctly, source the workspace where the softare is installed; then, the following need to be checked:

1. The SMB Gazebo simulation is running properly (`$ roslaunch smb_gazebo sim.launch launch_gazebo_gui:=true`)
	* You should see the SMB in RViz
	* `launch_gazebo_gui:=true` is used for creating a gazebo and visualizing it
2. The Path Planner can be launched (`$ roslaunch smb_navigation navigate2d_ompl.launch sim:=true global_frame:=tracking_camera_odom`)
	* You should see the occupancy map in RViz
3. Place a goal using the `2D Nav Goal` in RViz
	* A global and a local paths have to be generated
	* The SMB should move while tracking the local path
	
If everything runs, then the software is working and ready for the tutorial.
	
# Tutorial Slides
The slides for the tutorial will be available online just before the tutorial.
