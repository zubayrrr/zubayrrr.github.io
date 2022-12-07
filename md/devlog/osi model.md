---
created: 20210926141234636
desc: ''
id: mmu3q72ghud78jtb8fv44ex
title: OSI Model
updated: 1656563176275
---
   
OSI stands for Open Systems Interconnection, developed in 1977 by the International Organization for Standardization(ISO).   
   
   
- ISO 7498 is for the standard, OSI model.   
- OSI Model can also be referred to as OSI Stack.   
   
   
---   
   
OSI model doesn't always accurately describe how networks actually operate (some things can operate at multiple layers of the OSI model), our networks today operate on the [tcp⁄ip model](../devlog/tcp%E2%81%84ip%20model.md) model but OSI model was the standard to describe how all and any network can possibly operate.   
   
OSI model serves as a reference model:   
   
   
- To categorize functions of the network into particular layer(s).   
- To compare technologies across different manufacturers.   
- To understand how to best communicate with that device, how to troubleshoot it etc.   
   
The OSI model has 7 layers:   
| Group | # | Layer Name | Key Responsibilities | Data Type Handled | Scope | Common Protocols and Technologies |   
|--------------|---|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|--------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|   
| Lower Layers | 1 | Physical | Encoding and Signaling; Physical Data Transmission; Hardware Specifications; Topology and Design | Bits | Electrical or light signals sent between local devices | (Physical layers of most of the technologies listed for the data link layer) |   
| Lower Layers | 2 | Data Link | Logical Link Control; Media Access Control; Data Framing; Addressing; Error Detection and Handling; Defining Requirements of Physical Layer | Frames | Low-level data messages between local devices | IEEE 802.2 LLC, Ethernet Family; Token Ring; FDDI and CDDI; IEEE 802.11 (WLAN, Wi-Fi); HomePNA; HomeRF; ATM; SLIP and PPP |   
| Lower Layers | 3 | Network | Logical Addressing; Routing; Datagram Encapsulation; Fragmentation and Reassembly; Error Handling and Diagnostics | Datagrams / Packets | Messages between local or remote devices | IP; IPv6; IP NAT; IPsec; Mobile IP; ICMP; IPX; DLC; PLP; Routing protocols such as RIP and BGP |   
| Lower Layers | 4 | Transport | Process-Level Addressing; Multiplexing/Demultiplexing; Connections; Segmentation and Reassembly; Acknowledgments and Retransmissions; Flow Control | Datagrams / Segments / Packets | Communication between software processes | TCP and UDP; SPX; NetBEUI/NBF |   
| Upper Layers | 5 | Session | Session Establishment, Management and Termination | Sessions | Sessions between local or remote devices | NetBIOS, Sockets, Named Pipes, RPC |   
| Upper Layers | 6 | Presentation | Data Translation; Compression and Encryption | Encoded User **D**ata | Application data representations | SSL; Shells and Redirectors; MIME |   
| Upper Layers | 7 | Application | User Application Services | User **D**ata | Application data | DNS; NFS; BOOTP; DHCP; SNMP; RMON; FTP; TFTP; SMTP; POP3; IMAP; NNTP; HTTP; Telnet |   
   
