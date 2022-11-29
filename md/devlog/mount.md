---
created: '2022-05-14T00:00:00.000Z'
desc: ''
id: 9x9tnilgrp5wqa10f8odw8x
title: mount
updated: 1653305994057
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
All files in a **Linux** filesystem are arranged in form of a big tree rooted at ‘**/**‘.These files can be spread out on various devices based on your partition table, initially your parent directory is mounted(i.e attached) to this tree at ‘**/**‘, others can be mounted manually using GUI interface(if available) or using **mount** command.   
   
If you want to access a filesystem that is on another partition or disk - you’ll need to mount it or logically attach it to an existing directory of your Unix/Linux filesystem. This directory is called as mount point.   
   
```
mount -t type device dir
```
   
   
The commands tells the **Kernel** to attach the filesystem found at **device** to the **dir**.   
   
   
- If you leave the **dir** part of syntax it looks for a **mount point** in **/etc/fstab**.   
- You can use **–source** or **–target** to avoid ambivalent interpretation.   
   
  `mount --target /mountpoint`   
   
   
- **/etc/fstab** usually contains information about which device is need to be mounted where.   
- Most of the devices are indicated by files like **/dev/sda4**, etc. But it can be different for certain filesystems.   
   
**Some Important Options:**   
   
   
- **l** : Lists all the filesystems mounted yet.   
- **h** : Displays options for command.   
- **V** : Displays the version information.   
- **a** : Mounts all devices described at **/etc/fstab**.   
- **t** : Type of filesystem device uses.   
- **T** : Describes an alternative fstab file.   
- **r** : Read-only mode mounted.   
   
## Examples   
   
Running `mount` without any options will show all the currently attached filesystems along with virtual file systems such as [sysfs](../devlog/sysfs.md), [tmpfs](/not_created.md), [proc](../devlog/proc.md) and so on.   
   
Display all partitions of a specific filesystem type   
   
```
mount -l -t ext4
```
   
   
Storage drives are represented on the system as files in the `/dev` directory. Typically, files representing storage devices start with `sd` or `hd` followed by a letter. For instance, the first drive on a server is usually something like `/dev/sda`.   
   
Partitions on these drives also have files within `/dev`, represented by appending the partition number to the end of the drive name. For example, the first partition on the drive from the previous example would be `/dev/sda1`.   
   
Most times disks like USB drives are mounted automatically, if you want to mount it manually for various reasons such with different options or at a different mount point(other than `/media`)   
   
   
- Use [fdisk](../devlog/fdisk.md) to find the name of the device file.   
- Use [dmesg](../devlog/dmesg.md) to find the name of the device.   
- You can also use [lsblk](../devlog/lsblk.md) to find all block devices.   
   
```
sudo fdisk -l
dmesg
```
   
   
Once you have the name of the device, you can mount it on any dir that already exists.   
   
```
mkdir /home/user/Desktop/usb
sudo mount /dev/sdb /home/user/Desktop/usb
```
   
   
You can mount the same physical device on multiple mount points.   
   
Mount usually automatically recognises the filesystem type but if it fails you can explicitly specify it using `-t` option.   
   
```
sudo mount -t vfat /dev/sdb /home/user/Desktop/usb
```
   
   
Use [umount](../devlog/umount.md) to un-mount a mounted device.   
   
```
sudo umount /home/user/Desktop/usb
```
   
   
`-o` for additional options   
   
Mount in Read-Only mode   
   
```
sudo mount -o ro /dev/sdb /home/user/Destop/usb
```
   
   
To remount with other options or Write permissions   
   
```
sudo mount -o rw,remount /dev/sdb /home/user/Destop/usb
```
   
   
## Mounting an ISO file   
   
Start by creating a mount point   
   
```
mkdir ~/iso-mount
```
   
   
Mount ISO using mount command   
   
```
sudo mount /path_to_iso_file /home/user/iso-mount -o loop
```
   
   
See also: [gparted](../devlog/gparted.md)