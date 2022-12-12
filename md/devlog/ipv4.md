---
created: 1656585263009
desc: ''
id: d6dakasx29em4cil8uhjy62
title: Ipv4
updated: 1656595275716
---
   
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