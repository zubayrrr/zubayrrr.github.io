---
created: '2022-03-12T00:00:00.000Z'
desc: ''
id: 5fv3dcbwq6x4tla4qd6mx3a
tags:
- topics
title: Networking
updated: 1664481408609
---
   
## Networking Basics   
   
   
- **Host** are any devices which send or receive traffic.   
- [IP Address](../devlog/ip%20address.md) the identity of each host.   
   
**Networks**   
   
   
- A logical group of hosts which require similar connectivity.   
- A network is what transports traffic between hosts.   
- Networks can contain other networks([subnet](../devlog/subnet.md)s).   
- Networks connect to other networks([internet](../devlog/internet.md)).   
   
**Switches**   
   
   
- Switches facilitate communication within a network.   
- A switch forwards data packets between hosts. A switch sends packets directly to hosts.   
- A switch only sends data to the single device it is intended for (unlike a [hub](../devlog/hub.md), which is very dumb).   
- Network: A Grouping of hosts which require similar connectivity.   
- Hosts on a Network share the same IP address space.   
   
**Modem**   
   
   
- [Modem](../devlog/Modem.md) is short for modulator/demodulator.   
- There are two kinds of signals:   
  - A computer **only** reads Digital Signal.   
  - Analog Signal that is used on the internet.   
- To deal with this a modem is introduced - whose responsibility is a to convert the signals from Digital to Analog and vice versa.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656493565/wiki/g8gzj19fawcjw7v4xr06.png)   
   
**Router**   
   
A [router](../devlog/router.md) comes into the picture after a modem.   
   
There are generally two kinds of Routers - large routers for business and small routers for homes/small offices.   
   
Let's talk about small office/home routers:   
   
A router is what routes or passes internet connection to all your devices(after modem has done it's thing).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656493698/wiki/vl4jvm2mj37ysepiueqd.png)   
   
These small office/home routers typically come with a builtin switch with multiple ports(so you can connect multiple devices using ethernet cable connection), it also functions as a wireless access point so that Wi-Fi enabled devices can also have internet access.   
   
If you only need one device to access the internet you don't need a router - you can simply use a modem.   
   
   
---   
   
Routers select paths for data packets to cross networks and reach their destinations. This is done by connecting with different networks and forwarding data from network to network.   
   
Router facilitates communication between networks. As we said before that a switch looks after communication within a network a router allows us to join these networks together or at least give them access to each other if permitted.   
   
A router can provide a traffic control point (security, filtering, redirecting) More and more switches also provide some of these functions now.   
   
Routers learn which networks they are attached to. These are known as routes, a routing table is all the networks a router knows about.   
   
A router has an IP address in the networks they are attached to. This IP is also going to be each host's way out of their local network also known as a gateway.   
   
   
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
   
**Presentation styles** - taking ones and zeros and present them in the human readable format?   
   
   
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
   
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
The [OSI Model](../devlog/osi%20model.md) is just a reference/logical model. It was designed to describe the functions of the communication system by dividing the communication procedure into smaller and simpler components. But when we talk about the TCP/IP model, it was designed and developed by Department of Defense (DoD) in 1960s and is based on standard protocols. It stands for Transmission Control Protocol/Internet Protocol. The TCP/IP model is a concise version of the OSI model. It contains four layers, unlike seven layers in the OSI model.   
   
The layers are:   
   
   
- Process/Application Layer   
- Host-to-Host/Transport Layer   
- Internet Layer   
- Network Access/Link Layer   
   
## Difference between TCP/IP and OSI Model:   
   
| TCP/IP                                                                           | OSI                                                                                                    |   
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |   
| TCP refers to Transmission Control Protocol.                                     | OSI refers to Open Systems Interconnection.                                                            |   
| TCP/IP has 4 layers.                                                             | OSI has 7 layers.                                                                                      |   
| TCP/IP is more reliable                                                          | OSI is less reliable                                                                                   |   
| TCP/IP does not have very strict boundaries.                                     | OSI has strict boundaries                                                                              |   
| TCP/IP follow a horizontal approach.                                             | OSI follows a vertical approach.                                                                       |   
| TCP/IP uses both session and presentation layer in the application layer itself. | OSI uses different session and presentation layers.                                                    |   
| TCP/IP developed protocols then model.                                           | OSI developed model then protocol.                                                                     |   
| Transport layer in TCP/IP does not provide assurance delivery of packets.        | In OSI model, transport layer provides assurance delivery of packets.                                  |   
| TCP/IP model network layer only provides connection less services.               | Connection less and connection oriented both services are provided by network layer in OSI model.      |   
| Protocols cannot be replaced easily in TCP/IP model.                             | While in OSI model, Protocols are better covered and is easy to replace with the change in technology. |   
   
## Layers   
   
   
# Layer 1 - Network Interface Layer   
   
   
- Physical and electrical characteristics   
- Describes how to transmit [bit](../devlog/bit.md)s across the network   
- Determines how interface uses network medium ([Network Cables](../devlog/network%20cables.md))   
  - [Coax](../devlog/coax.md)ial, [Fiber Optic](../devlog/fiber%20optic.md), [Twisted Pair](../devlog/twisted%20pair.md) copper cabling   
- Layer 1 Examples:   
  - [Ethernet](../devlog/ethernet.md), Token Ring, FDDI], RS-232
   
   
