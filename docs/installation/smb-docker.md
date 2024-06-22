---
layout: default
title: SMB Docker
parent: Installation
nav_order: 2
has_toc: false
---

# 🐳 SMB Docker
{:.no_toc} 

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Using Docker for the SuperMegaBot Software
{:.no_toc} 

## Pre-requisites
1. Install Docker by following [the official website](https://docs.docker.com/get-docker/)

2. (Required if you want to run GUI application with VNC) Install Real VNC Viewer by following [the official website](https://www.realvnc.com/en/connect/download/viewer)

3. Clone this repository to your local machine

---

## Running the Docker container

There are two ways to run the Docker container. Choosing which one to use depends on how you want to use the GUI application. 

If you have a Linux machine and want to display the GUI application on your screen directly, you can use X11 forwarding. If you are using Windows or Mac, you should use VNC to access the GUI application.

### Running the container with X11 forwarding enabled

{: .important }
> It only works on Linux. If you are using Windows or Mac, please refer to the next section.

Run the following command to start the Docker container with X11 forwarding:

```bash
docker compose -f compose-x11.yaml up
```

If everything goes well, you should see instructions in the terminal on how to attach to the container. You should keep the `docker compose` running and open a new terminal to attach to the container with the following command:

```bash
docker exec -it smb_container_x11 zsh 
```

{: .note}
> If you are using a different shell, you can replace `zsh` with `bash`, `tmux`, etc.

If you open a GUI application in the container, it should be displayed on your screen.

Once you are finished, you can stop the container by pressing `Ctrl+C` in the terminal where you ran `docker compose up`.

(Optional) You can remove the container by running the following command:

```bash
docker compose -f compose-x11.yaml down
```

### Running the container with VNC enabled

{: .note}
> This method works on all platforms.

Run the following command to start the Docker container with VNC:

```bash
docker compose up
```

You can attach to the container with the following command:

```bash
docker exec -it smb_container zsh
```

{: .note}
> If you are using a different shell, you can replace `zsh` with `bash`, `tmux`, etc.

If you open a GUI application in the container, you can access it by connecting to `localhost:5901` with a VNC client. The password is `robotx`.

Once you are finished, you can stop the container by pressing `Ctrl+C` in the terminal where you ran `docker compose up`.

(Optional) You can remove the container by running the following command:

```bash
docker compose down
```

---

## Open multiple terminals inside the container

When working with ROS, you may need to open multiple terminals to run different commands. You can copy and paste the `docker exec ...` command to multiple terminals and run to open multiple terminals inside the container. As long as the `docker compose up` command is running, you can attach to the same container multiple times. It won't create a new container.

Alternatively, you can use `tmux` to manage multiple terminals in one terminal. For details on how to use `tmux`, please refer to the [official documentation](https://github.com/tmux/tmux/wiki).

---

## Try a GUI application

The default catkin workspace is `/workspaces/rss_workspace`. 

You can try to run the smb gazebo simulation inside the container to see if the GUI application works. 

You can run the following command to start the simulation:

```bash
cd /workspaces/rss_workspace
catkin build smb_gazebo
source devel/setup.zsh
roslaunch smb_gazebo sim.launch
```

If everything goes well, you should see the Gazebo simulation running and the GUI on your screen or VNC viewer.

{: .note}
We highly recommend to read the [`Customizing the Workspace`](./rss-workspace.md#customizing-the-workspace) and [`Tips & Tricks`](./rss-workspace.md#tips-and-tricks) sections in the [RSS workspace](./rss-workspace.md) to learn how to customize your docker environment and boost your coding productivity.

