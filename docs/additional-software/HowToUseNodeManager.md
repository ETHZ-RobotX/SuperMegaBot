---
layout: default
title: Node Manager
parent: Additional Software
---

# How to use fkie_node_manager for the SMB?
This documentation explains the basic steps about how to run node manager for the SMB.
{: .smb-info }

## Preliminary steps
1. The detailed instructions how to install the Node Manager can be found in the [multimaster_fkie repository](https://github.com/ETHZ-RobotX/multimaster_fkie). Please clone the repository within your SMB workspace.
  ```bash
  pip3 install ruamel.yaml
  ```
2. Connect your host machine to the proper WiFi network.
3. In your local machine add the hostname of the SMB.
  - on ssh console window run: `hostname` and `hostname -I` to get the address and name of the SMB to which you are connected
  - on your host machine, run `sudo nano /etc/hosts` and add the address with SMB hostname obtained within the previous step as depicted on the image below

## Establish a connection between host and SMB
1. On your local machine, in the console window, execute `hostname -I` to get an IP address. If multiple IP addresses are present, take the first one.

2. In the same console window, run:
```bash
export ROS_IP=#IP address of your host machine
```
after sourcing your workspace execute:
```bash
node_manager
```
3. Click on the Start button, set only the MCast Group to `224.0.0.1`, and without introducing any other changes press OK.
4. Start the synchronization node by pressing the button next to the available ROS Network in the upper left part of the Node Manager window.
5. Again, click Start, but now change the Host to the hostname of the SMB e.g. for SMB264 `10.0.4.5`, the MCast Group to `224.0.0.1`, and press OK. The SMB ROS Network should appear in the upper left corner of the Node Manager window, just below the localhost network.

## Launch files
In the panel below the ROS Network, you can search for launch files that can be started either on SMB or on your host machine. By selecting the appropriate launch file, in order to load it press the Load button in the lower part of this panel. After successfully loading the launch file the associated node should appear in the main panel.

### Start ROS node
Select a ROS node, which needs to be run, and use the green play button on the left side to start the node.

### Kill ROS node
In order to kill the node, select it and press the green stop button which is below the previously mentioned play button.

### Console for a single ROS node
If the node has been successfully launched, you can inspect it via the console output by pressing the console symbol or by pressing F3

### Editing launch file
To inspect and edit the launch file corresponding to the node of interest, select the node and press F4.

## Synchronization of both ROS masters
Node Manager synchronizes all the ROS topics and ROS services, but unfortunately not ROS parameters. To share the ROS parameters between both masters, go to the Parameter tab and load all parameters (symbol with small blue arrow). Then select which parameters need to be shared and export them to the second ROS Master by pressing the big blue arrow pointing to the right.

# Troubleshooting
  - If you are connected via VPN, the multicasting route needs to  be set manually. In the ssh console window execute:
    `sudo route add -net 224.0.0.0 netmask 255.255.255.0 dev zthnhbsdox`
  - You get an exception on access the remote host: Exception: ssh connection to REMOTE_HOST failed: not a valid RSA private key file. Generate an SSH key file with e.g. `ssh-keygen -p -m PEM -f ~/.ssh/id_rsa`
  - Before starting the node manager make sure that no processes are running in the detached mode, i.e. execute `screen -ls`. You should get a similar output to the following one:
    ```bash
    76259._roscore--11311	(21.06.2021 17:22:32)	(Detached)
    ```

    To kill such a process execute `kill 76259`.