# Layer 2 - Internet Layer   
   
   
- Packages data into IP Datagrams   
  - Contains source and destination IPs   
  - Forwards datagrams between hosts across the networks   
- Routes IP datagrams across networks   
- Connectivity occurs externally   
- Layer 2 Examples:   
  - [ip](../devlog/ip.md), [ICMP](../devlog/icmp.md), [ARP](../devlog/ARP.md), [RARP](../devlog/RARP.md)
   
   
# Layer 3 - Transport Layer   
   
It is very similar to the [transport layer - osi](/not_created.md)   
   
   
- Provides communication session management between hosts   
- Defines level of service and status of connection used for transport   
- Layer 3 Examples:   
  - [TCP](../devlog/TCP.md)   
  - [UDP](../devlog/udp.md)   
  - [RTP](../devlog/rtp.md)
   
   
# Layer 4 - Application Layer   
   
   
- Defines [tcp⁄ip model](../devlog/tcp%E2%81%84ip%20model.md) application protocols   
- Defines how programs interface with the transport layer service   
- Layer with which the user interacts   
- Layer 4 Examples:   
  - [HTTP](../devlog/http.md), [telnet  protocol](../devlog/telnet%20%20protocol.md)), [FTP](../devlog/ftp.md), [SNMP](../devlog/snmp.md), [DNS](../devlog/dns.md), [smtp](../devlog/smtp.md), [SSL](../devlog/ssl.md), [TLS](../devlog/tls.md) and so on.
   
   
## Data Transfer Over Network   
   
When we're trying to transfer data over network, we've to tell it where its going to go. We use [ip address](../devlog/ip%20address.md)es to get to the system but how does the data know which applications are listening on that system? Thats where Ports come into the picture.   
   
   
- Port numbers can range from 0 to 65,536, you can run services on all of these ports.   
- Ports are categorized into "Well-known" & "Reserved Ports".   
  - Well-known ports range from 0 to 1024.   
    - Examples: [FTP](../devlog/ftp.md) on Port 21, [HTTP](../devlog/http.md) on Port 80 and so on   
- Ephemeral Ports:   
  - Short-lived transport port that is automatically selected from predefined range   
  - Ports 1025 to 65,536   
  - Examples: Running a Web Application locally, such as TiddlyWiki on NodeJs on Port 4000.   
   
### Data Transfer in the real world   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656578336/wiki/ouwxuee31fco6wjridoh.png)   
   
