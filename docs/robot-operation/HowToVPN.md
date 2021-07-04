---
layout: default
title: How to VPN
parent: Operating the SMB
nav_order: 5
---

# How to establish the VPN connection?
{: .no_toc}

This documentation explains the basic steps about how to connect your host machine to the SMB via VPN connection. We use ZeroTier to connect to the robots via 4G. This is necessary if we operate the robots outside the range of the built-in wifi routers.
The following instructions will contain the configurations for SMB264.

## Installation

On the user PC, install zero tier client:

```bash
# In the host pc
curl -s https://install.zerotier.com | sudo bash
```

## Usage

### List all networks

Execute
```bash
sudo zerotier-cli listnetworks
```
to get the list of the networks, to which you are connected. Make sure that you are connected only to the network which corresponds to SMB on which you are working. Sample output for SMB264:

```bash
200 listnetworks <nwid> <name> <mac> <status> <type> <dev> <ZT assigned ips>
200 listnetworks aaaaaaaaaaaaaaaa SMB264 00:00:00:00:00:ad OK PUBLIC zthnhbsdox 00.000.00.00/00
```

### Join the network
To work on the robot you need to join the desired network of the given IP address. The IP address will be provided to you by the assistants. Joining the network with the ID `aaaaaaaaaaaaaaaa`, run:
```bash
sudo zerotier-cli join aaaaaaaaaaaaaaaa
```
Use `listnetworks` command from above to check if you have successfully connected to the desired network.


### Connect to the SMB
To enter the SMB just `ssh` into it as described in the [Connecting to the SMB](HowToConnectToSMB.md) section. Please, make sure that you are not connected to the local SMB network.

### Leave the network
Since all robots use the same IP range, the user must make sure that only one zerotier interface is active at a time for the forwarding to work properly. Use:
```bash
sudo zerotier-cli leave aaaaaaaaaaaaaaaa
```
to disconnect from a SMB network when you are not using it.

## Known Issues
If the robot is not connected to the internet but your computer is in the zerotier network you cannot ssh into the robot computer even if you are connected to the local wifi. This is because it tries to route the traffic to 10.0.0.0/24 through the zerotier network to which the robot computer is not connected. As a workaround, either leave the zerotier network or delete the route on your computer locally.
