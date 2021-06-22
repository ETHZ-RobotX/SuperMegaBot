---
layout: default
title: Operating the SMB
nav_order: 3
has_children: true
---

# How to use the SMB

## Connecting to the SMB
The necessary steps to power up the payload (on-board computer, network and sensors) and connect to the on-board computer are described in [How to connect to the SMB document](HowToConnectToSMB.md)

## Hardware related software
In order to be able to use the various sensors mounted on the SMB, the respective drivers and ROS packages need to be installed. 
While the [installation of the system-level drivers](installation_drivers.md) is already taken care of, the [hardware related ROS packages](installation_hw_packages.md) need to be added to the catkin workspace and built.

## Driving the SMB
The steps necessary to allow either manual or autonomous operations of the SuperMegaBot are described in [How to drive the SMB](HowToDriveTheSMB.md)
