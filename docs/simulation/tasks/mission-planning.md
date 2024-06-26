---
layout: default
title: Mission Planning
parent: Simulation
nav_order: 4
has_toc: false
---

# 📋 Mission Planning

You can plan a set of waypoints or twist messages as your mission where SMB will autonomously execute the specified missions. For more information, refer to [smb_mission_planner](https://github.com/ETHZ-RobotX/smb_mission_planner). The mission planner is based on the popular state machine library `smach`.

To start with, make sure the package is built,

```bash
# build the package
catkin build smb_mission_planner
```

## 🎥 Record a Mission

```bash
# launch the recorder
# if graph_msf is used
roslaunch smb_mission_planner mission_recorder.launch reference_frame:=world_graph_msf mission_file_name:=test_mission.yaml
```

which starts the node. You can then give recording instructions with ROS services. To record a mission, call

```bash
rosservice call /record_mission {"waypoint_mission","waypoint_1_name, waypoint_2_name, ..."}
```
where you can use your own mission_name and waypoint_names. The number of waypoints can be selected arbitrarily, just add more to the list. After you send the `/record_mission` service, instructions will appear in the command window where you launched the node. You can now input the waypoint poses of the current mission one by one. This can be done:

1. in RViz by clicking `2D Nav Goal` and visually placing the pose on your map.
2. by sending the desired pose in the topic `/move_base_simple/goal`.
3. by calling the service `rosservice call /record_base_pose`, which will record the current base pose as a waypoint. Make sure that the odometry topic for the base pose is set correctly (see Advanced Features on how to do that).

After having recorded all your missions, stop the node with `Ctrl-C`. All your recorded missions will be dumped to a YAML file (`mission.yaml` per default).
{: .note}

## 🚀 Run a Mission

The `mission_planner.py` executes the previously defined mission plan.

Remember to start the `graph_msf` and `smb_gazebo` using the steps in [navigation](../tasks/navigation.md).
{: .note}

Start the simulation and the path planner.
```bash
# launch the FAR planner
roslaunch smb_navigation navigate2d_cmu.launch use_msf:=true global_frame:=world_graph_msf state_estimation_topic:=/transformed_odom 
```

As soon as the path planner is ready to receive goals, start the `mission_planner` with

```bash
# launch the mission planner
roslaunch smb_mission_planner mission_planner.launch reference_frame:=world_graph_msf mission_file_name:=test_mission.yaml
```

The robot will now try to reach the specified waypoints of each mission one by one, as defined in the `yaml` file. In the command line window of the `mission_planner` you can find information on where and in which mission you currently are.

In order to make the above command run, you need to add few twist mission in the test_mission.yaml (since the provided mission_planner.py expect first to execute a FARWaypointMission and then a TwistMission). For this you can copy the twist mission from mission.yaml
```
twist_mission:
  twist_1:
    lin_vel: 1
    ang_vel: 1
    time: 5
  twist_2:
    lin_vel: 1
    ang_vel: 1
    time: 5
  twist_3:
    lin_vel: 1
    ang_vel: 1
    time: 5
```
and append it to the test_mission.yaml you just created. 


Example mission yaml file: 
[`mission.yaml`](https://github.com/ETHZ-RobotX/smb_mission_planner/blob/master/configs/missions/mission.yaml)

Please note that you need to edit the `mission_planner.py` as required to make it work, you can also refer to the [`mission_planner.py`](https://github.com/ETHZ-RobotX/smb_mission_planner/blob/master/src/smb_mission_planner/mission_planner.py) for an example implementation.
{: .note}
