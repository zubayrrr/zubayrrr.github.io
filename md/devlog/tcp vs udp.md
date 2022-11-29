---
created: 20211011055013716
desc: ''
id: fg9c1iu7kore9v72yvr9bji
title: TCP VS UDP
updated: 1656560704548
---
   
[TCP](../devlog/TCP.md) has a lot more overhead than [UDP](../devlog/udp.md).   
   
| Feature                | TCP                                                                                                             | UDP                                                                                                |   
| ---------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |   
| Connection status      | Requires an established connection to transmit data (connection should be closed once transmission is complete) | Connectionless protocol with no requirements for opening, maintaining, or terminating a connection |   
| Data sequencing        | Able to sequence                                                                                                | Unable to sequence                                                                                 |   
| Guaranteed delivery    | Can guarantee delivery of data to the destination router                                                        | Cannot guarantee delivery of data to the destination                                               |   
|Handshaking Techniques | Uses handshakes such as SYN, ACK, SYN-ACK|It’s a connectionless protocol i.e. No handshake|   
| Retransmission of data | Retransmission of lost packets is possible                                                                      | No retransmission of lost packets                                                                  |   
| Error checking         | Extensive error checking and acknowledgment of data                                                             | Basic error checking mechanism using checksums                                                     |   
| Method of transfer     | Data is read as a byte stream; messages are transmitted to segment boundaries                                   | UDP packets with defined boundaries; sent individually and checked for integrity on arrival        |   
| Speed                  | Slower than UDP                                                                                                 | Faster than TCP                                                                                    |   
| Broadcasting           | Does not support Broadcasting                                                                                   | Does support Broadcasting                                                                          |   
| Optimal use            | Used by HTTPS, HTTP, SMTP, POP, FTP, etc                                                                        | Video conferencing, streaming, DNS, VoIP, etc                                                      |