---
created: 1665628081859
desc: ''
id: sm1mkoil14qc14i3p1yewcm
title: Ip Address
updated: 1665628081859
---
   
Related: [subnet](../devlog/subnet.md)   
   
   
---   
   
IP Address is basically how computers(servers) talk to each other on the internet. IP Address is provided by a Network Interface of a computer, these are public IP Addresses. IP Address are made user friendly by using a [dns](../devlog/dns.md)that converts a domain name to an IP Address.   
   
**IP Address Components:**   
   
Like other network layer protocols, the IP addressing scheme is integral to the process of routing IP data through an internetwork.   
   
Each host on a TCP/IP network is assigned a unique 32-bit logical address. The IP address is divided into two main parts; the Network Number and the Host Number.   
   
The network number identifies the network and must be assigned by the Internet Network Information Center (InterNIC) if the network is to be part of the Internet.   
   
The host number identifies a host in the network and is assigned by the local network administrator.   
   
**IP Address Format:**   
   
The 32-bit IP address is grouped 8 bits at a time, each group of 8 bits is an octet. Each of the four octets are separated by a dot, and represented in decimal format, this is known as dotted decimal notation. Each bit in an octet has a binary weight (128, 64, 32, 16, 8, 4, 2, 1). The minimum value for an octet is 0 (all bits set to 0), and the maximum value for an octet is 255 (all bits set to 1).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655735910/wiki/wtzdd2lbx2pixujmqqx0.png)   
   
**IP Address Classes:**   
   
IP addressing supports three different commercial address classes; Class A, Class B, and Class C.   
   
In a class A address, the first octet is the network portion, so the class A address of, 10.1.25.1, has a major network address of 10. Octets 2, 3, and 4 (the next 24 bits) are for the hosts. Class A addresses are used for networks that have more than 65,536 hosts (actually, up to 16,581,375 hosts!).   
   
In a class B address, the first two octets are the network portion, so the class B address of, 172.16.122.204, has a major network address of 172.16. Octets 3 and 4 (the next 16 bits) are for the hosts. Class B addresses are used for networks that have between 256 and 65,536 hosts.   
   
In a class C address, the first three octets are the network portion. The class C address of, 193.18.9.45, has a major network address of 193.18.9. Octet 4 (the last 8 bits) is for hosts. Class C addresses are used for networks with less than 254 hosts.   
   
Via — [Basic IP Addressing and Troubleshooting Guide](http://penta2.ufrgs.br/trouble/ts_ip.htm)   
   
   
---   
   
## Structure of an IP Address   
   
IP Addresses are written in decimal dotted notation.   
   
`192.168.0.1`   
   
Each part of the IP address is a binary octet.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656322930/wiki/gruxal4tsobjfhxdkw00.png)   
   
This is important for [subnet](../devlog/subnet.md)ting.   
   
## Networks and Hosts   
   
Every IP address has a Network ID and a Host ID   
   
Network ID will remain same for every computer on this network.   
   
Host ID will be unique for every computer on this network.   
   
Subnet masks tells us which part is the Network ID and which is Host ID.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656323194/wiki/glrh3blvpzga1d4itquu.png)   
   
When we have `255` (all the 8 bits are 1) is where we essentially have a bit that is a `1`. It represents a Network ID.   
   
Last octet in the orange box is the Host ID, every bit in a subnet mask that is a `0` means there are values that can be assigned to host.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656323419/wiki/vsvc0stwao9rrbyuib2e.png)   
   
Lets say you’ve a network with several computers, they each will have different host IDs but same network ID.   
   
## Classes of IPv4 Address   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656323639/wiki/gnfsubay6bnavdg3spkv.png)   
   
**Private IP address range**   
   
Reserved for private/internal use in an organization according to IETF RFC-1918.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656323694/wiki/piorhozhal6mgghcyo24.png)   
   
   
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
   
   
   
---   
   
## How is an [ip address](../devlog/ip%20address.md) assigned?   
   
Apparently using some [dhcp](../devlog/dhcp.md) magic, [router](../devlog/router.md) assigns an [IP address](../devlog/ip%20address.md) to any computer/thing that connects to it.   
   
Why is that most of the IP address start from `192.168.1.204` when they each of the octet can be anywhere between 0.255?   
   
It is because of subnet mask. If your subnet mask is `255.255.255.0` it'll match one on one with `192.168.1.204` the first three of the IP address will always remain the same IN YOUR NETWORK.   
   
The last octet or the number in subnet if it is 0 - it basically tells us that the last octet can be whatever you want (as long as it is between 0-255)   
   
The first three octets are NETWORK ID - the last octet is HOST ID   
   
HOST ID will change based on the device connected.   
   
When a networks wants to talk to something that is not on the same network - it takes the help of Default Gateway aka Router.   
   
You cannot use `192.168.1.0` it is the NETWORK ADDRESS.   
   
OR   
   
You cannot use `192.168.1.255` it is the BROADCAST ADDRESS. When you send something to last IP Address in a network, it tells it to everyone in the network.   
   
OR   
   
You cannot use `192.168.1.1` because it's the Router's address(Default Gateway)   
   
In total you can `253` addresses.   
   
   
---   
   
Your IP Address is the size of 32 bits, 4 bytes(8 bits = 1 byte). Hence four binary octets.   
   
Powers of 2 chart is utilized to convert binary to decimal.   
   
8 Bit Octet Chart   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656331702/wiki/npacf0svnom9sisa86sd.png)   
   
## Resources   
   
   
- [what is an IP Address? // You SUCK at Subnetting // EP 1 - YouTube](https://www.youtube.com/watch?v=5WfiTHiU4x8)