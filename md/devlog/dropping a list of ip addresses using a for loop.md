---
created: 1653139719755
desc: ''
id: h2nd1ugulcavl8zrn3d054x
tags:
- tidbits
title: Dropping a List of IP addresses Using a For Loop
updated: 1653140104813
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Dropping packets from a list of IPs   
   
```bash
#!/bin/bash

DROPPED_IPS="8.8.8.8 1.1.1.1 10.10.10.1"
for ip in $DROPPED_IPS
do
  echo "Dropping packets from $ip"
  iptables -I INPUT -s $ip -j DROP
done
```
   
   
Supply list of IPs from a txt file   
   
```bash
#!/bin/bash

for ip in $(cat ips.txt)
do
  echo "Dropping packets from $ip"
  iptables -I INPUT -s $ip -j DROP
done
```
