---
created: 20211009090217120
desc: ''
id: arlkpmdlwn4hm2n8iu7gmgs
title: Switch
updated: 1656409011007
---
   
A switch is a smarter version of the [Hub](../devlog/hub.md), a device that connects network devices together.   
   
Switches learn which devices are on which ports, a switch knows what port to forward data to.   
   
It broadcasts data only to the port that needs to receive it.   
   
Provides more security and effcient bandwith usage than a hub.   
   
   
---   
   
   
- Layer 2 device used to connect multiple network segments together   
- Essentially a multiport [Bridge](../devlog/bridge.md)   
- Switches learn [MAC](../devlog/mac.md) addresses and make forwarding decisions based on them   
- Switches analyze _source_ [MAC](../devlog/mac.md) addresses in frames entering the switch and populate an internal MAC address table based on them   
   
   
---   
   
   
- Each port on a switch represents an individual [collision domains](/not_created.md)   
- All ports belong to the same [Broadcast Domain](../devlog/Broadcast%20Domain.md)   
   
   
---   
   
### How Switches Improve Network Performance   
   
   
- Using ARP to discover MAC addresses of devices on the network and storing them in MAC Address table to confirm it back to the original requester. Basically everyone on the network answers to the query for the MAC address.   
   
   
- And the next time, when anyone needs to communicate with anyone, they can directly communicate with them since [Switch](../devlog/switch.md) has memorized the MAC address of all the devices on the network.   
- In this way, Switches improve performance and security of the network.   
   
   
---   
   
### CAN table   
   
Content Addressable Memory (CAM) table is a system memory construct used by Ethernet switch logic which stores information such as MAC addresses available on physical ports with their associated VLAN Parameters. The CAM table, or content addressable memory table, is present in all switches for layer 2 switching.