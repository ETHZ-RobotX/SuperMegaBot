---
layout: default
title: Physical Robot
nav_order: 4
has_children: true
has_toc: false
---

# 🤖 Physical Robot

This section contains the documentation related to working with the physical SMB robot. This includes setting up hardware, driving the robot, and achieving different tasks.

## 🔌 Connecting to the SMB

The necessary steps to power up the payload (on-board computer, network, and sensors) and connect to the on-board computer are described in [How to connect to the SMB document](setting-up/connect-to-robot.md).

## 🛠️ Hardware-Related Software

To use the various sensors mounted on the SMB, the respective drivers and ROS packages need to be installed. While the [installation of the system-level drivers](setting-up/robot-workspace-setup.md#hardware-driver-installation) is already taken care of, the [hardware-related ROS packages](setting-up/robot-workspace-setup.md#setting-up-the-hardware-related-ros-packages) need to be added to the catkin workspace and built.

## 🚗 Driving the SMB

The steps necessary to allow either manual or autonomous operations of the SuperMegaBot are described in [How to drive the SMB](setting-up/powerup-and-drive.md).

## Table of Content

- [🔧 Setting Up](setting-up)
    - [⚡ Powerup and Drive](setting-up/powerup-and-drive.md)
    - [🔌 Connect to Robot](setting-up/connect-to-robot.md)
    - [🏗️ Setup Robot Workspace](setting-up/robot-workspace-setup.md)
        - [Hardware Driver Installation](setting-up/robot-workspace-setup.md#hardware-driver-installation)
        - [ROS Workspace Setup](setting-up/robot-workspace-setup.md#setting-up-the-hardware-related-ros-packages)
        - [Simplify Access to SMB](setting-up/robot-workspace-setup.md#simplify-access-to-smb)
- [🎯 Tasks](tasks)
    - [🔧 OPC](tasks/opc.md)
    - [📡 State Estimation](tasks/state-estimation.md)
    - [🚀 Navigation](tasks/navigation.md)
    - [🗺️ Mission Planning](tasks/mission-planning.md)
    - [🌍 Exploration](tasks/exploration.md)
    - [🔍 Object Detection](tasks/object-detection.md)
