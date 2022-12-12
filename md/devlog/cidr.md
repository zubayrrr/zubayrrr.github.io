---
created: 1656168061297
desc: ''
id: h75m1yelgfwk39wqm1ep89z
title: CIDR
updated: 1659799487438
---
   

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