Table via - [The TCP/IP Guide - OSI Reference Model Layer Summary](http://www.tcpipguide.com/free/t_OSIReferenceModelLayerSummary.htm)   
   
The mnemonic we can use to remember is: "**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way\!"   
   
At different layers, data/information is called by different names.   
   
The mnemonic to remember the data types in the OSI model is: "**D**on't **S**ome **P**eople **F**orget **B**irthdays?"   
   
   
---   
   
   
# Layer 1 – Physical layer   
   
This where the transmission of bits across the network occurs and is focused on the physical and electrical characteristics of the network.   
   
There is where we decide if we're using an [Ethernet](../devlog/ethernet.md) network or if we're using [Fiber Optic](../devlog/fiber%20optic.md), or Copper cables.   
   
No matter what method we're using to transmit our data, it will always be in the form of binary [bit](../devlog/bit.md)s   
   
Binary [bit](../devlog/bit.md)s are series of 1s and 0s.   
   
Each media has different ways of representing these [bit](../devlog/bit.md)s   
   
For example, if we're using a Copper wire such as in a [Cat5](/not_created.md) or [Cat6](/not_created.md) network, you'll find that the voltage of the wire will be zero for a 0 [bit](../devlog/bit.md) and to represent a 1, you might use a +5 or -5 voltage on the Copper wire.   
   
**Transition Modulation** is what dictates the change is (or how it should be interpreted), If it changed during the clock cycle, then a 1 is represented (otherwise it is a 0).   
   
In case of a [Fiber Optic](../devlog/fiber%20optic.md) cable, we'll be using light instead of voltages; when we want a 1, we turn the light on. when we want to represent a 0, we turn the light off.   
   
   
---   
   
Once we have the data from the [Media](../topics/media.md), we'll have [Connector Types](../devlog/connector%20types.md) on the end of the cables that go inside our devices. These connectors are wired based on a standard.   
   
   
- TIA/EIA-568-B   
  - [RJ-45](../devlog/rj-45.md) cables and ports   
- T-568A and T-568B   
  - Crossover cables   
- [Straight-Through Patch Cable](../devlog/straight-through%20patch%20cable.md) typically uses T-568B on both ends, but could also use T-568A.   
- See: [Pinouts](../devlog/pinouts.md)   
   
### Topology of the network at the Physical Layer   
   
   
- Layer 1 devices view networks from a physical topology perspective, as discussed in [Wired Network Topology](../devlog/wired%20network%20topology.md) & [Wireless Network Topology](../devlog/wireless%20network%20topology.md).   
   
   
---   
   
### Synchronizing communication at Physical Layer   
   
How do we know that the receiving end is ready to accept the [bit](../devlog/bit.md)s that we're ready to send?   
   
   
- We can work this out either Asynchronously or Synchronously:   
   
#### Asynchronous   
   
   
- Uses "start bits" and "stop bits" to indicate when transmissions occur from sender to receiver.   
   
#### Synchronous   
   
   
- Uses a reference block to coordinate the transmissions by both sender and receiver. Happens in Real-time. Uses a time source, transmits data on the cadence of the time.   
   
   
---   
   
### How is the bandwidth utilized?   
   
There are again two ways, Broadband and Baseband.   
   
#### Broadband   
   
   
- Divides bandwidth into separate channels. (e.g. Cable TV)   
   
#### Baseband   
   
   
- Uses all available frequencies on a medium (cable) to transmit data and uses a reference clock to coordinate the transmissions by both sender and receiver. (e.g. Telephone, Home [Ethernet](../devlog/ethernet.md))   
   
   
---   
   
### If we're using a single Baseband using all of the bandwidth how can we get more out of a limited network?   
   
   
- Time-Division Multiplexing (TDM)   
  - Each session takes a turn, using time slots, to share the medium between all users.   
- Statistical Time-Division Multiplexing (StatTDM)   
  - More efficient version of TDM since it dynamically allocates time slots on an as-needed basis instead of statically assigning.   
- Frequency-Division Multiplexing (FDM)   
  - Medium is divided into various channels based on frequencies and each session is transmitted over a different channel.   
   
   
---   
   
### Media at Layer 1 (Layer 1 Examples)   
   
Devices that give physical response, hence a physical layer device.   
   
   
- Cables   
  - [Ethernet](../devlog/ethernet.md)   
  - [Fiber Optic](../devlog/fiber%20optic.md)   
- Radio Frequencies   
  - [Wi-Fi](../devlog/wi-fi.md)   
  - [Bluetooth](../devlog/Bluetooth.md)   
  - [NFC](../devlog/nfc.md)   
- Infrastructure Devices   
  - [Hub](../devlog/hub.md)s   
  - Wireless Access Points   
  - [Media Converters](../devlog/media%20converters.md)
   
   
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
   
   
# Layer 5 – Session Layer   
   
Think of a session as a conversation that must be kept separate from others to prevent intermingling of the data.   
   
This layer permits the users of different platforms to set up an active communication session between themselves.   
   
The main function of this layer is to provide sync in the dialogue between the two distinctive applications. The synchronization is necessary for efficient delivery of data without any loss at the receiver end.   
   
**Example.**   
   
Assume that a sender is sending a big data file of more than 2000 pages. This layer will add some checkpoints while sending the big data file. After sending a small sequence of 40 pages, it ensures the sequence & successful acknowledgment of data.   
   
If verification is OK, it will keep repeating it further till the end otherwise it will re-synchronize and re-transmit.   
   
This will help in keeping the data safe and the whole data host will never completely get lost if some crash happens. Also, token management, will not allow two networks of heavy data and of the same type to transmit at the same time.   
   
### Setting up a Session   
   
   
- Check user credentials   
- Assign numbers to session to identify them   
- Negotiate services needed for session   
- Negotiate who begins sending data   
   
   
---   
   
### Maintaining Session   
   
   
- Transfer the data   
- Reestablish a disconnected session   
- Acknowledging receipt of data   
   
   
---   
   
### Tearing Down a Session   
   
   
- Due to mutual agreement   
  - After the transfer is done   
- Due to other party disconnecting   
   
   
---   
   
### Layer 5 Examples   
   
   
- [H323](../devlog/H323.md)   
  - Used to setup, maintain, and tear down a voice/video connection.   
- [NetBIOS](../devlog/netbios.md)   
  - Used by computers to share files over a network.
   
   
# Layer 6 – Presentation Layer   
   
   
- Responsible for formatting the data exchanged and securing the data with proper encryption.   
- Functions:   
  - Data formatting   
  - Encryption   
   
As suggested by the name itself, the presentation layer will present the data to its end users in the form in which it can easily be understood. Hence, this layer takes care of the syntax, as the mode of communication used by the sender and receiver may be different.   
   
### Data Formatting   
   
   
- Formats data for proper compatibility between devices.   
  - ASCII   
  - GIF   
  - JPG   
- Ensures data is readable by receiving system   
- Provides proper data structures   
- Negotiates data transfer syntax for the [Application Layer - OSI](../devlog/application%20layer%20-%20osi.md)   
   
   
---   
   
### Encryption   
   
   
- Used to scramble the data in transit to keep it secure for prying eyes.   
- Provides confidentiality of data.   
- E.g.   
  - [TLS](../devlog/tls.md) to secure data between your PC and website.   
   
   
---   
   
### Layer 6 Examples   
   
**Presentation styles** - taking ones and zeros and present them in the human readable format   
   
   
- [HTML](/not_created.md), [XML](/not_created.md), [PHP](/not_created.md), [languages.javascript](../devlog/languages.javascript.md)   
- [ASCII](/not_created.md), [EBCDIC](/not_created.md), [UNICODE](/not_created.md)   
- GIF, JPG, TIF, SVG, PNG   
- MPG, MOV   
   
**Encryption styles** - how do we secure data in a jumbled format?   
   
   
- [TLS](../devlog/tls.md), [SSL](../devlog/ssl.md)
   
   
# Layer 7 – Application Layer   
   
   
- Provides application level services (Not MS Word or Notepad)   
- Layer where the users communicate with the computer   
- Functions:   
  - Application services   
  - Services advertisement   
   
This layer grants a direct interface and access to the users with the network. The users can directly access the network at this layer. Few Examples of services provided by this layer include e-mail, sharing data files, FTP GUI based software like Netnumen, Filezilla (used for file sharing), telnet network devices etc.   
   
There is vagueness in this layer as is not all user-based information and the software can be planted into this layer.   
   
For Example, any designing software can’t be put directly at this layer while on the other hand when we access any application through a web browser, it can be planted at this layer as a web browser is using HTTP (hypertext transfer protocol) which is an application layer protocol.   
   
### Application Services   
   
Application level services in the [OSI Model](../devlog/osi%20model.md) context mean stuff like file transfer, the user communicates with the computer and the computer passes on the user request to the network.   
   
   
- Application services unite communicating components from more than one network application.   
- E.g:   
  - File transfers and file sharing   
  - E-mail   
  - Remote access   
  - Network management activities   
  - [Client](../devlog/client.md)/[Server](../devlog/server.md) Processes   
   
   
---   
   
### Service Advertisement   
   
   
- Some applications send out announcements   
- States the services they offer on the network   
- Some centrally register with the Active Directory server instead   
- E.g:   
  - Printer   
  - File Servers   
   
   
---   
   
### Layer 7 Examples   
   
   
- E-mail ([POP3](../devlog/pop3.md), [IMAP](../devlog/imap.md), [smtp](../devlog/smtp.md))   
- Web Browsing ([HTTP](../devlog/http.md), [HTTPS](../devlog/https.md))   
- Domain Name Service ([DNS](../devlog/dns.md))   
- File Transfer Protocols ([FTP](../devlog/ftp.md), [FTPS](/not_created.md))   
- Remote Access ([telnet  protocol](../devlog/telnet%20%20protocol.md)), [ssh](../devlog/ssh.md))   
- Simple Network Management Protocol ([SNMP](../devlog/snmp.md))
   
   
   
