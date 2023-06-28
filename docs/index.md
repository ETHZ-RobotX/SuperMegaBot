---
layout: default
title: The SuperMegaBot
nav_order: 1
---

# The SuperMegaBot
{:.no_toc}
Documentation of the SuperMegaBot (SMB) for the ETHZ Robotics Summer School.

* Table of contents
{:toc}

## Introduction
This documentation aims at introducing basic usage of the SMB software.
 
A [simulation environment](#the-simulation) based on Gazebo can be used to get a basic understanding of the SMB software and perform basic testing.
This simulation is part of the core software setup.

Furthermore, the fundamentals of how to use the real robot are described as well.

## The Simulation
For simulation of the SuperMegaBot the Gazebo environment is used.
It incorporates a simulation of the 4-wheeled robot including most of its sensors (16 beam Lidar, RGB camera, tracking camera, IMU)

### Setup
To setup the simulation, you have two options:

  1. Use a [docker environment](core-software/docker_installation.md) or
  2. follow the steps described in the [core software documentation](core-software/installation_core.md) to install the software stack in a native Ubuntu 20.04 environment. 


### Running the simulation environment
Once the SMB software is setup, you can start the simulation by following the steps in [How To Run the SMB Software](core-software/HowToRunSoftware.md)

## Operating the real robot
Please follow the steps described in [How to use the SMB](robot-operation) to operate a SuperMegaBot.

## Issue tracking
Please use the [issues page](https://github.com/ETHZ-RobotX/SuperMegaBot/issues) to report any issues concerning the robots (hardware and software related issues).

## History
The SuperMegaBot was originally developped by the ETH Construction Robotics group. It is now maintained by the [ETHZ RobotX Center](https://center-for-robotics.ethz.ch/).

### RSS 2019 Edition
See the [link](https://github.com/ethz-asl/eth_supermegabot)
