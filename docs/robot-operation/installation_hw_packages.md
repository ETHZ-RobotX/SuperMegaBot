# Setting Up The Hardware Related ROS packages
{: .no-toc}
In this document, the steps required to install the ROS packages related to the SMB hardware are described.

This section is only for the SMB itself. It is not needed to install drivers and packages related to sensors on a personal computer. 
{: .smb-mention }

The installation of the hardware related ROS packages should be on in addition to the SMB core software installation. 
{: .smb-info }

## Table of Contents
* Table of contents
{: .toc}

## Download ROS packages
To clone the HW related repositories by using the vcs tool run the following terminal commands sequentially. 

```bash
# Navigate to the directory of src
# Do not forget to change <...> parts
cd <directory_to_ws>/<catkin_ws_name>/src

# Download the packages
vcs import --recursive --input https://raw.githubusercontent.com/ETHZ-RobotX/SuperMegaBot/master/smb_hw.repos?token=AIDKBDU4PBIOTTL4DIPL6R3A2JQ66 .

# Magic of rosdep
# Install dependencies
rosdep install --from-paths . --ignore-src --os=ubuntu:focal -r -y

```
