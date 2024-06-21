---
layout: default
title: Exploration
parent: Robot Operation
grand_parent: Physical Robot
nav_order: 5
has_toc: false
---

# 🗺️ Exploration

{: .no_toc}

* Table of contents
{:toc}

## 🛞 SMB core software
Launch the core software on the robot:
```bash
# In the terminal of SMB
roslaunch smb smb.launch
```

## 🧭 Lower Level Planner
Launch the slam:
```bash
# In a new terminal on SMB
roslaunch roslaunch smb_msf_graph smb_msf_graph.launch
```

Launch the local planner and path follower:
```bash
# In a new terminal on SMB
roslaunch smb_navigation navigate2d_cmu.launch use_msf:=true global_frame:=world_graph_msf state_estimation_topic:=/transformed_odom launch_far_planner:=false
```

At this stage you should be able to set the local way points for SMB to follow as described in Navigation section.

## 🗺️ Exploration with TARE Planner

Launch TARE Planner for exploration:
```bash
# In a new terminal on SMB
roslaunch smb_exploration smb_rss_tare.launch rviz:=false
```