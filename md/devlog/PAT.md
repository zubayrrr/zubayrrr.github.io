---
created: 1656339880759
desc: ''
id: pusng10ldrmh1va6q7rn1uf
title: PAT
updated: 1656339889533
---
   
Topics::  [networking](../topics/networking.md)   
   
   
---   
   
Port Address Translation (PAT) is an extension of Network Address Translation (NAT) that permits multiple devices on a LAN to be mapped to a single public IP address to conserve IP addresses.   
   
PAT is similar to port forwarding except that an incoming packet with destination port (external port) is translated to a packet different destination port (an internal port). The Internet Service Provider (ISP) assigns a single IP address to the edge device. When a computer logs on to the Internet, this device assigns the client a port number that is appended to the internal IP address, giving the computer a unique IP address.   
   
If another computer logs on the Internet, this device assigns it the same public IP address, but a different port number. Although both computers are sharing the same public IP address, this device knows which computer to send its packets, because the device uses the port numbers to assign the packets the unique internal IP address of the computers.   
   
— via [Port Address Translation](https://www.cisco.com/assets/sol/sb/RV320_Emulators/RV320_Emulator_v1-1-0-09/help/Setup13.html)