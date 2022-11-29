---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: b97p1rha3zv9gm49n6ieom7
title: lsblk
updated: 1652815757533
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**Lsblk** is used to display details about block devices and these block devices(Except ram disk) are basically those files that represent devices connected to the pc. It queries **/sys** virtual file system and **udev db** to obtain information that it displays. And it basically displays output in a tree-like structure. This command comes pre-installed with the util-Linux package.   
   
## Examples   
   
To display block devices.   
   
```
lsblk
```
   
   
To display empty block devices as well.   
   
```
lsblk -a
```
   
   
To print size information in bytes.   
   
```
lsblk -b
```
   
   
> via — [lsblk Command in Linux with Examples - GeeksforGeeks](https://www.geeksforgeeks.org/lsblk-command-in-linux-with-examples/)