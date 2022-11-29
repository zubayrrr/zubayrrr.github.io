---
created: 20211009092337388
desc: ''
id: co4eno6fzx5ov2408cmwe3w
title: Ethernet
updated: 1653437364795
---
   
   
- IEEE 802.3 standard   
- In early computer networks, there were many different network technologies competing for a portion of the market share   
- Ethernet, Token Ring, FDDI and others fought for dominance   
- Currently, Ethernet is dominant for Layer 1   
   
### Origins of Ethernet   
   
   
- Was first run over [Coax](../devlog/coax.md) cables (10Base5, 10Base2), using vampire taps, BNC connectors.   
- Ethernet has changed to using [Twisted Pair](../devlog/twisted%20pair.md) cables using [UTP](../devlog/utp.md), [STP](../devlog/stp.md)   
- 10BASE-T is [UTP](../devlog/utp.md) - max speed 10 Mbps and max distance 100 meters, this is clearly not enough   
   
### How should devices access the network?   
   
   
- Deterministic   
  - Very organized and orderly   
  - Need an electronic token to transmit   
  - For example: Token Ring   
- Contention-based   
  - Very chaotic   
  - Transmit (almost) whenever you want   
  - For example: [Ethernet](../devlog/ethernet.md)   
   
   
---   
   
### CSMA/CD   
   
   
- [Ethernet](../devlog/ethernet.md) devices transmit based on a principle called Carrier Sense Multiple Access/Collision Detect or CSMA/CD   
- Carrier Sense   
  - Listen to the wire, verify it is not busy   
- Multiple Access   
  - All devices have access at any time   
- Collision Detect   
  - If two deviecs transmit at the same time, a collision occurs   
  - Back off, wait a random time and try again   
   
   
---   
   
### Collision Domains   
   
   
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
   
   
---   
   
### Speed Limitations   
   
<table>   
<thead>   
<tr class="header">   
<th style="text-align: center;">Ethernet Type</th>   
<th style="text-align: center;">Bandwidth Capacity</th>   
<th style="text-align: center;">Description</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td style="text-align: center;">Ethernet</td>   
<td style="text-align: center;">10 Mbps</td>   
<td style="text-align: center;">10 million bits per second</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;">Fast Ethernet</td>   
<td style="text-align: center;">100 Mbps</td>   
<td style="text-align: center;">100 million bits per second</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;">Gigabit Ethernet</td>   
<td style="text-align: center;">1000 Mbps (I Gbps)</td>   
<td style="text-align: center;">1 billion bits per second</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;">10-Gigabit Ethernet</td>   
<td style="text-align: center;">10 Gbps</td>   
<td style="text-align: center;">10 billion bits per second</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;">100-Gigabit Ethernet</td>   
<td style="text-align: center;">100 Gbps</td>   
<td style="text-align: center;">100 billion bits per second</td>   
</tr>   
</tbody>   
</table>   
   
   
- Bandwidth is the measure of how many bits the network can transmit in 1-second (bps)   
- Type of cable determines the bandwidth capacity of the network   
   
   
---   
   
### Distance Limitations   
   
<table>   
<thead>   
<tr class="header">   
<th style="text-align: center;">Ethernet Standard</th>   
<th style="text-align: right;">Media Type</th>   
<th style="text-align: center;">Bandwidth Capacity</th>   
<th style="text-align: center;">Distance Limitation</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td style="text-align: center;">10BASE-T</td>   
<td style="text-align: right;">Cat 3 or Higher</td>   
<td style="text-align: center;">10 Mbps</td>   
<td style="text-align: center;">100 m</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;">100BASE-TX</td>   
<td style="text-align: right;">Cat 5 or Higher</td>   
<td style="text-align: center;">100 Mbps</td>   
<td style="text-align: center;">100 m</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;">1000BASE-TX</td>   
<td style="text-align: right;">Cat 6 or Higher</td>   
<td style="text-align: center;">1 Gbps</td>   
<td style="text-align: center;">100 m</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;">1000BASE-SX</td>   
<td style="text-align: right;"><a href="#MMF" class="tc-tiddlylink tc-tiddlylink-resolves">MMF</a></td>   
<td style="text-align: center;">1 Gbps</td>   
<td style="text-align: center;">220 m</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;">1000BASE-LX</td>   
<td style="text-align: right;"><a href="#MMF" class="tc-tiddlylink tc-tiddlylink-resolves">MMF</a></td>   
<td style="text-align: center;">1 Gbps</td>   
<td style="text-align: center;">550 m</td>   
</tr>   
<tr class="even">   
<td style="text-align: center;">1000BASE-LX</td>   
<td style="text-align: right;"><a href="#SMF" class="tc-tiddlylink tc-tiddlylink-resolves">SMF</a></td>   
<td style="text-align: center;">1 Gbps</td>   
<td style="text-align: center;">5 km</td>   
</tr>   
<tr class="odd">   
<td style="text-align: center;">100BASE-ZX</td>   
<td style="text-align: right;"><a href="#SMF" class="tc-tiddlylink tc-tiddlylink-resolves">SMF</a></td>   
<td style="text-align: center;">1 Gbps</td>   
<td style="text-align: center;">70 km</td>   
</tr>   
</tbody>   
</table>   
   
   
- Type of cable determines the distance limitation of the network