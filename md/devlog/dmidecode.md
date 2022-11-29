---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: bq9mpfb6cm052t59jj8l1u7
title: dmidecode
updated: 1653318721001
---
   
Topics::  [linux](../topics/linux.md)   
Related::  [top](../devlog/top.md), [free](../devlog/free.md)   
   
   
---   
   
Dmidecode reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard (see a sample output). This information typically includes system manufacturer, model name, serial number, BIOS version, asset tag as well as a lot of other details of varying level of interest and reliability depending on the manufacturer. This will often include usage status for the CPU sockets, expansion slots (e.g. AGP, PCI, ISA) and memory module slots, and the list of I/O ports (e.g. serial, parallel, USB).   
   
> via — [dmidecode](https://www.nongnu.org/dmidecode/)   
   
```
dmidecode -t memory
```
   
   
```
dmidecode -t memory | grep -i size
dmidecode -t memory | grep -i max
```
