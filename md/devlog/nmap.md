---
caption: Network Mapper
created: 20211011081705090
desc: ''
id: b22uf82a31xkdp1cnlx713v
title: Nmap
updated: 1653437672473
---
   
   
- Network Mapper is a command line tool that maps the network.   
- Do [ping](../devlog/ping.md) sweeps to check what is up and available.   
- Look at individual ports and what OS that remote [Server](../devlog/server.md) is running.   
   
   
---   
   
Scanning from a machine connected to the [LAN](../devlog/lan.md), scanning for open ports on a web server also on [LAN](../devlog/lan.md) using [Nmap](../devlog/nmap.md)   
   
    nmap -sS -O 10.0.2.6 |more   
   
   
- `-sS` tells `nmap` to do a SYN Scan using only SYN packets from the [Three-Way Handshake] (SYN-SYN/ACK-ACK).   
- `-O` tells `nmap` to also scan what OS the web server is using.   
- `10.0.2.0` should be replaced with the target [ip address](../devlog/ip%20address.md).   
- `|more` tells `nmap` to give result one after another.   
- Example Output: ![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.pbozqpwksbr.png)   
- All of the unused service/port should be closed to make the server secure.   
- [zenmap](../devlog/zenmap.md) is GUI for [Nmap](../devlog/nmap.md)