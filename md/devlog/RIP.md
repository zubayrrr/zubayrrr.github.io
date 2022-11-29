---
created: 1656504907504
desc: ''
id: 47kqarif53fgm4mn91r2kcg
title: RIP
updated: 1656505378448
---
   
Routing Information Protocol (RIP) is a dynamic routing protocol that uses hop count as a routing metric to find the best path between the source and the destination network. It is a distance-vector routing protocol that has an AD value of 120 and works on the Network layer of the OSI model. RIP uses port number 520.   
   
Hop Count   
Hop count is the number of routers occurring in between the source and destination network. The path with the lowest hop count is considered as the best route to reach a network and therefore placed in the routing table. RIP prevents routing loops by limiting the number of hops allowed in a path from source and destination. The maximum hop count allowed for RIP is 15 and a hop count of 16 is considered as network unreachable.   
   
Features of RIP   
   
1. Updates of the network are exchanged periodically.   
2. Updates (routing information) are always broadcast.   
3. Full routing tables are sent in updates.   
4. Routers always trust routing information received from neighbor routers. This is also known as Routing on rumors.