### IPv4 Packets   
   
IPv4 Packets (Packet Header) contain the following information:   
   
   
- Source Address   
  - IP of sender   
- Destination Address   
  - IP of receiver   
- IP Flags   
  - Allows packet fragmentation   
- Protocol   
  - [TCP](../devlog/TCP.md) or [UDP](../devlog/udp.md)   
   
## Ports and Protocols   
   
   
| Port Number      | Service name           | Transport protocol | Description                                                                                                                                                                                                                  |   
| ---------------- | ---------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |   
| 7                | Echo                   | TCP, UDP           | Echo service                                                                                                                                                                                                                 |   
| 20               | FTP-data               |  TCP, SCTP         | File Transfer Protocol data transfer                                                                                                                                                                                         |   
| 21               | FTP                    |  TCP, UDP, SCTP    | File Transfer Protocol (FTP) control connection                                                                                                                                                                              |   
| 22               | SSH-SCP                | TCP, UDP, SCTP     |  Secure Shell, secure logins, file transfers (scp, sftp), and port forwarding                                                                                                                                                |   
| 23               | Telnet                 | TCP                | Telnet protocol—unencrypted text communications                                                                                                                                                                              |   
| 25               | SMTP                   | TCP                |  Simple Mail Transfer Protocol, used for email routing between mail servers                                                                                                                                                  |   
| 53               | DNS                    | TCP, UDP           |  Domain Name System name resolver                                                                                                                                                                                            |   
| 69               | TFTP                   | UDP                | Trivial File Transfer Protocol                                                                                                                                                                                               |   
| 80               | HTTP                   | TCP, UDP, SCTP     | Hypertext Transfer Protocol (HTTP) uses TCP in versions 1.x and 2.  HTTP/3 uses QUIC, a transport protocol on top of UDP                                                                                                     |   
| 88               | Kerberos               | TCP, UDP           | Network authentication system                                                                                                                                                                                                |   
| 102              | Iso-tsap               | TCP                | ISO Transport Service Access Point (TSAP) Class 0 protocol                                                                                                                                                                   |   
| 110              | POP3                   | TCP                | Post Office Protocol, version 3 (POP3)                                                                                                                                                                                       |   
| 135              | Microsoft EPMAP        | TCP, UDP           | Microsoft EPMAP (End Point Mapper), also known as DCE/RPC Locator service, used to remotely manage services including DHCP server, DNS server, and WINS. Also used by DCOM                                                   |   
| 137              | NetBIOS-ns             | TCP, UDP           |  NetBIOS Name Service, used for name registration and resolution                                                                                                                                                             |   
| 139              | NetBIOS-ssn            | TCP, UDP           | NetBIOS Session Service                                                                                                                                                                                                      |   
| 143              | IMAP4                  | TCP, UDP           |  Internet Message Access Protocol (IMAP), management of electronic mail messages on a server                                                                                                                                 |   
| 381              | HP Openview            | TCP, UDP           | HP data alarm manager                                                                                                                                                                                                        |   
| 383              | HP Openview            | TCP, UDP           | HP data alarm manager                                                                                                                                                                                                        |   
| 443              | HTTP over SSL          | TCP, UDP, SCTP     | Hypertext Transfer Protocol Secure (HTTPS) uses TCP in versions 1.x and 2. HTTP/3 uses QUIC, a transport protocol on top of UDP.                                                                                             |   
| 464              | Kerberos               | TCP, UDP           | Kerberos Change/Set password                                                                                                                                                                                                 |   
| 465              | SMTP over TLS/SSL, SSM | TCP                | Authenticated SMTP over TLS/SSL (SMTPS), URL Rendezvous Directory for SSM (Cisco protocol)                                                                                                                                   |   
| 587              | SMTP                   | TCP                | Email message submission                                                                                                                                                                                                     |   
| 593              | Microsoft DCOM         | TCP, UDP           | HTTP RPC Ep Map, Remote procedure call over Hypertext Transfer Protocol, often used by Distributed Component Object Model services and Microsoft Exchange Server                                                             |   
| 636              | LDAP over TLS/SSL      | TCP, UDP           | Lightweight Directory Access Protocol over TLS/SSL                                                                                                                                                                           |   
| 691              | MS Exchange            | TCP                | MS Exchange Routing                                                                                                                                                                                                          |   
| 902              | VMware Server          | unofficial         | VMware ESXi                                                                                                                                                                                                                  |   
| 989              | FTP over SSL           | TCP, UDP           | FTPS Protocol (data), FTP over TLS/SSL                                                                                                                                                                                       |   
| 990              | FTP over SSL           | TCP, UDP           |  FTPS Protocol (control), FTP over TLS/SSL                                                                                                                                                                                   |   
| 993              | IMAP4 over SSL         | TCP                | Internet Message Access Protocol over TLS/SSL (IMAPS)                                                                                                                                                                        |   
| 995              | POP3 over SSL          | TCP, UDP           | Post Office Protocol 3 over TLS/SSL                                                                                                                                                                                          |   
| 1025             | Microsoft RPC          | TCP                | Microsoft operating systems tend to allocate one or more unsuspected, publicly exposed services (probably DCOM, but who knows) among the first handful of ports immediately above the end of the service port range (1024+). |   
| 1194             | OpenVPN                | TCP, UDP           | OpenVPN                                                                                                                                                                                                                      |   
| 1337             | WASTE                  | unofficial         | WASTE Encrypted File Sharing Program                                                                                                                                                                                         |   
| 1589             | Cisco VQP              | TCP, UDP           | Cisco VLAN Query Protocol (VQP)                                                                                                                                                                                              |   
| 1725             | Steam                  | UDP                | Valve Steam Client uses port 1725                                                                                                                                                                                            |   
| 2082             | cPanel                 | unofficial         | cPanel default                                                                                                                                                                                                               |   
| 2083             | radsec, cPanel         | TCP, UDP           |  Secure RADIUS Service (radsec), cPanel default SSL                                                                                                                                                                          |   
| 2483             | Oracle DB              | TCP, UDP           | Oracle database listening for insecure client connections to the listener, replaces port 1521                                                                                                                                |   
| 2484             | Oracle DB              | TCP, UDP           | Oracle database listening for SSL client connections to the listener                                                                                                                                                         |   
| 2967             | Symantec AV            | TCP, UDP           | Symantec System Center agent (SSC-AGENT)                                                                                                                                                                                     |   
| 3074             | XBOX Live              | TCP, UDP           | Xbox LIVE and Games for Windows – Live                                                                                                                                                                                       |   
| 3306             | MySQL                  | TCP                |  MySQL database system                                                                                                                                                                                                       |   
| 3724             | World of Warcraft      | TCP, UDP           | Some Blizzard games, Unofficial Club Penguin Disney online game for kids                                                                                                                                                     |   
| 4664             | Google Desktop         | unofficial         | Google Desktop Search                                                                                                                                                                                                        |   
| 5432             | PostgreSQL             | TCP                | PostgreSQL database system                                                                                                                                                                                                   |   
| 5900             | RFB/VNC Server         | TCP, UDP           | virtual Network Computing (VNC) Remote Frame Buffer RFB protocol                                                                                                                                                             |   
| 6665             | IRC                    | TCP                | Internet Relay Chat                                                                                                                                                                                                          |   
| 6669             | IRC                    | TCP                | Internet Relay Chat                                                                                                                                                                                                          |   
| 6881             | BitTorrent             | unofficial         | BitTorrent is part of the full range of ports used most often                                                                                                                                                                |   
| 6999             | BitTorrent             | unofficial         | BitTorrent is part of the full range of ports used most often                                                                                                                                                                |   
| 6970             | Quicktime              | unofficial         | QuickTime Streaming Server                                                                                                                                                                                                   |   
| 8086             | Kaspersky AV           | TCP                | Kaspersky AV Control Center                                                                                                                                                                                                  |   
| 8087             | Kaspersky AV           | UDP                | Kaspersky AV Control Center                                                                                                                                                                                                  |   
| 8222             | VMware Server          | TCP, UDP           | VMware Server Management User Interface (insecure Web interface).                                                                                                                                                            |   
| 9100             | PDL                    | TCP                | PDL Data Stream, used for printing to certain network printers[1                                                                                                                                                             |   
| 10000            | BackupExec             | unofficial         | Webmin, Web-based Unix/Linux system administration tool (default port)                                                                                                                                                       |   
| 12345            | NetBus                 | unofficial         | NetBus remote administration tool (often Trojan horse).                                                                                                                                                                      |   
| 27374            | Sub7                   | unofficial         | Sub7 default                                                                                                                                                                                                                 |   
| 18006            | Back Orifice           | unofficial         | Back Orifice 2000 remote administration tools                                                                                                                                                                                |   
   
Via - [50 Common Ports You Should Know - GeeksforGeeks](https://www.geeksforgeeks.org/50-common-ports-you-should-know/)
   
   
## Look-into   
   
   
- IPv4/IPv6 Packet Header   
- TCP/UDP Packet Header   
   
See also: [Using nmap to look for open ports](../devlog/Using%20nmap%20to%20look%20for%20open%20ports.md)
   
   
# IPv4 Addressing   
   
The IPv4 address is a 32-bit number that uniquely identifies a network interface on a system. An IPv4 address is written in decimal digits, divided into four 8-bit fields that are separated by periods. Each 8-bit field represents a byte of the IPv4 address. This form of representing the bytes of an IPv4 address is often referred to as the dotted-decimal format.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656592001/wiki/uraeawlkks6yqmy5ci3n.png)   
   
The following figure shows the component parts of an IPv4 address, `172.16.50.56`.   
   
#### Parts of IPv4   
   
   
- **Network part:**      
  The network part indicates the distinctive variety that’s appointed to the network. The network part conjointly identifies the category of the network that’s assigned.   
   
- **Host Part:**      
  The host part uniquely identifies the machine on your network. This part of the IPv4 address is assigned to every host.      
  For each host on the network, the network part is the same, however, the host half must vary.   
   
- **Subnet number:**      
  This is the nonobligatory part of IPv4. Local networks that have massive numbers of hosts are divided into subnets and subnet numbers are appointed to that.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656585458/wiki/yavrzufmne9yunyfearq.png)   
   
   
