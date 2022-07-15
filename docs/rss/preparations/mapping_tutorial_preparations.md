---
layout: default
title: Mapping Tutorial
grand_parent: Robotics Summer School
parent: Tutorial Preparations
nav_order: 3
nav_exclude: false
---

# Preparations for Mapping Tutorial

## Download tutorial scripts and data

Download the following [folder](https://drive.google.com/drive/folders/1GC9h8f6164sgmsRAUPblgw6pvxkMf8z0?usp=sharing) which contains the tutorial scripts and maps. You can place this folder anywhere on your filesystem.

## Open3d python install (required for the interactive part of mapping tutorial)

You need to install the open3d python API.

### Option 1 - ppa

You can install open3d from a PPA. The PPA contains Open3d and all dependencies. First add the PPA to your system:

```shell
sudo add-apt-repository ppa:roehling/open3d
sudo apt update
sudo apt install libopen3d-dev
```

### Option 2 - pip

`pip install 'open3d==0.15.2'`

### Option 3 - anaconda

This option is recommended if you are familiar with conda environments. In case you have not used conda and want to learn, you can install anaconda by following the instructions [here](https://linuxize.com/post/how-to-install-anaconda-on-ubuntu-20-04/)

Create a conda environment with python 3.6 or activate an existing one.

#### Install open3d inside conda

`pip install open3d` (or conda install -c open3d-admin -c conda-forge open3d if pip does not work)

### Verify the installation

Check the open3d version (it should be 0.15)

In the terminal open python console (type python in the conda terminal)

```shell
# Import open3d with: `import open3d`
# Check the version by typing: `open3d.__version__`
python -c 'import open3d; print(open3d.__version__)'
```

## open3d_slam install (cpp package, required for building maps)

For running *open3d_slam* you will need the open3D library. Follow [the instructions above](#open3d-python-install-required-for-the-interactive-part-of-mapping-tutorial) to install open3d.

Follow the [documentation on how to update the SMB software](../../core-software/update_software.md) to download the *open3d_slam* repo into your catking workspace. Alternatively, you can clone it manually:

```bash
cd <catkin_ws>/src
git clone https://github.com/leggedrobotics/open3d_slam.git slam/open3d_slam
```

Once the repo has been cloned, build the ROS integration with:

```bash
catkin build open3d_slam_ros
```
Run an example to make sure that your installation is okay (see documentation, sample datasets).

Download a rosbag from [here](#download-rosbags)

Run `roslaunch open3d_slam_ros mapping_rosbag.launch` and pass the rosbag filename as an argument. You can check more detailed documentation on how to run *open3d_slam* [here](https://open3d-slam.readthedocs.io/en/latest/usage.html).

## Miscellaneous

### Download rosbags

In order to follow the tutorial you will need the following rosbags:

- [First mission rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/first_mission_wangen.bag)
- [Second mission rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/second_mission_wangen.bag)
- [Challenge site rosbag](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/challenge_site.bag)


### Download additional pre-built maps for localization

- [Complete map Wangen](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/wangen_map_decimated.pcd)
- [Challenge site map](http://robotics.ethz.ch/~asl-datasets/2021_RSS_datasets/SLAMTutorial/challenge_decimated.pcd)

## The tutorial

Tutorial slides are [here](https://drive.google.com/drive/folders/1pGW5H-B_lmcF_J35kizlfmYaa_C9urtk?usp=sharing)
