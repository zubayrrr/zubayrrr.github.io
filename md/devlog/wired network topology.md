---
created: 20211009093551640
desc: ''
id: 3tjqysfje7v916n5bbpa8k3
title: Wired Network Topology
updated: 1653318536180
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
Network Topologies:   
   
   
- Physically:   
  - How many devices are connected by media (physical cabling)   
  - Where are they physically located at   
- Logically:   
  - How the actual network traffic flows   
  - How are they logically connected   
   
   
---   
   
### Bus Topology   
   
A single cable running through an area that requires network connectivity and each device "taps" into the cable using either a T-connector or vampire tap. (big thick metal cable, each device connected would clamp onto the big cable and establish a connection hence a vampire tap, very old, not used today), a single collision domain.   
   
   
---   
   
### Ring Topology   
   
Uses a cable running in a circular loop and each device is connected to the ring with the data traveling in a singular direction. Ring toplogy that uses an electronic token to prevent collisions by requiring a device to hold the "token" when communicating on the network called a "Ring Token".   
   
#### Fiber Distributed Data Interface   
   
FDDI Ring in Fiber networks use two counter-rotating rings for redundancy.   
   
Modern ring networks are usually FDDI networks.   
   
   
---   
   
### Star Topology   
   
Most popular pysical LAN topology where devices connect to a single contralizzed point or device. Central point is normally a [Switch](../devlog/switch.md).   
   
If the central device fails, the entire network fails. Star Topology has a single point of failure.   
   
   
---   
   
### Hub-and-Spoke Topology   
   
Similar to Star but with WAN Links instead of LAN connections and it is used connecting multiple sites.   
   
   
---   
   
### Full-Mesh Topology   
   
Most redundant toplogy where every node connects to very other node and optimal routing between nodes is always available.   
   
Number of connections can get high and messy with increasing number of devices in the network.   
   
![](https://cdn.jsdelivr.net/gh/zubayrrr/twiki/bin/image.9pewkof3kcf.png)   
   
   
---   
   
### Partial-Mesh Topology   
   
Hybrid of the full-mesh and hub-and-spoke topologies.   
   
Provides optimal routes between some sites, while avoiding the expense of connecting every site.   
   
Network traffic patterns must be considered to design it effectively.