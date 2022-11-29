---
created: '2022-05-12T00:00:00.000Z'
desc: ''
id: 05txufwh4u6s1aop2eky199
title: netstat
updated: 1656559732725
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
Netstat is a command-line tool used by system administrators to evaluate network configuration and activity. The term Netstat is results from network and statistics. It shows open ports on the host device and their corresponding addresses, the routing table, and masquerade connections.   
   
Netstat is part of a package named net-tools.   
   
## Display Routing table:   
   
Netstat command shows the routing table detail on the terminal. If you wish to see the routing table, use the –nr flag with Netstat; it shows the kernel routing table in the same way that route does. Use the below command:   
   
```
netstat -nr
```
   
   
Instead of using symbolic address names, the -nr option allows Netstat to print addresses divided by dots   
   
## Display interface statistics:   
   
Using the ‘-i’ flag or option with Netstat will show statistics for the currently configured network interfaces.   
   
```
netstat -i

#or

netstat -ai
```
   
   
If the “–a” flag is also used with “-i”, the command prints all of the kernel interfaces.   
   
## Display Network connection:   
   
To view active or passive sockets, Netstat has a range of options. Active [TCP](../devlog/TCP.md), [UDP](../devlog/udp.md), [RAW](/not_created.md), and Unix socket connections are specified by the –t, –u, –w, and –x options, respectively.   
   
```
netstat -ta
```
   
   
## Display Network Services:   
   
Run the following command to see a list of networks, their current states, and their associated ports:   
   
```
netstat -pnltu
```