- Subnet mask defines the network portion   
  - Network portion if binary 1   
  - Host portion if binary 0   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656592063/wiki/gapcxwmkfgyk1pocnobt.png)   
   
# Classes of IP Address   
   
   
- Default subnet mask is assigned by first octet   
  - Classful Mask if using default subnet mask   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656592872/wiki/duckdmgbrvvo2am5hazc.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656593725/wiki/kbyzrh9dfdqxoigaldkq.png)   
   
The subnet mask does not actually contain network or host portion of an IPv4 address, it simply tells where to look for these portions in a given IPv4 address.   
   
**Notice that 127 is skipped between Class A and Class B, it is a reserved block for the loopback address(`127.0.0.1`).**   
   
## Subnet mask   
   
Finally understanding what subnet mask is   
   
For example take two IP addresses and tell if they both can communicate(predict that they’re part of the same network - or share same netowkr ID)   
   
`10.10.10.1` and `10.10.20.16`   
   
Can you tell if they are both part of the same network? You simply CANNOT   
   
Why? Because how is it going to assume what part of this IP tells you the network ID and which portion tells you the host ?   
   
For that we need a subnet mask   
   
For the above IPs lets assume `255.0.0.0` is the subnet mask   
   
Which means(refer to the chart above) that they’re part of the same network and do not need a router to communicate, a switch will do the trick.   
   
