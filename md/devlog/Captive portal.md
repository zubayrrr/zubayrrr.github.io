---
category: '2022'
created: 2022-11-30 16:46:10.449000+00:00
id: 2f04434f-d591-43c5-95de-b7e710100699
tags:
- devlog
title: Captive Portal
updated: 2022-11-30 16:46:10.873000+00:00
---
   
Topics:: [Networking](../topics/networking.md), [Linux](../topics/linux.md)   
   
   
---   
   
If Captive Portal doesn’t pop up on it’s own:   
   
```bash
route -n
```
   
   
Captive Portal isn’t popping up on a Linux machine that has docker installed.   
   
You might need to delete these devices docker installs such as `docker0` and other starting with `br-`   
   
```bash
sudo ip link delete <device>
```
