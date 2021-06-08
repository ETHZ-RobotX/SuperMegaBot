
# Setting up the SMB Simulation Software
> The updated SMB software is still work in progress! Thus, this documentation explains the steps to install SMB software. Installation process might lack of some dependencies. 

> Please inform oilter@ethz.ch for any missing library, package, driver, error or any kind of unclear instruction.

## Remark

The SMB software consists of two parts: core and hardware related.

If you want to use the system on a real SMB robot with real sensors and actuators, the [hardware related part](installation_hw.md) should be installed **on top of the core part**. This document contains the instructions about SMB core software, which also contains the simulation environment.

## Table of Contents
- [Setting up the SMB Simulation Software](#setting-up-the-smb-simulation-software)
  - [Remark](#remark)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Closed source packages](#closed-source-packages)
- [Software Installation](#software-installation)
  - [Catkin Workspace and all Packages](#catkin-workspace-and-all-packages)
  - [Installing Dependencies](#installing-dependencies)
  - [Finalization](#finalization)


## Prerequisites
- ROS Noetic
> Note that, the system has been developed in Ubuntu 20.04.

To see if the system has the correct ROS distribution please use the following terminal command. 

```bash
echo $ROS_DISTRO
# output: noetic
```
If you do not see the output, please refer to the [official ROS website](http://wiki.ros.org/noetic/Installation/Ubuntu) to install **ROS Noetic Desktop**. 

After installation, please ensure that environment variables like ROS_ROOT and ROS_PACKAGE_PATH are set. In order to verify the installation by running the following terminal command.

```bash
printenv | grep ROS
```
***(TODO: Noetic Desktop or Desktop Full )***

## Closed source packages

Currently, for some of the core software packages, you'll need to be granted access by the [Robotic Systems Lab](https://rsl.ethz.ch/). These repositories are hosted on bitbucket, thus you'll need a bitbucket (Atlassian) account. 
Send your account details (username and associated email address) to [Johannes from RSL](https://rsl.ethz.ch/the-lab/people/person-detail.MjU0MDk1.TGlzdC8yNDQyLC0xNDI1MTk1NzM1.html) and ask for permission to access the RSS related SMB repositories.

# Software Installation

## Catkin Workspace and all Packages

Create a new catkin workspace.

```bash
# create the directories
# Do not forget to change <...> parts
mkdir -p <directory_to_ws>/<catkin_ws_name>/src
cd <directory_to_ws>/<catkin_ws_name>/

# initilize the catkin workspace
catkin init
catkin config --extend /opt/ros/noetic
catkin config -DCMAKE_BUILD_TYPE=Release
```

<details><summary> Example: </summary>
<p>


```bash
# Example directory to ws and catkin workspace name
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
# Example ends
```

</p>
</details>



To download the SMB packages, the vcs command-line tools will be used. For more information about the tool you can check the [link](http://wiki.ros.org/vcstool).

To install ***vcstool*** run the following terminal command.

```bash
sudo apt install python3-vcstool
```
To download the SMB packages by using vcs tool run the following terminal commands in order. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/smb.repos .
```

## Installing Dependencies

To install the dependencies, rosdep package will be used. For more information about the package you can check the [link](https://docs.ros.org/en/independent/api/rosdep/html/)

To install ***rosdep*** package run the following terminal commands in order, unless you did not do in the ROS installation step.

```bash
sudo apt-get install python3-rosdep
sudo rosdep init
rosdep update
```

To download the SMB dependencies by using rosdep package run the following terminal commands in order. 
```bash
# Navigate to the directory of workspace
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Magic of rosdep
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y
```

Installing all the dependency may take a while. 

## Finalization
Since every SMB package and dependency is installed, you can build the project.
```bash
# Navigate to the directory of workspace
cd <directory_to_ws>/<catkin_ws_name>/

catkin build smb_gazebo
```

You should see that every package is built.
After you built the packages, you can add the source file into .bashrc so that you do not have to source it everytime you log in a new terminal. 

```bash
# Do not forget to change <...> parts
echo "source <directory_to_ws>/<catkin_ws_name>/devel/setup.bash" >> ~/.bashrc
```

### Hardware related software
To get everything running on the real robot, you also need to follow the steps describe in the [hardware related software installation description](installation_hw.md).
