---
created: 1656559710214
desc: ''
id: ahxqeweymljwoy5u6g6hxb3
title: TCP
updated: 1656560718865
---
   
   
- Transmission Control Protocol is a connection-oriented protocol.   
- It is a reliable way to transport segments across the network.   
  - If segment is dropped, protocol detects it and resends segments.   
- Acknowledgements are received for successful communications.   
- Flow control through [windowing](../devlog/windowing.md)   
- Used for all network data that needs to be assured to get to its destination.   
- A three way handshake   
   
TCP is a connection-oriented and reliable protocol. In this protocol, firstly the connection is established between the two hosts of the remote end, only then the data is sent over the network for communication. The receiver always sends an acknowledgment of the data received or not received by the sender once the first data packet is transmitted.   
   
After receiving the acknowledgment from the receiver, the second data packet is sent over the medium. It also checks the order in which the data is to be received otherwise data is re-transmitted. This layer provides an error correction mechanism and flow control. It also supports client/server model for communication.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656560069/wiki/rrevv3mbzgu9ffjnfkqk.png)   
   
See also: [tcp vs udp](../devlog/tcp%20vs%20udp.md)