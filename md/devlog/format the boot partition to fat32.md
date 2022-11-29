---
created: 20211101191427820
desc: ''
id: r08bzdg34axuhyu8ljpt4r8
tags:
- tidbits
title: Format the boot partition to FAT32
updated: 1652815757263
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`sudo mkfs.vfat -F32 /dev/sdb1` make sure to change `/dev/sdb1` to the appropriate disk name