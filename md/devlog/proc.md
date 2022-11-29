---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: 4cmnu8nf5qp9o17i5ecn6xx
title: /proc
updated: 1657956449313
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Proc file system (procfs) is virtual file system created on fly when system boots and is dissolved at time of system shut down.   
   
It contains useful information about the processes that are currently running, it is regarded as control and information center for kernel.   
   
The proc file system also provides communication medium between kernel space and user space.   
   
The **/proc** directory is present on all **Linux** systems, regardless of flavor or architecture.   
   
**/proc** directory is **NOT** a real **File System**, in the sense of the term. It is a **Virtual File System**. Contained within the **procfs** are information about processes and other system information. It is mapped to **/proc** and mounted at **boot** time.   
   
## Examples   
   
```
ls -l /proc
```
   
   
```
cat /proc/meminfo
```
   
   
```
# directories only
ls -l /proc | grep '^d'
```
   
   
[process](../devlog/process.md)es have entries created in the /proc file system with their PIDs   
   
```
ps -aux
```
   
   
```
ls -ltr /proc/7494
```
   
   
> — via [proc file system in Linux - GeeksforGeeks](https://www.geeksforgeeks.org/proc-file-system-linux/)   
> — via [Exploring /proc File System in Linux](https://www.tecmint.com/exploring-proc-file-system-in-linux/)   
   
See also: [sysfs](../devlog/sysfs.md)