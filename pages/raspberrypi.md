---
layout: page
title: Raspberrypi
categories: [raspberrypi]
tags: [raspberrypi, computers]
type: page
---


# Commands

```bash
# Find out which Raspberry Model you are using
cat /proc/device-tree/model
```

# Setup
## Raspberry Pi OS

The image for both Raspberry Pi 2 Model B and Raspberry Pi 3 are same

Download the Lite image version from 

[https://www.raspberrypi.org/downloads/raspberry-pi-os/](https://www.raspberrypi.org/downloads/raspberry-pi-os/)

### Install using mac

Reference
[https://www.instructables.com/id/How-to-Install-and-configure-Raspbian-on-Raspberry/](https://www.instructables.com/id/How-to-Install-and-configure-Raspbian-on-Raspberry/)
[https://www.raspberrypi.org/documentation/installation/installing-images/mac.md](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)

```bash
diskutil list
diskutil unmount /dev/disk2s1
diskutil list
df -h
sudo diskutil eraseDisk FAT32 RASPBIAN MBRFormat /dev/disk2
diskutil unmount /dev/disk2s1
diskutil unmountDisk /dev/disk2
sudo dd bs=1m if=~/Downloads/2020-02-13-raspbian-buster.img of=/dev/rdisk2 conv=sync
sudo diskutil eject /dev/rdisk2
diskutil unmountDisk /dev/rdisk2
```








