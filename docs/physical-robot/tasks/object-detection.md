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
- `object_detection_classes="[0,1,2,10]"`: Populate this list with the IDs of objects added to the real scene. If you leave this empty, it will try to detect the following objects `[0,24, 25, 28, 32, 39, 41, 45, 46, 47, 56]` from the dataset. To see what numbers correspond to what items, check out the [Artefact Detection Tutorial](../../rss/preparations/artefact_detection_tutorial_preparations.md) page and look for the **YOLOv5 Supported Object Classes** section. The example `[0, 1, 2, 10]` corresponds to person, bicycle, car, and fire hydrant.

To launch the detection pipeline locally, run:

```bash
# In the host PC
roslaunch object_detection object_detection.launch object_detection_classes="[0,1,2,10]"
```

To view the bounding boxes and get more information about the detections use the following two commands:

```bash
rosrun rqt_image_view rqt_image_view
```

Then select the following topic to see the bounding boxes in the image: 

```
/object_detector/detections_in_image
```

To get more information like position, classification, etc. subscribe to or echo the following topic: 

```bash
rostopic echo /object_detector/detection_info
```

For more information, please check out the [Artefact Detection Tutorial](../../rss/preparations/artefact_detection_tutorial_preparations.md).
