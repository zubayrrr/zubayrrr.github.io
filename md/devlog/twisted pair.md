---
created: 20211005105059156
desc: ''
id: q6rcmbb4k2on7oh9zfm90ba
title: Twisted Pair
updated: 1656501136701
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
   
- Transmits electrons   
- Twists reduces interference   
- Most popular physical LAN media type   
- Eight individually insulated strands of copper wire inside each cable   
- Types:   
  - Shielded([STP](../devlog/stp.md)) gives additional insulating barrier against electronic magnetic interference (beneficial where theres a lot of electrical noise)   
  - Unshielded ([UTP](../devlog/utp.md)) doesn't have extra protection but is useful in most standard office environments and is also cheaper.   
   
   
---   
   
#### T-568A wiring standard   
   
   
- Often used for [Crossover Cable](../devlog/crossover%20cable.md), used to link older [Ethernet](../devlog/ethernet.md) netowork switches, although modern switches can detect what type of cable is plugged in.   
- Only one end of the cable is made using this standard.   
   
#### T-568B wiring standard   
   
   
- Used for [Straight-Through Patch Cable](../devlog/straight-through%20patch%20cable.md).   
- Both end of the cables are twisted using this standard.   
   
   
---   
   
### Twisted Pair cable throughput   
   
<table>   
<thead>   
<tr class="header">   
<th>Category</th>   
<th>Max Throughput</th>   
<th style="text-align: right;">Max Distance</th>   
</tr>   
</thead>   
<tbody>   
<tr class="odd">   
<td>Cat 3</td>   
<td>10 Mbps</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
<tr class="even">   
<td>Cat 5</td>   
<td>100 Mbps</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
<tr class="odd">   
<td>Cat 5e</td>   
<td>1,000 Mbps (1 Gbps)</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
<tr class="even">   
<td>Cat 6</td>   
<td>1,000 Mbps (1 Gbps)</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
<tr class="odd">   
<td>Cat 6a</td>   
<td>10,000 Mbps (10 Gbps)</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
<tr class="even">   
<td>Cat 7</td>   
<td>100,000 Mbps (10 Gbps)</td>   
<td style="text-align: right;">100 meters</td>   
</tr>   
</tbody>   
</table>   
   
The thicker the copper the better, the more twists of the adjacent wires per inch to reduce crosstalk interference.   
   
   
---   
   
### Type of Twisted Pair Connectors   
   
   
- RJ-45:   
   
<!-- end list -->   
   
   
- 8-pin connector in Ethernet networks   
- Most Ethernet use only 4-pins   
- It is a [Twisted Pair](../devlog/twisted%20pair.md) cable connector.   
- You can also use it for token ring network if you've the appropriate equipment.   
   
<!-- end list -->   
   
   
- RJ-11:   
   
<!-- end list -->   
   
   
- 6-pin connector   
- It is a [Twisted Pair](../devlog/twisted%20pair.md) cable connector   
- Commonly only 2 or 4 pins are used   
- Commonly found in telephone systems   
- A basic telephone setup really requires only two wires