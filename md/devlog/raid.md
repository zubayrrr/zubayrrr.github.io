---
created: 20211006095319896
desc: ''
id: v3dpyitp2w8cu33k2zripsf
title: RAID
updated: 1652622339362
---
   
Redundant Array of Independent Disks   
   
Allows multiple disks to work together for fault tolerance and performance and makes it appear a single logical disk for the OS. Often found in high-end desktops and certainly in servers.   
   
A group of physical or virtual disks working together   
   
   
- Increased performance and fault tolerance   
- Disks should be hot-swappable   
   
#### Hardware RAID uses a physical RAID controller (either embedded on motherboard as firmware or comes as an add-on)   
   
#### Software RAID manages logical disks using the OS   
   
   
---   
   
RAID 0   
   
   
- Striped Volume - writing data across two disks   
   
RAID 1   
   
   
- Mirrored Volume - writing a copy to a secondary disk   
   
RAID 5   
   
   
- Striping with Distributed Parity   
   
RAID 10   
   
   
- RAID 1 + RAID 0   
- Combines mirroring and striping   
- Requires four disks   
   
RAID 50   
   
   
- RAID 5 + RAID   
- Combines distributed parity and striping   
- Requires six disks