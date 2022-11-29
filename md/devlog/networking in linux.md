---
created: 20211029071020310
desc: ''
id: ck6ds17ovyjf6n0sidmat7v
title: Networking in Linux
updated: 1656322630487
---
   
Topics::  [linux](../topics/linux.md), [networking](../topics/networking.md)   
   
   
---   
   
   
- Getting Information about the Network Interfaces   
  - [ifconfig](../devlog/ifconfig.md), [ip](../devlog/ip.md)   
  - `lo` stands for loopback (inteface)   
  - [enp0s3](../devlog/enp0s3.md) for the [Ethernet](../devlog/ethernet.md) interface   
  - There are other names for interfaces such as [wlo1](/not_created.md) , [wlan0](../devlog/wlan0.md) for wireless interface.   
- When configuring network intefaces using [ip](../devlog/ip.md), [ipconfig](/not_created.md), [route](../devlog/route.md) you must run them as root([sudo](../devlog/sudo.md))   
- Network inteface configuration set by [ifconfig](../devlog/ifconfig.md) or [ip](../devlog/ip.md) are not persistent, after a system restart all the changes are lost. To make them persist, we need to edit distro specifc configuration file. For example on Ubuntu you have to use [netplan](../devlog/netplan.md), [systemd-networkd](../devlog/systemd-networkd.md) for static configuration of the network.   
- Network Troubleshooting/Tesing   
  - [ping](../devlog/ping.md)