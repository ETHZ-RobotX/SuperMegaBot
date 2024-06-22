---
layout: default
title: SLAM Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 3
nav_exclude: false
---

# 🧭 Preparations for SLAM Tutorial

This section highlights the steps to follow to prepare for the SLAM tutorial during the Robotics Summer School 2024.

The official documentation can be found in the [open3d_slam_advanced_rss_2024_public](https://github.com/ETHZ-RobotX/open3d_slam_advanced_rss_2024_public) repo.

## 🔧 Setting-up

The tutorial material can be run if you have successfully followed the [installation steps](../../installation/index.md). Using [RSS Workspace](../../installation/rss-workspace.md) is recommended.

```bash
# build smb_slam
catkin build -c smb_msf_graph smb_slam
```

## 📂 Resources

### 🔍 Open3D SLAM Resources

To refer information about `open3d_slam` repo can be found here:
- [Repo](https://github.com/leggedrobotics/open3d_slam)
- [Docs](https://open3d-slam.readthedocs.io/en/latest/)

You have installed everything correctly if building ```smb_slam``` doesn't throw any error.

### 🗃️ ROSBags

In order to follow the tutorial, you might need the following rosbags from `RSS2023` if you plan on creating an offline map:

- [First mission rosbag](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-11-33-01_smb263.bag)
- [Second mission rosbag](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-11-39-50_smb263.bag)
- [Challenge site rosbag](http://robotics.ethz.ch/~asl-datasets/2023_RoboticsSummerSchool_testing_data/2023-06-16-11-45-45_smb263.bag)

### 📋 Tutorial Material

The link for the tutorial slides will be available soon [here]().

The link for the tutorial scripts will be available soon [here]().


<!-- ### Download tutorial scripts and data

Download the following [folder](https://drive.google.com/drive/folders/1UYSW2WWhQVyTyuiPeuYasUF1EvQcqu1R?usp=sharing) which contains the tutorial scripts and maps. -->


<!-- ## Manual Installation (Optional)

### Open3d Python install

You need to install the open3d python API which will be needed for tutorial on scan registration. We will use conda for this.

1. Install anaconda:  
    a. You can follow the instructions [here](https://linuxize.com/post/how-to-install-anaconda-on-ubuntu-20-04/)  
    b. Type ```yes``` to the following prompt(```Do you wish the installer to initialize Anaconda3 by running conda init?```)  
    c. Run the following command so that conda base is not automatically activated in every new terminal:  
         ```conda config --set auto_activate_base false``` 

2. Create a new conda environment:   
    ```
    conda create -n open3d_env python=3.8
    ```

3. Activate the conda environment:  
    ```
    conda activate open3d_env
    ```
4. Install open3d in the activated conda environment.
    ```
    pip install open3d==0.16.0
    ```

#### Verify the installation  

Check the open3d version (it should be 0.16)

1. In a terminal activate the conda environment and open python console:
    ```bash
    conda activate open3d_env
    python
    ```
2. Import open3d and check the version:
    ```
    import open3d
    open3d.__version__
    ```

### Open3d_slam install (cpp package, required for online SLAM and Localization)

Make sure that you have installed the repositories following the instructions [here](https://ethz-robotx.github.io/SuperMegaBot/core-software/installation_core.html
) for core SMB software since we will be running online SLAM in Gazebo simulation.  

Some additional dependencies are required for Open3d_slam for which you can follow these steps:

```bash
sudo apt install libgoogle-glog-dev
sudo apt install libglfw3 libglfw3-dev
sudo apt install ros-noetic-jsk-rviz-plugins
sudo apt install liblua5.2-dev
sudo add-apt-repository ppa:roehling/open3d
sudo apt update
sudo apt install libopen3d-dev
```

You can now go to your rss workspace and directly build the package smb_gazebo and smb_slam by running the following command:

```bash
cd smb_ws # PATH TO YOUR WORKSPACE
catkin build smb_gazebo smb_slam
``` -->