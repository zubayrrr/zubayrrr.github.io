---
created: 20211010112527180
desc: ''
id: 5xbq8dqh6wbqd14aqyn863v
title: ping
updated: 1653437730947
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
The Ping tool is used to test whether a particular host is reachable across an IP network. A Ping measures the time it takes for packets to be sent from the local host to a destination computer and back. The Ping tool measures and records the round-trip time of the packet and any losses along the way.   
   
`ping` works by sending [ICMP](../devlog/icmp.md) echo request package to the specified destination [ip address](../devlog/ip%20address.md) and waits for a reply. When the destination receives the package it will respond back with an [ICMP](../devlog/icmp.md) echo reply.   
   
## Example   
   
   
- `ping ubuntu.com` sends echo request packets continiously   
  - `ping` will resolve domain into an address(public [ip address](../devlog/ip%20address.md)).   
  - An IP Address can be set to multiple domain names and ping performs reverse DNS resolution asking the [dns](../devlog/dns.md) configured on the system what the domain of the IP is. The DNS Server will respond back with one domain.   
  - Add `-n` to prevent ping from doing reverse DNS lookup.   
- If you ping an IP Address that is down you'll get no response.   
- To specify number of echo request packets, `ping -c 4 ubuntu.com` will send 4 packets.   
- `icmp_seq` will the number of the packet, you can use this to detect issues with bad routing.   
- `ttl` time to leave value in the received packets and is normally the number of hops nand [router](../devlog/router.md)s between the source and the destination.   
- `time` ping time measured in milliseconds, round trip time, `rtt`, less is better. time less than 30 excellent, 30-50 is avg, 50-100 slow, value greater than 100 probably means you cannot run real-time applications such as [VoIP](/not_created.md) or Video calls.   
- By default `ping` waits for 1 second before it sends a packet, we can change this interval with `-i` option   
  - `ping -i 0.4 -c 5 google.com`   
  - Only the superuer can set this value to less than 0.2 seconds   
- `q` option to just get the summary   
- Send packets witn incremental `ttl` value to discover the path a packet takes. When a router receives a packet with `ttl` value as 1, it'll discard the packet and notify the source with an ICMP time exceeded packet. So a packet with TTL value 1 really means discovering the first router towards the destination.   
  - `ping -t 1 -c 3 -n ubuntu.com` first router   
  - `ping -t 2 -c 3 -n ubuntu.com` second router   
  - `ping -t 2 -c 3 -n ubuntu.com` third router and so on   
   
### Troubleshooting for connectivity issues   
   
   
- `route -n` to get default gateway   
- `ping defaultGW` if the ping doesn't work, theres a problem with LAN, maybe unauthenticated to the wireless access point or you don't have the right IP Address set.   
- ping a public IP Address on the internet, something stable like public DNS Server of Google (8.8.8.8) or public DNS Server of Cloudflare (1.1.1.1)   
  - ping 8.8.8.8   
  - ping 1.1.1.1   
  - If this doesn't work, theres an internet connectivity issue, check router configuration or check with [ISP](/not_created.md).   
- ping an inter domain, something like google.com   
  - If this doesn't work, you've a DNS issue, check that you're correct [dns](../devlog/dns.md) and theres nothing filtering the packets, probably a configuration error related to DNs on your side or the DNS server is down.   
  - change the DNS Server to 8.8.8.8 and try again.