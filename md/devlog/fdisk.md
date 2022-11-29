---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: i84env82kxcly9udsbwt1t6
title: fdisk
updated: 1652815757689
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`fdisk` is a menu-driven command-line utility that allows you to create and manipulate partition tables on a hard disk.   
   
## Examples   
   
To list the `/dev/sda` partition table and partitions you would run:   
   
```
fdisk -l /dev/sda
```
   
   
When no device is given as an argument, `fdisk` will print partition tables of all devices listed in the `/proc/partitions` file:   
   
```
fdisk -l
```
   
   
> via — [Fdisk Command in Linux (Create Disk Partitions) | Linuxize](https://linuxize.com/post/fdisk-command-in-linux/)