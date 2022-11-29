---
created: 20211010103518376
desc: ''
id: ofmapzoha5kl5i46y1lkc2b
title: Data Link Layer - OSI
updated: 1656501965850
---
   
# Layer 2 – Data-link Layer   
   
In the Data Link Layer, we'll package up the [bit](../devlog/bit.md)s we received from the Layer 1 ([Physical Layer - OSI](../devlog/physical%20layer%20-%20osi.md)) and put them in [Frames](/not_created.md) and take those frames and transmit them throughout the network while performing error detection/correction, uniquely identifying network devices with an address ([MAC](../devlog/mac.md)), and a providing flow control.   
   
### LLC   
   
**Logical Link Control** provides connection services and allows acknowledgement of the receipt of messages.   
   
It is the most basic form of flow control. It also provides basic error control functions, such as, informed the sender if they received a corrupted frame, it does this using a checksum.   
   
LLC allows a device to make a request for either less information at a time or to replay that information.   
   
### How is communication synchronized?   
   
 **Isochronous**   
   
- Similar to Synchronous in [Physical Layer - OSI](../devlog/physical%20layer%20-%20osi.md) but they also create time slots for transmission.   
- They use a common reference clock source and create time slots for transmission with less overhead than synchronous or asynchronous methods.   
**Synchronous**   
   
- Network devices agree on clocking method to indicate beginning and end of frames and can use control characters or separate timing channels.   
**Asynchronous**   
   
- Network devices reference their own internal clocks and use start/stop [bit](../devlog/bit.md)s.   
   
   
---   
   
### Layer 2 Examples   
   
   
- [NIC](../devlog/nic.md)   
- [Bridge](../devlog/bridge.md)s   
- [Switch](../devlog/switch.md)es   
- [MAC](../devlog/mac.md) Addresses