---
created: 20211008082949492
desc: ''
id: i5tq42jsqq76e5c3b57gwy7
title: Storage and RAID Issues
updated: 1652622340543
---
   
   
- Storage media does not last forever - back up your data\!   
- HDDs have mechanical components; they WILL probably fail sooner than SSDs.   
- Storage issues can be software or hardware. (file system)   
   
### Common Storage-related Symptoms   
   
   
- Failure to read or write to disk (is this a permissions issue or if the file system has any issues? or if the disk is unable to read/write from certain sectors).   
- Clicking noise - imminent failure   
- Slower than usual disk performance   
- Disk driver not recognized (usually on start up)   
- OS not found (corruption with OS boot files)   
- RAID not found (software or hardware RAID controller)   
   
### Self-Monitoring Analysis and Reporting Technology   
   
   
- S.M.A.R.T   
- Disk driver firmware   
- Used with server and disk storage arrays   
- Predicts imminent HDD failure   
- Backup data   
   
### Solving Storage-related Issues   
   
   
- RAID Controller diagnostics - either from BIOS, if its an addon you might have to press a certain key on startup to trigger diagnostics (eg: CTRL + G for Intel).   
- Replace failed disks (in case of clicking noise)   
- Test network storage (check connectivity, permissions, network congestion).   
- OS disk volume diagnostics.   
- Ensure cables are plugged in   
- Software based Disk Scanning; eg: SpinRite