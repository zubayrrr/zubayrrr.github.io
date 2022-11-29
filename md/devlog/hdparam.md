---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: t2nexja55v4h5ha3pnjldmd
title: hdparam
updated: 1652815757381
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
“**hdparm**“(i.e, hard disk parameter) is one of the command line programs for Linux which is used to handle disk devices and hard disks. With the help of this command, you can get statistics about the hard disk, alter writing intervals, acoustic management, and DMA settings. It can also set parameters related to drive caches, sleep mode, power management, acoustic management, and DMA settings.   
   
**Note:** When no flags are specified, `–acdgkmnru` is presumed.   
   
## Examples   
   
**Command to display information of the hard drive:** It is one of the most significant features as it unveils details of the hard disk drive, you need to use -I option and hard disk drive here.   
   
```
hdparm -I /dev/sda
hdparm -i /dev/sda
```
   
   
**Command to display all the options:**   
   
```
hdparm -h
```
   
   
**Command to test hard disk drive speed:**   
   
`--direct` option will bypass the page cache causing the reads to go directly from the drive to the hdparm command buffer; its a raw [input output](../devlog/io.md)   
   
```
hdparm -t /dev/vdb
hdparm -t --direct /dev/sda
```
   
   
**Command to measure hard disk cache read speed:**   
   
```
hdparm -T /dev/vdb
```
