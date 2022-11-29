---
caption: User Datagram Protocol
created: 20211010120256830
desc: ''
id: k57h8hxtsubu8fdb61aahxc
title: UDP
updated: 1656560739212
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
   
- User Data-gram Protocol is a connection-less protocol.   
- Unreliable transport of segments.   
  - If dropped, sender is unaware. No sequencing or acknowledgement.   
- No [Windowing](../devlog/windowing.md), re-transmission.   
- Good for audio/video streaming (less overhead, increased performance).   
- E.g. YouTube video/audio streaming   
   
UDP is a connectionless and unreliable protocol. Once data is transmitted between two hosts, the receiver host doesn’t send any acknowledgment of receiving the data packets. Thus the sender will keep on sending data without waiting for an acknowledgment.   
   
This makes it very easy to process any network requirement as no time is wasted in waiting for acknowledgment. The end host will be any machine like a computer, phone or tablet.   
   
This type of protocol is widely used in video streaming, online games, video calls, voice over IP where when some data packets of video are lost then it doesn’t have much significance, and can be ignored as it doesn’t make much impact on the information it carries and doesn’t have much relevance.   
   
See also: [tcp vs udp](../devlog/tcp%20vs%20udp.md)