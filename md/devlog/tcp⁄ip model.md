---
created: 20210926141245140
desc: ''
id: q92tfbbhyglmyk3jdtx5vm5
title: TCP⁄IP Model
updated: 1656581236010
---
   
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