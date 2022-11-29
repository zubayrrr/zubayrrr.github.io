---
created: '2021-10-10T00:00:00.000Z'
desc: ''
id: 2lmaspsqaxrf42wuvmcp02f
title: Network Layer - OSI
updated: 1656505695504
---
   
# Layer 3 – Network Layer   
   
   
- At Layer 3 we're concerned with Routing(forwarding traffic with logical addresses or [ip address](../devlog/ip%20address.md))   
- Routing is called Switching at Layer 3, which can be confusing because [Switch](../devlog/switch.md)es are Layer 2 ([Data Link Layer - OSI](../devlog/data%20link%20layer%20-%20osi.md)) devices.   
- Connection services   
- Bandwidth usage   
- Multiplexing strategies   
   
   
---   
   
### Logical Address   
   
   
- Numerous routing protocols were used for logical addressing over the years:   
  - AppleTalk   
  - Internetwork Packet Exchange(IPX)   
  - Internet Protocol (IP)   
- IP is one of the logical addressing schemes, only Internet Protocol (IP) remains dominant. [ip address](../devlog/ip%20address.md)   
  - [IPv4](../devlog/ipv4.md)   
  - [IPv6](/not_created.md)   
   
   
---   
   
### How should data be _forwarded_ or routed?   
   
Three main ways of achieving this are as follows:   
   
   
- Packet switching(known as _routing_)   
  - Data is divided into packets and forwarded.   
- Circuit switching   
  - Dedicated communication link is established between two devices.   
- Message switching   
  - Data is divided into messages, similar to packet switching, except, these messages may be stored then forwarded.   
   
   
---   
   
### Route Discovery and Selection   
   
   
- [router](../devlog/router.md)s maintain a routing table to understand how to forward a packet based on destination [ip address](../devlog/ip%20address.md)   
- Manually configured as a static route or dynamically through a routing protocol   
  - [RIP](../devlog/RIP.md)   
  - [OSPF](../devlog/OSPF.md)   
  - [EIGRP](../devlog/EIGRP.md)   
   
All these routers are talking to each other and they know which way is the fastest way to the destination. The routers take into account the traffic on the network etc.   
   
   
---   
   
### Connection Services   
   
   
- Layer 3 augments Layer 2 to improve reliability.   
- Flow control   
  - Prevents sender from sending data faster than receiver can get it.   
- Packet reordering   
  - Allows packets to be sent over multiple links and across multiple routes for faster service.   
   
   
---   
   
### Internet Control Message Protocol (ICMP)   
   
   
- Used to send error messages and operational information about an IP destination(common used one is [ping](../devlog/ping.md)).   
- Not regularly used by end-user applications.   
- Used in troubleshooting ([ping](../devlog/ping.md) & [traceroute](../devlog/traceroute.md))   
   
   
---   
   
### Layer 3 Examples   
   
   
- [router](../devlog/router.md)s   
- Multilayer [Switch](../devlog/switch.md)s   
- [IPv4](../devlog/ipv4.md) protocol   
- [IPv6](/not_created.md) protocol   
- [ICMP](../devlog/icmp.md)   
   
### Subnet mask   
   
The network address and the host address defined in the IP address is not solely efficient to determine that the destination host is of the same sub-network or remote network. The subnet mask is a 32-bit logical address that is used along with the IP address by the routers to determine the location of the destination host to route the packet data.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656505733/wiki/g2s3ypo7rzywlll8o2m9.png)   
   
**For the above Example,** by using a subnet mask 255.255.255.0, we get to know that the network ID is 192.168.1.0 and the host address is 0.0.0.64. When a packet arrives from 192.168.1.0 subnet and has a destination address as 192.168.1.64, then the PC will receive it from the network and process it further to the next level.   
   
Thus by using subnetting, the layer-3 will provide an inter-networking between the two different subnets as well.   
   
The IP addressing is a connectionless service, thus the layer -3 provides a connectionless service. The data packets are sent over the medium without waiting for the recipient to send the acknowledgment. If the data packets which are big in size are received from the lower level to transmit, then it splits it into small packets and forwards it.   
   
At the receiving end, it again reassembles them to the original size, thus becoming space efficient as a medium less load.