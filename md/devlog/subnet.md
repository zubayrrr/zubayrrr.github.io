---
created: 1655350929391
desc: ''
id: 9vmmmhyayk6vi0i7w5cnwjv
title: Subnet
updated: 1656596477742
---
   
**IP Subnet Addressing:**   
   
All Classes of IP networks can be divided into smaller networks called subnetworks (or subnets).   
   
Dividing the major class network is called subnetting. Subnetting provides network administrators with several benefits. It provides extra flexibility, makes more efficient use of network address utilization, and contains broadcast traffic because a broadcast will not cross a router.   
   
Subnets are under local administration. As such, the outside world sees an organization as a single network, and has no detailed knowledge of the organization's internal network structure.   
   
A given network address can be broken up into many subnetworks. For example, 172.16.1.0, 172.16.2.0, 172.16.3.0, and 172.16.4.0 are all subnets of the Class B network 171.16.0.0.   
   
**IP Subnet Mask:**   
   
A subnet address is created by "borrowing" bits from the host field and designating them as the subnet field. The number of borrowed bits is variable and specified by the subnet mask.   
   
The following figure shows how bits are "borrowed" from the host address field to create the subnet address field:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655736057/wiki/hnvqgvajvxuug5jct9aj.png)   
   
Subnet masks use the same format and representation technique as network mask format, the subnet mask has binary 1s in all bits specifying the network and subnetwork fields, and binary 0s in all bits specifying the host field.   
   
The following figure shows a sample subnet mask:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655736067/wiki/cz15tvvibn0kjpyo4zki.png)   
   
Via - [Basic IP Addressing and Troubleshooting Guide](http://penta2.ufrgs.br/trouble/ts_ip.htm)   
   
   
- Each subnet inside a [vpc](/not_created.md) has to have a different set of [ip address](../devlog/ip%20address.md)es.   
   
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