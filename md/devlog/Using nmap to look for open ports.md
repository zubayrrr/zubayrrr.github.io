---
created: 20211011083245452
desc: ''
id: ks0724ic46vnuso02phu8ow
title: Nmap - Open ports
updated: 1656581394695
---
   
Topics::  [linux](../topics/linux.md), [networking](../topics/networking.md)   
   
   
---   
   
Scanning from a machine connected to the [LAN](../devlog/lan.md), scanning for open ports on a web server also on [LAN](../devlog/lan.md) using [Nmap](../devlog/nmap.md)   
   
`nmap -sS -O 10.0.2.6 |more`   
   
   
- `-sS` tells `nmap` to do a SYN Scan using only SYN packets from the Three-Way Handshake (SYN-SYN/ACK-ACK).   
- `-O` tells `nmap` to also scan what OS the web server is using.   
- `10.0.2.0` should be replaced with the target [ip address](../devlog/ip%20address.md).   
- `|more` tells `nmap` to give result one after another.   
- Example Output: ![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.pbozqpwksbr.png)   
- All of the unused service/port should be closed to make the server secure.   
- zenmap is GUI for [Nmap](../devlog/nmap.md)