We can use Class C subnet mask for Class A and Class B IP address but cannot use Class A and Class B subnet mask for Class C IP address.   
   
Some more examples:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656594629/wiki/hk9tpoxztalbecnkahgl.png)   
   
## Drawbacks of Classful Addressing   
   
   
- **Lack of internal address flexibility**: Large organizations are assigned "monolithic" blocks of addresses that don't match well with the structure of the internal network.   
- **Inefficient use of address space**: The existence of only three block sizes(classes A,B and C) leads to wastage of limited IP address space.   
- **Proliferation of router table entries**: As the internet grows, more entries are required for routers to handle the routing if IP datagrams, which causes performance problems for routers. Attempting to reduce inefficient address space allocation leads to even more router table entries.
   
   
## Routable IPs   
   
   
- Publically routable IP addresses are globally managed by ICANN.   
	- Internet Corporation for Assigned Names and Numbers   
		- ARIN, LACNIC, AFNIC, APNIC and RIPE NCC   
	- Public IPs must be purchased before use through your ISP.   
   
   
## Private IPs   
   
   
- Private IP’s can be used by anyone.   
- Not routable outside your local area network.   
- [NAT](../devlog/NAT.md) allows for routing of private IPs through a public IP.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656595632/wiki/dqv5dipadhxwg6buduxl.png)   
   
