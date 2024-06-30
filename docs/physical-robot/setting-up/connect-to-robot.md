---
layout: default
title: Connect to Robot
parent: Setting Up
grand_parent: Physical Robot
nav_order: 2
has_toc: false
---

# Connect to SMB Physical Robot
{:.no_toc}

In the following, the basic usage of the SMB payload is described.

* Table of contents
{:toc}

## Powering up the payload
The SMB payload can be powered by either the SMB payload power supply or a payload battery. You can also plug several power sources (e.g. power supply and battery). While the payload power supply is plugged, the battery will not be discharged but also not charged. Once the power supply is disconnected, the system automatically switches over to the first battery (as long as it it charged enough) and subsequently to the second battery.

### Connecting the Battery
Please be sure that you are well informed about the type of the battery you are using. Read the safety document and do not hesitate to ask for help if you are not sure about something!
{: .warning }

While placing the battery into its drawer, visually verify that the wires are not twisted, sheared or wedged into something!
{: .warning }

If you notice or suspect even a small amount of expansion on the battery, inform your supervisor!
{: .warning }

Do not cut the wires!
{: .warning }

Be sure that wire tips are connected to the right way as the color of connected tips should be same! 
{: .warning }

Li-Ion batteries are affected by the same problems as other lithium based batteries. This means that overcharge, over-discharge, over-temperature, short circuit, crush and nail penetration may all result in a catastrophic failure, including the pouch rupturing, the electrolyte leaking, and fire.
{: .warning }

### Turning on the SMB payload
In order to power-up the computer on the SMB use the [Payload Power Switch](../images/SMB_Backpanel.png). Close the lid of the switch to prevent shut-down by mistake.

## Connecting to the SMB 

### Remark
In the document there are two terminal types:

1. Terminal of host PC: The terminal that has access to host pc system.
   
2. Terminal of SSH: The terminal that has SSH connection to the SMB, therefore has access to the SMB system.

### Connect to the SMB network
In order to connect to SMB, you can either use the Wifi of the SMB or connect using a ethernet cable.

Use the following details of the wireless network of the SMB: 
  * Wifi (SSID): SMB_26x
  * Password: SMB_26x_RSS
  
*where x is the last digit of SMB Robot Number*


Once you are connected, from the terminal you should connect the SMB via SSH. 

**The ip addresses of every SMB is 10.0.x.5 where x is the last digit of SMB Robot Number**.
*Example: For SMB 263 the on-board computer IP address is 10.0.3.5*
{: .note }

Note that there might be an error in the host PC while trying to connect the SMB via ssh. Please read the terminal and use the suggested command in terminal to remove the previous ssh connection settings. 
{: .note }

```bash
# In the terminal of host pc
# Do not forget to change x and <user>
ssh <user>@10.0.x.5
# Password: <password>
```

**You should connect to the SMB with your given username. The Username is your team number**.
*Example: For team 1, the username is team1*
{: .note }


Once you are connected to the SMB you will see an IP address and port tuple on the terminal starting with `http://`. Please save it since we will need it in the next step. 

If you do not see such a tupple, please start the roscore and check the part `ROS_MASTER_URI`.

```bash
# In the terminal of SSH
roscore
# See the part of ROS_MASTER_URI
```

#### Network Sharing

Whenever the 4G connection is not working well, you can connect the SMB NUC to another Wi-Fi using,

```bash
#! Terminal becomes terminal of SSH! 

# To view connections available, this shows the list of connections available to join
nmcli connection show

# To connect the SMB to Internet (you can specify the connections available from above command, e.g: sudo nmcli connection up mavt-asl-iot)
sudo nmcli connection up
```

If by any case the 4G network is not working and you are connected to internet using `nmcli connection up`, you may want to share the internet with jetson and your personal computer connected to WiFi.

Sharing with the Jetson,
```bash
# in the SMB
./ics_gpu.sh
```

Sharing with the PC,
```bash
# in the SMB
./ics_gpu.sh

# in the Host
## in Ubuntu
sudo route add default 10.0.x.5 # replace x with SMB26X if it's 263 X is 3
sudo systemd-resolve --set-dns=10.0.x.1 --set-dns=8.8.8.8 --interface=eth0 # use your network interface, e.g: eth0

## in Mac
sudo route delete default
sudo route add default 10.0.x.5 # replace x with SMB26X if it's 263 X is 3
sudo networksetup -setdnsservers Wi-Fi 10.0.x.1 8.8.8.8 # use your network interface, e.g: Wi-Fi, to list all networks use `networksetup -listallhardwareports`
```

## Visualization Settings

In order to use the visualization tools of ROS, we will set the SMB as ROS master on our local machine:

```bash
# In the terminal of host pc. 
export ROS_MASTER_URI=http://10.0.x.5:<port>
# the ip and port tuple we have saved in the previous step  
```

Now we can run SMB software and visualize it in the host pc. 

In order to give commands from the host pc to SMB, ROS_IP should be set. 

```bash
# In the terminal of host pc

ifconfig
# See the ip addres of wlp4s0
# It is probably 10.0.x.100

export ROS_IP=<wlp4s0_ip>
# the ip and port tuple we have saved in the previous step  
```

Note that at every new terminal you have to repeat the steps under the title of Running the Software. Please refer to [the Notions and Devices document](../NotionsAndDevices.md) for more information related to 'export' command.
{: .note }

To use the packages and run the software please refer to the [How to Run Software](../core-software/HowToRunSoftware.md)
{: .note }


## How to establish the VPN connection? (Optional)

This documentation explains the basic steps about how to connect your host machine to the SMB via VPN connection. We use ZeroTier to connect to the robots via 4G. This is necessary if we operate the robots outside the range of the built-in wifi routers.
The following instructions will contain the configurations for SMB264.

### Installation

On the user PC, install zero tier client:

```bash
# In the host pc
curl -s https://install.zerotier.com | sudo bash
```

### Usage

#### List all networks

Execute
```bash
sudo zerotier-cli listnetworks
```
to get the list of the networks, to which you are connected. Make sure that you are connected only to the network which corresponds to SMB on which you are working. Sample output for SMB264:

```bash
200 listnetworks <nwid> <name> <mac> <status> <type> <dev> <ZT assigned ips>
200 listnetworks aaaaaaaaaaaaaaaa SMB264 00:00:00:00:00:ad OK PUBLIC zthnhbsdox 00.000.00.00/00
```

#### Join the network
To work on the robot you need to join the desired network using a network ID. The network ID address will be provided to you by the assistants. To join the network with the ID `aaaaaaaaaaaaaaaa`, run:
```bash
sudo zerotier-cli join aaaaaaaaaaaaaaaa
```
Use `listnetworks` command from above to check if you have successfully connected to the desired network.


#### Connect to the SMB
To enter the SMB just `ssh` into it as described in the [Connecting to the SMB](HowToConnectToSMB.md) section. Please, make sure that you are not connected to the local SMB network.

#### Leave the network
Since all robots use the same IP range, the user must make sure that only one zerotier interface is active at a time for the forwarding to work properly. Use:
```bash
sudo zerotier-cli leave aaaaaaaaaaaaaaaa
```
to disconnect from a SMB network when you are not using it.

### Known Issues
If the robot is not connected to the internet but your computer is in the zerotier network you cannot ssh into the robot computer even if you are connected to the local wifi. This is because it tries to route the traffic to 10.0.0.0/24 through the zerotier network to which the robot computer is not connected. As a workaround, either leave the zerotier network or delete the route on your computer locally.
