---
layout: default
title: State Estimation
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 1
nav_exclude: false
---

# Preparations for State Estimation Tutorial
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{: .important }
> To prepare for the Tutorial on State Estimation, make sure [SMB simulation environment](../../simulation/setting-up/index.md) is set up and running.

## Download files
In order to follow the tutorial you will need the rosbag files located in the following folder:
  - [Rosbag folder](https://drive.google.com/drive/folders/1wOOfgYPC7JieQTXkpSQL0dHi8cU4xAJL?usp=sharing)

Download the rosbag(s) into a folder of your choice. In the tutorial this location will be denoted as `<path_to_bagfile>`.

---

## Compile gtsam_catkin

To compile the required packages, simply run
```bash
catkin build gtsam_catkin
```
This will build gtsam in you workspace and could take up to 5 minutes depending on your CPU.

{: .note}
The very first build of `gtsam_catkin` usually takes longer than subsequent build. Even after cleaning the build result with `catkin clean`, it will still be much faster, as the compiled binaries are preserved in the `lib/gtsam_catkin` folder in the source space.

---

## Build smb_msf_graph
To build `smb_msf_graph` run
```bash
catkin build smb_msf_graph
```
This will compile all dependencies present in the workspace, including open3d_slam.

---

## Check the compiled code
You can test the success of the compilation by running the following code (from the root directory of the workspace).

```bash
source devel/setup.bash    # or `wssetup` if you are using rss_workspace
roslaunch smb_msf_graph smb_msf_graph.launch
```
If everything launches without any error messages, your C++ software is ready for the tutorial.

---

## Running the ROS Bag File in Docker (Only for rss_workspace and smb_docker)

### Copying the ROS Bag File into the Docker Container

If you use `rss_workspace` and `smb_docker`, you can copy them into the Docker container using the docker cp command. Ensure the Docker container is running before performing these steps:

1. Find the name of the Docker container by running the following command (make sure your Docker container is running)

   ```bash
   docker ps
   ```

   The output will look like this if you are using the rss_workspace:
   ```
   CONTAINER ID   IMAGE                            COMMAND       CREATED         STATUS         NAMES
   1234567890ab   vsc-rss_workspace-123asd-uid     "/bin/bash"   5 minutes ago   Up 5 minutes   sad_hawking
   ```
   
   or like this if you are using the smb_docker:
   ```
   CONTAINER ID   IMAGE             COMMAND       CREATED         STATUS         NAMES
   1234567890ab   smb_docker        "/bin/bash"   5 minutes ago   Up 5 minutes   sad_hawking
   ```

   In this example, the name of the Docker container is `sad_hawking`.

2. Copy the ROS bag file into the Docker container, replacing `<NAME-OF-CONTAINER>` with the actual name of the Docker container and `/path/to/your/rosbag.bag` with the path to the ROS bag file on your local machine:

   ```bash
   docker cp /path/to/your/rosbag.bag <NAME-OF-CONTAINER>:/workspaces/rss_workspace/src/rosbags/
   ```

   {: .note}
   If you are using vscode, you can try to drag and drop the rosbag into the vscode file explorer to copy it into the container. But be aware that this might take longer than `docker cp`. For example, it might take a few minutes to copy a 1GB file.

3. Navigate to the directory containing the ROS bag file inside the container:

   ```bash
   cd /workspaces/rss_workspace/src/rosbags
   ```

4. Play the ROS bag file:

   ```bash
   rosbag play <rosbag_name>.bag
   ```

   {: .note }
   > If the bag file does not run and you see an error like:
   >
   > ```
   > [ERROR] [1718830710.056746147]: [registerPublisher] Failed to contact master at [localhost:11311]. Retrying...
   > ```
   > You might need to start the ROS master with the following command:
   > ```
   > roscore
   > ```

---

## (Optional, but recommended) System Installs
* terminator, because multiple terminals will be needed during the tutorial.

```bash
sudo apt-get install terminator
```

{: .note}
If you are using [rss_workspace](../../installation/rss-workspace.md), jsk_rviz_plugins is already installed.

* jsk_rviz_plugins, for visualizing TF-paths in RVIZ.


```bash
sudo apt-get install ros-noetic-jsk-rviz-plugins
```

