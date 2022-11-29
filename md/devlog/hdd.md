---
caption: Hard Disk Drives
created: 20211006111646144
desc: ''
id: mhmqfudlq6zg7v2nadq14u7
title: HDD
updated: 1652622336936
---
   
   
- Contain a series of spinning rigid metal platters, one on top of the other, very close but not touching.   
- Read and write heads must move over spinning platters to read and write.   
- Uses power to driver motors which results in noise and heat.   
- They're magnetic drives   
- Internal interface - [PATA](../devlog/pata.md), [SATA](/not_created.md), [SCSI](/not_created.md)   
- External interface - [USB](../devlog/usb.md), eSATA, [SCSI](/not_created.md), SAS   
   
### Magnetic Drive Characteristics   
   
   
- Rotational Speed - 5,400 RPM, 7,200 RPM, 10,000 RPM, 15,000 RPM (faster is better).   
- Pysical Sizes - 2.5", 3.5" - Eg: SATA 2.5, SATA 3.5   
   
### HDD Security   
   
#### HDD Password   
   
   
- Password must be entered on boot up   
- Password is stored with the disk firmware   
   
#### Trusted platform module   
   
   
- TPM   
- Stored disk encryption keys   
- Verifies machine startup integrity   
   
#### LoJack   
   
   
- Tracking mechanism for stolen laptops   
- Can be enabled from BIOS/UEFI - sometimes also stored on HDD (in form of software)