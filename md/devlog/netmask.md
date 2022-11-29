---
created: 20211029075736628
desc: ''
id: yaz8aekqoejlmuhhyj4v63y
title: netmask
updated: 1652817053242
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
A Netmask is a 32-bit "mask" used to divide an IP address into subnets and specify the network's available hosts. In a netmask, two bits are always automatically assigned. For example, in 255.255.225.0, "0" is the assigned network address. In 255.255.255.255, "255" is the assigned broadcast address. The 0 and 255 are always assigned and cannot be used.   
   
Netmask defines how "large" a network is or if you're configuring a rule that requires an IP address and a Netmask, the Netmask will signify to what range of the Network the rule will apply to.   
   
Sometimes you will see that a Netmask is defined by one number, e.g., 24. This number is the length of the Netmask in bits:   
   
> —via [What is a Netmask? - Teltonika Networks Wiki](https://wiki.teltonika-networks.com/view/What_is_a_Netmask%3F)