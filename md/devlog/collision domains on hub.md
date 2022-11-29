---
created: 20211013094627410
desc: ''
id: e0ug7ilzwuclmjrey8psnvv
title: Collision Domains on Hub
updated: 1653318485179
---
   
   
- [Hub](../devlog/hub.md)s were used to connect multiple network segments together   
- Each [LAN](../devlog/lan.md) segment becomes a separate [Collision Domains](../devlog/collision%20domains.md)   
- As the network gets larger in which a [Hub](../devlog/hub.md) is being utilized to connect all the machines, the network will get more chaotic as [Hub](../devlog/hub.md) don't break up [Collision Domains](../devlog/collision%20domains.md), it'll be treated as one large collision domain.   
- To deal with this issue a [Bridge](../devlog/bridge.md) needs to be introduced to the network.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.cqfqt7rooe6.png)