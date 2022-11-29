---
created: 20211013081203244
desc: ''
id: uirqzeld6hvqmdshssza5we
title: Collision Domains
updated: 1653318536112
---
   
   
- Comprised of all devices on shared [Ethernet](../devlog/ethernet.md) segment (everything on same cable or [Hub](../devlog/hub.md))   
- Devices operate at half-duplex when connected to a [Hub](../devlog/hub.md) (Layer 1 Device)   
- Devices must listen before they transmit to avoid collisions when operating as `CSMA/CD`   
- The larger the Collision Domain, the more chaos in the network.   
- Collision Domains need to broken down into smaller chunks for more efficiency   
   
   
---   
   
### Collision Domains on [Switch](../devlog/switch.md)es   
   
   
- [Ethernet](../devlog/ethernet.md) [Switch](../devlog/switch.md)es increase scalability of the network by creating multiple collision domains   
- Each port on a switch is a Collision Domain, no chance of collisions and increases speed   
- Switches can operate in full-duplex mode   
   
   
---   
   
### Collision Domains on [Hub](../devlog/hub.md)s   
   
   
- [Hub](../devlog/hub.md)s were used to connect multiple network segments together   
- Each [LAN](../devlog/lan.md) segment becomes a separate [Collision Domains](../devlog/collision%20domains.md)   
- As the network gets larger in which a [Hub](../devlog/hub.md) is being utilized to connect all the machines, the network will get more chaotic as [Hub](../devlog/hub.md) don't break up [Collision Domains](../devlog/collision%20domains.md), it'll be treated as one large collision domain.   
- To deal with this issue a [Bridge](../devlog/bridge.md) needs to be introduced to the network.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.cqfqt7rooe6.png)