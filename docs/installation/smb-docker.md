---
layout: default
title: SMB Docker
parent: Installation
nav_order: 3
has_toc: false
---

# 🐳 SMB Docker
{:.no_toc} 

To use the SMB Docker, basic knowledge of Docker is needed. Please check [the official website](https://docs.docker.com) to learn how to build, save, reconnect, etc.
{: .note}

* Table of contents
{:toc}

## Setting up Docker

### 🐧 Linux

1. Install Docker by following [the official website](https://docs.docker.com/engine/install/)
2. Clone the [repo](https://github.com/ETHZ-RobotX/smb_docker/) into a directory on your host computer
3. Run the bash file to create the container

```bash
# Go to the directory where you downloaded the repo to
cd <path/to/repo>

# Activate Container
./create_container.bash
```


This will automatically set up your system to later run the docker and download the pre-compiled image from Docker Hub. Once downloaded, the script starts a container called `smb_container` that can be used to run the SMB software (see [reconnecting to the docker container](#-re-connecting-to-the-docker-container)).

### 🪟 Windows

1. Install Docker Desktop by using [the official website](https://docs.docker.com/desktop/windows/install/)
2. Install VcXsrv [here](https://sourceforge.net/projects/vcxsrv/)
3. Launch VcXsrv and configure the settings as shown in the pictures:

   ![setup 1](../../images/docker_setup_1.png){: width="600px"}

   ![setup 2](../../images/docker_setup_2.png){: width="600px"}

   ![setup 3](../../images/docker_setup_3.png){: width="600px"}

4. Open PowerShell and run

```bash
# Run docker
docker run -it --env="DISPLAY=host.docker.internal:0.0" --volume=smb_volume:/home/catkin_ws/src --net=host --name smb_container ethzrobotx/smb_docker bash
```


5. To exit the container, type `exit` in the terminal.

## 🖥️ Setup Visual Studio Code for Use with Docker Container

Visual Studio Code is a powerful integrated development environment that even allows accessing code inside a Docker container.
Usage of Visual Studio is not necessary.
{: .note}

1. Open Visual Studio Code and install the **dev - containers** extension.
2. Click on the extension on the bottom left corner and attach to the previously created container.
3. When the new window opens, install the **C/C++** and **Python** extensions from Microsoft inside the container. This is needed in order to get autocompletion.
4. The catkin workspace is located in /home/catkin_ws

## 🔄 (Re-)Connecting to the Docker Container

Once you have set up the smb_container, you can create a terminal (bash shell) by running

```bash
docker exec -it smb_container bash
```


There is no need to run the script create_container.sh anymore. 

If you closed all running instances of bash in the `smb_container`, you might need to start it again by running

```bash
# start docker container
docker start smb_container

# create a terminal (bash) in the container:
docker exec -it smb_container bash
```


The latter command can be repeated multiple times to create several terminals in the same container.

## 🕹️ How to Use the Simulation in the Docker Container

If you want to run the simulation, you can follow the [how to run SMB software](../tasks) and run the commands given there in a terminal in the smb_container. I.e.

```bash
# create a terminal (bash) in the container:
docker exec -it smb_container bash
```
