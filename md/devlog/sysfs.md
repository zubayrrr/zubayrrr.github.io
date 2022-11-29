---
created: 1657956449008
desc: ''
id: b3424uszw3e3l9htw309zer
title: /sys
updated: 1657956749007
---
   
Related::  [linux](../topics/linux.md)   
   
   
---   
   
In addition to /[proc](../devlog/proc.md), the kernel also exports information to another virtual file system called sysfs. sysfs is used by programs such as udev to access device and device driver information. The creation of sysfs helped clean up the proc file system because much of the hardware information has been moved from proc to sysfs.   
   
Procfs and sysfs do the same, but sysfs is newer and a little bit more structured.   
   
The sysfs file system is mounted on /sys. The top-level directories are shown. Following is a brief description of some of these directories:   
   
   
- `/sys/block`   
- `/sys/bus`   
- `/sys/class`   
- `/sys/devices`   
- `/sys/firmware`   
- `/sys/module`   
- `/sys/power`   
   
## The `sysctl` Utility   
   
The sysctl utility can also be used to view or modify values to writable files in the `/proc` `/sys` directory. To view the current kernel settings, enter:   
   
`sysctl -a`   
   
Via - [Understanding The sysfs File System (/sys) in Linux – The Geek Diary](https://www.thegeekdiary.com/understanding-the-sysfs-file-system-in-linux/)