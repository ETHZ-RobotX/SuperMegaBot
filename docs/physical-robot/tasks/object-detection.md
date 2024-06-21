---
layout: default
title: Object Detection
parent: Robot Operation
grand_parent: Physical Robot
nav_order: 6
has_toc: false
---

# 🕵️‍♂️ Object Detection 

Once the planner is set up and the real SMB is running, you can begin experimenting with object detection. Ensure that the `object_detection` package is built. If it isn't, use the following command:

```bash
# On the host PC
catkin build object_detection   
```

Next, launch the object detection locally with these parameters for the real robot:

- `model_path=""`: Don't set this parameter if you want to use the pre-installed model. If you have a downloaded model, specify its path.
- `model="yolov5l6"`: Selects the pre-installed YOLOv5 model.
- `object_detection_classes="[0,1,2,10]"`: Populate this list with the IDs of objects added to the Gazebo scene. If you leave this empty, it will try to detect all the objects. To see what numbers correspond to what items, check out the [Artefact Detection Tutorial](../../rss/preparations/artefact_detection_tutorial_preparations.md) page and look for the **YOLOv5 Supported Object Classes** section. `[0, 1, 2, 10]` correspond to person, bicycle, car, and fire hydrant.

To launch the detection pipeline locally, run:

```bash
# In the host PC
roslaunch object_detection object_detection.launch object_detection_classes="[0,1,2,10]"
```

For more information, please check out the [Artefact Detection Tutorial](../../rss/preparations/artefact_detection_tutorial_preparations.md).
