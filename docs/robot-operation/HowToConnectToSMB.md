---
layout: default
title: Connecting to the SMB
parent: Operating the SMB
nav_order: 1
---

# How to connect to the SMB
{:.no_toc}


* Table of contents
{:toc}

## Connecting to the SMB 

In order to power-up the computer on the SMB use the [Payload Power Switch](images/SMB_Backpanel.png) Close the lid of the switch to prevent shut-down by mistake.
In order to connect to SMB remotely, the host PC should connect the Wifi of the SMB: 
  * Wifi (SSID): smb-<SMB_ROBOT_NUMBER>
  * Password: SMB_<SMB_ROBOT_NUMBER>_RSS or *_RSL

Once you are connected, from the terminal you should connect the SMB via SSH. **The ip addresses of every SMB is 11.0.0.5** .

Note that there might be an error in the host PC while trying to connect the SMB via ssh. Please read the terminal and use the suggested command in terminal to remove the previous ssh connection settings. 
{: .smb-info }

```bash
# In the terminal of host pc
ssh smb@11.0.0.5
# Password: smb

#! Terminal becomes terminal of SSH! 

# To connect the SMB to Internet 
nmcli connection up
```
Once you are connected to the SMB you will see an IP address and port tuple on the terminal starting with 'http://'. Please save it since we will need it in the next step. 

If you do not see such a tupple, please start the roscore and check the part ROS_MASTER_URI.

```bash
# In the terminal of SSH
roscore
# See the part of ROS_MASTER_URI
```


## Visualization Settings

In order to use the visualization tools of ROS, we will set the SMB as ROS master on our local machine:

```bash
# In the terminal of host pc
export ROS_MASTER_URI=http://11.0.0.5:<port>
# the ip and port tuple we have saved in the previous step  
```

Now we can run SMB software and visualize it in the host pc. 

In order to give commands from the host pc to SMB, ROS_IP should be set. 

```bash
# In the terminal of host pc

ifconfig
# See the ip addres of wlp4s0
# It is probably 11.0.0.100

export ROS_IP=<wlp4s0_ip>
# the ip and port tuple we have saved in the previous step  
```

Note that at every new terminal you have to repeat the steps under the title of Running the Software. Please refer to [the NotionsAndDevices document](NotionsAndDevices.md) for more information related to 'export' command.
{: .smb-info }

To use the packages and run the software please refer to the [HowToRunSoftware](core-software/HowToRunSoftware.md)
{: .smb-info }
