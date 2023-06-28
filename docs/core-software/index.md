---
layout: default
title: SMB Core Software
nav_order: 2
has_children: true
---

# SMB Core Software

{:.no_toc}
The SMB core software allows simulation of the robot in a gazebo environment but is also required on the real robots.

## Using Docker

To run the SMB software only in simulation, you can use a Docker image with pre-compiled software. Details are given in the [SMB docker documentation](docker_installation.md). With this, no further installation is needed.

## Local Installation

Instead of running the docker image, you can install the simulation/SMB core software on a native Ubuntu 20.04 running ROS Noetic: Follow the steps described in the [installation documentation](installation_core.md).


## Starting the Simulation

Once the SMB core software is installed, you can start the simulation by following the steps in [How To Run the SMB Software](HowToRunSoftware.md)
