---
created: '2021-10-29T00:00:00.000Z'
desc: ''
id: b9855u2ordmv6yq1723mj98
title: Troubleshooting for connectivity issues
updated: 1653437730926
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
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