---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: 5euazqrat5ldhoospe3xh87
title: lsusb
updated: 1652815757445
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**lsusb** is a utility for displaying information about USB buses in the system and the devices connected to them.   
   
To make use of all the features of this program, you need to have a Linux kernel which supports the /proc/bus/usb interface (e.g., Linux kernel 2.3.15 or newer).   
   
## Examples   
   
`-v` : This option is used to display the output in verbose mode and also display detailed information about the devices connected.   
   
```
lsusb -v
```
   
   
`-s` : This option is used to display the only device specified by the bus and/or device number.   
   
```
lsusb -s 2:4
```
   
   
`-t` : This option is used to dump the physical USB device hierarchy as a tree.   
   
```
lsusb -t
```
   
   
`-D` : This option is used to display information about the specified device file. The device file should be like `/dev/usb/002/004`.   
   
```
lsusb -D /dev/bus/usb/002/004
```
   
   
> via — [lsusb command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/lsusb-command-in-linux-with-examples/)