## Specialized IPs   
   
   
- Loopback address (`127.x.x.x` range) Home   
	- Refers to the device itself and is used for testing    
	- Most commonly used at `127.0.0.1`   
   
   
- Automatic Private IP Addresses (APIPA)   
	- Dynamically assigned by OS when DHCP server is unavailable and an address has not been assigned.   
	- Range of `169.254.x.x`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656595864/wiki/ialin5xihhskcrxzkger.png)   
   
   
Special address ranges are never assigned by an administrator or DHCP server.
   
   
## Drawbacks of Classful Addressing   
   
   
- **Lack of internal address flexibility**: Large organizations are assigned "monolithic" blocks of addresses that don't match well with the structure of the internal network.   
- **Inefficient use of address space**: The existence of only three block sizes(classes A,B and C) leads to wastage of limited IP address space.   
- **Proliferation of router table entries**: As the internet grows, more entries are required for routers to handle the routing if IP datagrams, which causes performance problems for routers. Attempting to reduce inefficient address space allocation leads to even more router table entries.
   
   
## Classless Interdomain Routing (CIDR)   
   
CIDR is a notation for describing blocks of IP addresses and is used heavily in various networking configurations. IP addresses contain 4 octets, each consisting of 8 bits giving values between 0 and 255. The decimal value that comes after the slash is the number of bits consisting of the routing prefix. This in turn can be translated into a netmask, and also designates how many available addresses are in the block.   
   
Sometimes we want to vary the length of our subnet masks and we don’t want to stick to the standard classes so we use CIDR. It helps optimize the IP space. It uses variable length subnet mask(VLSM).   
   
CIDR (Classless Inter-Domain Routing) -- also known as supernetting -- is a method of assigning Internet Protocol (IP) addresses that improves the efficiency of address distribution and replaces the previous system based on Class A, Class B and Class C networks.   
   
## Resources   
   
   
- [CIDR.xyz](https://cidr.xyz/)   
- [IPv4, CIDR, and VPC Subnets Made Simple! - YouTube](https://www.youtube.com/watch?v=z07HTSzzp3o&t=216s)   
- [What is CIDR block | Easy demo of CIDR | AWS VPC CIDR Demo | Understanding CIDR with AWS VPC Subnet - YouTube](https://www.youtube.com/watch?v=aPW-ZAo09Pg)
   
   
## Look into   
   
   
- [What Is a Network Access Control List (Network ACL)? | Fortinet](https://www.fortinet.com/resources/cyberglossary/network-access-control-list)