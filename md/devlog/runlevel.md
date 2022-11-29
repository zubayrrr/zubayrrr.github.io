---
created: 1657955532345
desc: ''
id: dhsgcsibsmvtuotgamzjcj1
title: Runlevel
updated: 1657955882336
---
   
Related::  [linux](../topics/linux.md)   
   
   
---   
   
A runlevel is one of the modes that a Unix-based, dedicated server or a VPS server OS will run on. Each runlevel has a certain number of services stopped or started, giving the user control over the behavior of the machine. Conventionally, seven runlevels exist, numbered from zero to six.   
   
After the Linux kernel has booted, the init program reads the /etc/inittab file to determine the behavior for each runlevel. Unless the user specifies another value as a kernel boot parameter, the system will attempt to enter (start) the default runlevel.   
   
Most Linux servers lack a graphical user interface and therefore start in runlevel 3. Servers with a GUI and desktop Unix systems start runlevel 5. When a server is issued a reboot command, it enters runlevel 6.   
   
The important thing to note here is that there are differences in the runlevels according to the operating system. The standard LINUX kernel supports these seven different runlevels :   
   
| Run Level | Mode                            | Action                                                                         |   
| --------- | ------------------------------- | ------------------------------------------------------------------------------ |   
| 0         | Halt                            | Shuts down system                                                              |   
| 1         | Single-User Mode                | Does not configure network interfaces, start daemons, or allow non-root logins |   
| 2         | Multi-User Mode  with no NFS(network file system)                | Does not configure network interfaces or start daemons.                        |   
| 3         | Multi-User Mode with Networking  under the command line interface and not under the graphical user interface. | Starts the system normally.                                                    |   
| 4         | Undefined                   | Not used/User-definable                                                        |   
| 5         | X11                             | As runlevel 3 + display manager(X)   With GUI (graphical user interface) and this is the standard runlevel for most of the LINUX based systems.                                           |   
| 6         | Reboot                          | Reboots the system                                                             |   
   
   
Sources:   
   
   
- [Linux Runlevels Explained | Liquid Web](https://www.liquidweb.com/kb/linux-runlevels-explained/),   
- [Run Levels in Linux - GeeksforGeeks](https://www.geeksforgeeks.org/run-levels-linux/)