---   
   
## Lab   
   
Using [wireshark](../devlog/wireshark.md) packet analyzer to pull apart network traffic and see the different layers of the OSI model.   
   
## Lab   
   
   
- Wireshark captures data from network interface.   
  - You specify the interface where you want to capture data from.   
- When you want to capture data from a network that is not yours(you're not part of) you need a network interface card that can be put into monitor(or promiscuous) mode.   
   
1. Start your wireshark: `sudo wireshark`   
2. Select the Network Interface you want to capture from   
   
	![](https://res.cloudinary.com/zubayr/image/upload/v1656564583/wiki/fq6qfmktq5g307dfd2hp.png)   
   
3. Wireshark will start capturing data   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656564634/wiki/vkhseens6nesk0jpc80c.png)   
   
4. As we know that data is called by different names at different layers, for example frames, packets etc.   
5. Select a frame from the frame list   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656564941/wiki/mogpgsv01imjawha3unt.png)   
   
We can see information about this particular frame, it’s source and destination IP, in this case it seems like the request was sent to my Samsung device.   
   
Below in the packet bytes menu, we can also see that the data is in scrambled state(hexdecimal and ASCII).   
   
You can even view the data in bits(binary). Right click and convert the data into your desired format.   
   
6. Analyzing a layer 7 packet   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656566188/wiki/y8xnjecfoiu6lswkfinz.png)   
   
We can see that this was an HTTP frame, it originated from what application(qBittorrent), we see that our target is doing some shady torrenting.   
   
Let’s see if we can follow this stream and check what they actually got.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656566302/wiki/qoxgwp5afttglbg2yk88.png)   
   
It looks like this particular HTTP GET request sent back some data - it’s not really HTML, like you’d expect(?).   
   
You can save all the captured traffic in a `.pcap` file and try to analyze the traffic, put the captured traffic back into it’s original state etc.
   
   
## Resources   
   
   
- [7 Layers of The OSI Model (A Complete Guide)](https://www.softwaretestinghelp.com/osi-model-layers/#1_Layer_1_8211_Physical_layer)