---
layout: default
title: Trajectory Optimization Tutorial
parent: Summer School Tutorials
nav_order: 2
---

# Preparations for Trajectory Optimization Tutorial
To prepare for the Tutorial on Trajectory Optimization, only the [SMB core software](../core-software/installation_core.md) must be set up and installed. However, you need to check out `feature/TO_tutorial` branch on the `smb_common` repository and rebuild it. 

```bash
# Fetch and checkout the branch
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src/smb_common
git fetch origin feature/TO_tutorial
git checkout feature/TO_tutorial

# rebuild
catkin build smb_gazebo
```

## Check software installation
To test if the installation is working correctly, source the workspace where the software is installed; then, the following need to be checked:

1. The SMB Gazebo simulation is running properly (`$ roslaunch smb_gazebo sim.launch mpc:=true`)
	* You should see the SMB in RViz
2. The obstacle-avoidance MPC example becomes active by the first manual command. Place a goal using the `2D Nav Goal` in RViz
	* The SMB should move while avoiding the green pillars
	
If everything runs, then the software is working and ready for the tutorial.
