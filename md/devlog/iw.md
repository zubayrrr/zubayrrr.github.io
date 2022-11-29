---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: 8d1ya7990mhbcd1kidhigtj
title: iw
updated: 1653437708505
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Show / manipulate wireless devices and their configuration   
   
`iw` is a newer command which is more powerful than `iwconfig`, but different syntax that [ifconfig](../devlog/ifconfig.md)/[iwconfig](/not_created.md). (In fact there is an analogous command called [ip](../devlog/ip.md) which is meant to replace ifconfig for wired interfaces   
   
## Examples   
   
```
iw list | less
```
   
   
To view the available WiFi hardware/interfaces:   
   
```
$ iw dev
```
   
   
You can check the link details:   
   
```
$ iw dev wlan0 link
```
   
   
To disconnect from an AP run:   
   
```
$ sudo iw dev wlan0 disconnect
```
   
   
> — via [Using iw to Manage Wireless LAN in Linux](http://ict.siit.tu.ac.th/help/iw)