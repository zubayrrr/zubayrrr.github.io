---
created: '2021-10-29T00:00:00.000Z'
desc: ''
id: pjbeze05otspq0j7j48beqp
title: DNS
updated: 1656342034486
---
   
Topics::  [networking](../topics/networking.md),[linux](../topics/linux.md)   
   
   
---   
   
   
- Domain Name Service operates on [Port 53](/not_created.md)   
- Hierarchical decentralized naming system for computers, services, or other resources connected to the internet or a private network.   
- Converts domain names to [ip address](../devlog/ip%20address.md)es   
   
   
- On the latest version of Ubuntu, the DNS is under the control of [systemd-resolve](/not_created.md) [daemon](../devlog/daemon.md).   
- A service that provides DNS name resolution to local services and applications and can be configured with [netplan](../devlog/netplan.md), the default network management tool on Ubuntu.   
- To display the DNS server used by the system:   
  - `systemd-resolve --status`   
   
   
---   
   
The Domain Name System (DNS) turns domain names into IP addresses, which browsers use to load internet pages. Every device connected to the internet has its own IP address, which is used by other devices to locate the device.   
   
In the first step DNS resolver, also called recursive resolver designed to receive DNS queries from a web browser and other applications. The resolver receives a hostname, for example, **www.example.com**, and is responsible for tracking down the IP addresses for that hostname.   
   
After that root server is translating human-readable hostname into IP addresses. There are 13 logical root servers worldwide, denoted by letter A through M controlled by Cogen, the University of Maryland, and the U.S arm lab. The TLD nameserver takes the domain provided in the query and provides the IP of an authoritative name server. The authoritative name server takes the domain name and subdomain, and it returns the correct IP address to the DNS resolver.   
   
## DNS Records   
   
   
- [Why Do Some Websites Start With WWW1? (Not WWW) - YouTube](https://www.youtube.com/watch?v=8Fq-hsGYS-8)