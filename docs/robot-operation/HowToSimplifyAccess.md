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

This section assumes, that you haven't set up multiple key files yet. {: .smb-info }


Instead of typing the password everytime you connect to the robot, you may also copy your public ssh key to the robot. 

In a nutshell, follow the steps below:

```bash
test ! -e ~/.ssh/id_rsa.pub && ssh-keygen  # generate ssh keys if they don't exist yet
ssh-copy-id team2@10.0.1.5   # adjust username and robot IP address!
```

Combined with setting up the robot in `~/.ssh/config` this allows connecting to the robot without the need to type the password. 


More details can be found in the [official documentation of ssh-copy-id](https://www.ssh.com/academy/ssh/copy-id).
