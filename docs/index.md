# The SuperMegaBot
{:.no_toc}
Documentation of the SuperMegaBot (SMB) for the ETHZ Robotic Summer School.

* Table of contents
{:toc}

## Introduction
This documentation aims at introducing basic usage of the SMB software. 
To get a basic understanding and perform basic testing, a simulation environment based on Gazebo can be used.
This simulation is part of the basic software setup.

Furthermore, the fundamentals in how to use the real robot is described as well.

## The Simulation
For simulation of the SuperMegaBot, the Gazebo environment is used. 
It incorporates a simulation of the 4-wheeled robot including most of its sensors:
- 16 beam Lidar
- RGB camera
- Tracking camera
- IMU

### Installation
To install the simulation, follow the steps described in the [installation documentation](installation.md).

### Running the simulation environment
_refer to documentation of simulation_

## Operating the real robot
_Detailed information on extra pages_

_Content of those might be:_

### Control of robot using RC control
Robots can be controlled using a RC remote

### Using ROS environment 
- reading sensors (incl. joypad commands)
- sending control commands using the ROS environment (i.e. controlling the robot using joypad)
