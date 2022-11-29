---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: gck1glk8wmjsg66ewljko7s
title: lshw
updated: 1653305654080
---
   
Topics::  [linux](../topics/linux.md)   
Related::  [[inxi]   
   
   
---   
   
*lshw(list hardware)* is a small Linux/Unix tool which is used to generate the detailed information of the system’s hardware configuration from various files in the */proc* directory. *lshw* can also report exact memory configuration, firmware version, mainboard configuration, CPU version and speed, cache memory configuration, bus speed, etc on DMI-capable x86 or IA-64(Itanium family of 64 microprocessors) system and some PowerPC machine. This command needs root permission to show full information else partial information will be displayed.   
   
**Syntax:**   
   
```bash
lshw [-format] [-options ...]
```
   
   
**Where format can be:**   
   
   
- _-html_: Output hardware tree as HTML.   
- _-xml_: Output hardware tree as XML.   
- _-short_: Output hardware paths.   
- _-businfo_: Output bus information.   
   
## Examples   
   
```
sudo lshw | less
```
   
   
```
sudo lshw -json | less
```
   
   
```
sudo lshw -html > hw.html
```
   
   
```
sudo lshw -short
```
   
   
Single line displaying each disk   
   
```
lshw -C disk -short
```
