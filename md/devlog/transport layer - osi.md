---
created: '2021-10-10T00:00:00.000Z'
desc: ''
id: nygs97pchi3schragqr6gei
title: Transport Layer - OSI
updated: 1656567329375
---
   
# Layer 4 – Transport Layer   
   
   
- The Transport Layer (Layer 4) is the dividing line between the upper layers and the lower layers.   
- Data is sent as **Segments** and Datagrams.   
- [TCP](../devlog/TCP.md)/[UDP](../devlog/udp.md) are the two protocols used in Transport Layer.   
- We also have reliability features such as [Windowing](../devlog/windowing.md) and [Buffering](../devlog/buffering.md).   
   
   
---   
   
This layer guarantees an end to end error-free connection between the two different hosts or devices of networks. This is the first one which takes the data from the upper layer i.e. the application layer, and then splits it into smaller packets called the segments and dispenses it to the network layer for further delivery to the destination host.   
   
It ensures that the data received at host end will be in the same order in which it was transmitted. It provides an end to end supply of the data segments of both inter and intra sub-networks. For an end to end communication over the networks, all devices are equipped with a Transport service access point (TSAP) and are also branded as port numbers.   
   
A host will recognize its peer host at the remote network by its port number.   
   
**Error Detection & Control**: Error checking is provided in this layer because of the following two reasons:   
   
Even if no errors are introduced when a segment is moving over a link, it can be possible for errors to be introduced when a segment is stored in the router’s memory (for queuing). The data link layer is not able to detect an error in this scenario.   
   
There is no assurance that all the links between the source and destination will provide error scrutiny. One of the links may be using a link layer protocol which doesn’t offer the desired outcomes.   
   
### The methods used for error check and control are CRC (cyclic redundancy check) and checksum.   
   
**CRC**: The concept of CRC (Cyclic Redundancy Check) grounds on the binary division of the data component, as the remainder of which (CRC) is appended to the data component and sent to the receiver. The recipient divides data component by an identical divisor.   
   
If the remainder comes up to zero then the data component is allowed to pass to forward the protocol, else, it is assumed that the data unit has been distorted in transmission and the packet is discarded.   
   
**Checksum Generator & checker**: In this method, the sender uses the checksum generator mechanism in which initially the data component is split into equal segments of n bits. Then, all the segments are added together by employing 1’s complement.   
   
Later, it complements once again, and now it turns into checksum and then is sent along with the data component.   
   
**Example**: If 16 bits is to be sent to the receiver and bits are 10000010 00101011, then the checksum that will be transmitted to the receiver will be 10000010 00101011 01010000.   
   
Upon receiving the data unit, the receiver divides it into n equal size segments. All the segments are added using 1’s complement. The result is complemented once more and If the result is zero, the data is accepted, else discarded.   
   
This error detection & control method permits a receiver to rebuild the original data whenever it is found corrupted in transit.   
   
### Layer 4 Examples   
   
   
- [TCP](../devlog/TCP.md)   
- [UDP](../devlog/udp.md)   
- [WAN Accelerators](/not_created.md)   
- [Load Balancer](../devlog/load%20balancer.md)s   
- [firewall](../devlog/firewall.md)s   
   
See: [tcp vs udp](../devlog/tcp%20vs%20udp.md)