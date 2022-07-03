---
layout: default
title: How to simplify access
parent: Operating the SMB
nav_order: 6
nav_exclude: false
---

# How to simplify access to SMB
{: .no_toc}

When connecting to a remote computer using ssh, you can simplify the process by the following hints.

## Setup ~/.ssh/config
If it doesn't exist yet, create the file `~/.ssh/config` and add the following lines (remember to adjust them to your needs).

```
Host smb-263
  Hostname 10.0.3.5
  User team5
```

You may now connect as user team5 to smb-263 on `10.0.3.5` by just executing `ssh smb-263`. 

## SSH Public Key Authentication

This section assumes, that you haven't set up multiple key files yet.
{: .smb-info }

Instead of typing the password everytime you connect to the robot, you may also copy your public ssh key to the robot. 

In a nutshell, follow the steps below:

```bash
test ! -e ~/.ssh/id_rsa.pub && ssh-keygen  # generate ssh keys if they don't exist yet
ssh-copy-id team2@10.0.1.5   # adjust username and robot IP address!
```

Combined with setting up the robot in `~/.ssh/config` this allows connecting to the robot without the need to type the password. 

More details can be found in the [official documentation of ssh-copy-id](https://www.ssh.com/academy/ssh/copy-id).

## Setting ROS_MASTER_URI and ROS_IP
Setting the environment variables `ROS_MASTER_URI` and `ROS_IP` properly is the best strategy to avoid any communication issues in the ROS network. 

A convinient way to set the variables is to adjust the following code to match your robot and add it to the file `~/.bash_aliases` (or `~/.bashrc`):
```bash
alias connect-smb261='export ROS_MASTER_URI=http://10.0.1.5:11311 ; 
export ROS_IP=`ip route get 10.0.1.5 | awk '"'"'{print $5; exit}'"'"'` ; 
echo "ROS_MASTER_URI and ROS_IP set to " ; 
printenv ROS_MASTER_URI ; 
printenv ROS_IP'
```

Then (for any newly openend terminal), you can execute `connect-smb261` to set the correct environment variables for your robot.
