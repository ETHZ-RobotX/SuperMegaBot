---
layout: default
title: Introduction
nav_order: 1
has_children: true
has_toc: false
---

# 🤖 The SuperMegaBot
{:.no_toc}

Welcome to the documentation of the SuperMegaBot (SMB) for the ETHZ Robotics Summer School.

<img src="{{ 'images/smb_closeup.jpeg' | absolute_url }}" width="100%" alt="Image of SMB">

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📘 Introduction
This documentation aims to introduce the basic usage of the SuperMegaBot, a 4-wheeled skid-steered robot, in both simulation and real robot scenarios. Furthermore, it provides instructions on how to run different tasks using the robot and includes step-by-step tutorials.

<!-- The experience is twofold: a [simulation environment](#smb-simulation) using Gazebo, and the physical robot. The software stack runs on ROS Noetic. -->

## 📥 Install the SMB Software locally

To get started, please refer to the [installation guide](installation/index.md).

## 📚 Documentation Structure

The documentation is mainly divided into two parts: [Simulation](simulation/index.md) and [Physical Robot](physical-robot/index.md). The simulation part is designed to provide a comprehensive understanding of the robot and allow for testing, even without access to the physical robot. The physical robot part is for setting up the physical robot and running different tasks using the robot.

## 🖥️ SMB Simulation
For simulating the SuperMegaBot, we utilize the Gazebo environment. It includes a simulation of the 4-wheeled robot, complete with its sensors (16-beam Lidar, RGB camera, tracking camera, IMU). The simulation environment is designed to provide a comprehensive understanding of the robot and allow for testing, even without access to the physical robot.

Once you have successfully installed the SMB software, you can start the simulation by following the steps in [Simulation Tasks](simulation/index.md).

## 🤖 SMB Physical Robot
To set up the physical robot, please refer to the [setting up the physical robot](physical-robot/setting-up/index.md) guide.
Once the setup is complete, you can explore how SMB can be operated by referring to the [robot operation](physical-robot/tasks/index.md) section.

For more information about the robot hardware, you can visit the [robot hardware](info/robot-hardware.md) page.


## 🐞 Issue Tracking
Please use the [issues page](https://github.com/ETHZ-RobotX/SuperMegaBot/issues) to report any issues concerning the robots (hardware and software related issues).

## 📜 History
The SuperMegaBot was originally developed by the ETH Construction Robotics group. It is now maintained by the [ETHZ RobotX Center](https://center-for-robotics.ethz.ch/).

### 📅 RSS 2019 Edition
See the [link](https://github.com/ethz-asl/eth_supermegabot).
