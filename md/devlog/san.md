---
caption: Storage Area Network
created: 20210927120051080
desc: ''
id: c6l91ma2iizawnkxiioocm9
title: SAN
updated: 1653437514197
---
   
[Network External Storage](../devlog/network%20external%20storage.md)   
   
Storage Area Network uses specialized equipment that deals only with disk [IO](../devlog/io.md) over a specialized storage network.   
   
   
- Hosts access remote network storage as opposed to [DAS](../devlog/das.md)   
- Host book device can exist on a SAN   
- Dedicated network for disk I/O traffic over a network (nothing to do with [tcp⁄ip model](../devlog/tcp%E2%81%84ip%20model.md) traffic)   
- Fibre Channel (FC)   
- Fibre Channel over Ethernet (FCoE)   
- iSCSI