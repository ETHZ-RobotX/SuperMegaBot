---
layout: default
title: Frequently Asked Questions
nav_order: 6
---

# Frequently Asked Questions
{ .no-toc}
This page should cover the most frequent question that arise when using the SMB simulation and working on the real robot.

For the recent and past queries please refer to the [Github Issues](https://github.com/ETHZ-RobotX/SuperMegaBot/issues) of this repository.

* Table of contents
{:toc}

## How can I transfer a file to an USB3 drive?

(from <https://askubuntu.com/questions/37767/how-to-access-a-usb-flash-drive-from-the-terminal> )

### Figure out the name of the usb stick
Most likely the device name of the usb stick is called `sda1`, but it could be different. To find the name of the usb drive, execute:
```bash
lsblk
```

### Create a mounting point
Create the folder where the usb will be mounted (essentially a folder linked to the usb). Create the following folder if it does not already exist.
```bash
sudo  mkdir /media/usb
```

### Mount the usb
```bash
sudo mount /dev/sda1 /media/usb
```

### Unmount!
Remember to unmount the usb stick before disconnecting it. Otherwise you may corrupt it!
```bash
sudo umount /media/usb
```
