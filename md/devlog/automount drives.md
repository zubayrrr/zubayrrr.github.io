---
created: 20211115135749864
desc: ''
id: 95cux82u98rigb8qiope5uj
tags:
- tidbits
title: Automount drives
updated: 1652815757509
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
### Locate the partition to mount   
   
`sudo fdisk -l`   
   
### Locate the UUID   
   
`sudo blkid`   
   
### Create a mount point   
   
    sudo mkdir /data   
    sudo groupadd data   
    sudo usermod -aG data USERNAME (Where USERNAME is the name of the user to be added)   
   
    sudo chown -R :data /data   
   
### Automount entrypoint   
   
`sudo nano /etc/fstab`   
`UUID=14D82C19D82BF81E /data auto nosuid,nodev,nofail,x-gvfs-show 0 0`   
   
### Testing   
   
`sudo mount -a`   
   
if fails do `sudo reboot`   
   
[Source](https://www.techrepublic.com/article/how-to-properly-automount-a-drive-in-ubuntu-linux/)