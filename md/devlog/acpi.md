---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: psmspnhje8fsk8atyi2dmyt
title: acpi
updated: 1653305966434
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**acpi** command is used to display the battery status and other ACPI information. It displays the information from the /[proc](../devlog/proc.md) or the /[sys](/not_created.md) filesystem, such as battery status or thermal information.   
   
## Examples   
   
**-b | –battery** : It displays the battery information.   
   
```
acpi -bi
```
   
   
**-V | –everything** : It is used to show every device, overrides above options.   
   
```
acpi -V
```
   
   
**-p | –proc** : It uses the old /proc interface, default is the new /sys one.