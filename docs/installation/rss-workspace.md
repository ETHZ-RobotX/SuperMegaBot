---
layout: default
title: RSS Workspace
parent: Installation
nav_order: 1
---

# 🛠️ RSS Workspace
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

{: .important }
Please [create an issue](https://github.com/ETHZ-RobotX/rss_workspace/issues) for any missing library, package, driver, error, or any kind of unclear instruction related to the RSS Workspace.

The **RSS Workspace** is built to provide an out-of-the-box working environment for simulation tasks and connecting with the SMB Physical Robot. It leverages [Docker](https://www.docker.com/), [VSCode Dev Containers](https://code.visualstudio.com/docs/remote/containers) to provide a consistent and reproducible development environment across different platforms.

This has been tested on the following platforms:
- ✅ Ubuntu 22.04/20.04 AMD64
- ✅ Windows 11 AMD64
- ✅ MacOS Sonoma AMD64 and ARM64 (Apple Silicon)

For other Linux distros, the steps should be similar to Ubuntu and work for both AMD64 and ARM64 architectures. For Windows 10, the steps should be similar to Windows 11. The same applies to different versions of MacOS.

---

## 📋 Prerequisites

### Git
Make sure you have installed Git on your system. ([Instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git))

### VSCode
Ensure you have a working VSCode setup and that it is up to date to avoid any issues.

[How to set up VSCode?](https://code.visualstudio.com/learn/get-started/basics)

### Install other requirements
Follow the [preparation steps](https://github.com/ETHZ-RobotX/rss_workspace#preparation) to install the necessary requirements for the RSS Workspace.

### **(Optional)** Fork the repository
If you want to customize your workspace and save your changes, you can fork the repository to your GitHub account and clone the forked repository.

---

## ⚙️ Open workspace locally

### **Method 1**: Clone the workspace to your local file system and open it in VScode.

{: .note }
The Dev Containers extension uses "bind mounts" to source code in your local filesystem by default. While this is the simplest option, on macOS and Windows, you may encounter slower disk performance when using `catkin build` or other disk-intensive operations. If you encounter this issue, consider using Method 2.

##### Clone the workspace

```bash
# replace the URL with your forked repository if you have forked it
git clone https://github.com/ETHZ-RobotX/rss_workspace.git  

# Open the workspace in VScode. You can also open the folder in VScode manually.
code rss_workspace 
```

##### Reopen workspace in dev container
Press `Ctrl+Shift+P` or `F1` to open the command palette, type `Reopen in Container` and select the command to reopen the workspace in a Dev Container.

### **Method 2**: Clone the workspace to a docker volume and open it in VScode. 

[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/ETHZ-RobotX/rss_workspace)

#### **TL;DR**: 
Click the badge above or [here](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/ETHZ-RobotX/rss_workspace) to open the workspace in a Dev Container. If the link does not work, follow the detailed steps below.

{: .note}
This method will clone the workspace to a docker volume. File data will be chunked and managed by Docker. Though, the chunked data are stored in the local file system, you cannot access them directly. This may be useful if you want to keep your local file system clean or if you encounter performance issues when using the workspace on macOS or Windows. To know more about the docker volume, please refer to the [Docker documentation](https://docs.docker.com/storage/volumes/).

#### **Detailed Steps:**

In VSCode,
1. Open the Command Palette by pressing `F1`.
2. Copy the following link or the forked repository link to the clipboard `https://github.com/ETHZ-RobotX/rss_workspace.git`.
3. Search for _"clone"_ and select **Dev Containers: Clone Repository in Container Volume**.
4. Paste the copied link into the box and press enter.
5. The dev container will set up properly. (This might take some time as it pulls base docker images and builds locally. You can click `Starting Dev Container (show log)` at the bottom right to see the progress.)

---

## 🛠️ (Optional) Building the SMB Catkin Workspace
You can build all packages at once by running

```bash
catkin build
```

or build a specific package when needed by running

```bash
catkin build <package_name>
```

{: .warning }
> Be cautious, `catkin build` compiles files in parallel, which may quickly eat up your memory and CPU resource. We provide a shell alias `build-limit` to limit the number of parallel jobs and memory usage defined as follows:
>
> ```bash
> alias build-limit="catkin build --jobs 8 --mem-limit 70%"
> ```

{: .note}
`build-limit` and `catkin build` can be used interchangeably.

---

## 🖥️ Using the Terminal

### Integrated Terminal
We use `zsh` by default in the integrated terminal. You can set up your shell preferences in `.vscode/settings.json` or click the dropdown button in the terminal to select the default shell profile.

<img src="{{ 'images/terminal_dropdown.png' | absolute_url }}" alt="Terminal Dropdown" width="100%"/>

Every terminal opened inside VSCode sources the system ROS setup file by default. To source the RSS catkin workspace setup file in newly opened terminals, we provide a shell alias `wssetup` defined as follows:

```bash
alias wssetup="source ${ROOT}/devel/setup.zsh"
```

where `${ROOT}` is a pre-defined variable pointing to the workspace root directory inside the container. You can simply use `wssetup` to source the workspace in the terminal.

### Multiple Terminals with tmux
When working with ROS, it is often useful to have multiple terminals open. We provide a pre-configured tmux session with multiple panes. You can start the tmux session by clicking the dropdown button in the terminal and selecting `smb-tmux`.

<img src="{{ 'images/smb_tmux.png' | absolute_url }}" alt="Terminal Dropdown" width="100%"/>

{: .note}
`smb-tmux` runs `scripts/start_smb_tmux.sh` to start the tmux session under the hood. We highly recommend modifying the script to suit your needs. When remote accessing the the physical robots, you can copy the script to the physical robot and run it to have a similar tmux session.

---

## 👣 Additional Steps

### Windows Users

In each terminal, you have to manually set the `ROS_HOSTNAME`.

```bash
export ROS_HOSTNAME=localhost
```

---

## 🖼️ Visualizing GUI 

### Using X11 forwarding

{: .important}
**Works only on Linux**


This works out of the box in Linux; when a GUI is launched, the window pops up.

{: .note}
> Please note that this might have some rendering issues when the windows are resized, especially in RViz.

### Using VNC (remote desktop) (Recommended for Windows/Mac)

{: .important}
Works on Linux, Windows, and Mac

Modify the [line](https://github.com/ETHZ-RobotX/rss_workspace/blob/5db953b27bb6c1ca603944d1345371c666ad93af/.devcontainer/devcontainer.json#L20) in the `.devcontainer/devcontainer.json` to

```json
"DISPLAY": ":1"
```
and rebuild the workspace by opening the command palette (`Ctrl+Shift+P`) and selecting `Remote-Containers: Rebuild Container`.

**How to open the VNC viewer?**

Open the following link [(http://localhost:6080/)](http://localhost:6080/) in the browser to connect with the VNC environment. Click the connect button to open the viewer. (password: `robotx`)

Check whether everything is working by opening RViz:

```bash
# In VSCode terminal (Terminal->New Terminal)
# wssetup    # Source the workspace setup file if not sourced
roslaunch smb_gazebo sim.launch
```

### Using VNC Viewer

{: .important}
Works on Linux, Windows, and Mac

1. Install the Real VNC Viewer following the steps on the [RealVNC website](https://www.realvnc.com/en/connect/download/viewer/).
2. Open the RealVNC Viewer.
3. File -> New Connection.
4. Add `localhost:5901` as the VNC Server.
5. Click Ok.
6. Click and open the new connection.
7. Ignore the unencrypted connection issue.

Now you can see the GUI desktop similar to noVNC.

Check whether everything is working by opening RViz:

```bash
# In VSCode terminal (Terminal->New Terminal)
# wssetup    # Source the workspace setup file if not sourced
roslaunch smb_gazebo sim.launch
```

---

## 🎨 Customizing the Workspace

{: .important}
To save your customization, you should fork the repository and clone the forked repository. You can then customize the workspace as needed and push the changes to your forked repository.

{: .note}
You can take a look of the following files and get an idea of what aliases/tools are pre-configured to make your life easier.

* Add additional packages and productivity tools (e.g., `autojump`, `htop`, etc.) in the `.devcontainer/Dockerfile`.
* Add additional features and vscode extensions in the `.devcontainer/devcontainer.json`.
* Add additional shell aliases and functions in the `.devcontainer/setup_alias.sh`.
* Add additional tmux configurations in the `.tmux.conf`.
* Customize you tmux session in the `scripts/start_smb_tmux.sh`.

---

## 💡 Tips & Tricks

### [Tmux](https://github.com/tmux/tmux/wiki) 

#### _Use tmux in the workspace and remote access the physical robot via SSH_
Tmux is a terminal multiplexer; it allows you to create several "pseudo terminals" from a single terminal. It decouples the terminal from the main program (SSH at the remote), protecting it from being closed accidentally when connection is lost. It is particularly useful when remote accessing the physical robot via SSH, as it allows you to keep the program running even when the connection is lost and provides a multi-pane terminal interface for better organization.

#### _Tmux mouse mode_
We enable tmux mouse mode by default. You can use the mouse to switch between panes and scroll up and down in the terminal.

#### _Tmux panes synchronization_
You can toggle pane synchronization mode by pressing `Ctrl+b` and `Ctrl+s`. It is useful when you want to type the same command in multiple panes.

### GUI

#### _GUI Screen is oversized?_
On the left menu,
Go to settings -> scaling mode -> try with local scaling/remote resizing

#### _Windows spawn oversized?_
Right-click on the window title bar -> Maximize (this will fit the window into the screen size)

#### _VNC default resolution is too small?_
Modify build arguments `VNC_RESOLUTION` in the `.devcontainer/devcontainer.json` file and rebuild the workspace.