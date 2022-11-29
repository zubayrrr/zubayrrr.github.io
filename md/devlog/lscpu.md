---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: cvbp3oosvmmr6n0mhrl75vw
title: lscpu
updated: 1652815757405
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
lscpu is a command-line utility to display information about the CPU architecture. It reads the CPU architecture information from **sysfs** and **/proc/cpuinfo** files and prints in the terminal. The information includes the number of CPUs, threads, cores, sockets, and Non-Uniform Memory Access (NUMA) nodes. It also displays CPU caches and cache sharing, family, model, bogoMIPS, byte order, and stepping.   
   
```
lscpu -[options]
```
   
   
Some available options in lscpu command are:   
   
   
- **-a**: print both online and offline CPUs   
- **-b**: print online CPUs only   
- **-c**: print offline CPUs only   
- **-e**: print in an extended readable format   
- **-p**: print CPU information in parsable format   
   
## Examples   
   
```
lscpu | grep -i mhz
```
   
   
```
lscpu -J
```
   
   
You can use `-e` or `--extended` option to print the CPU information in an extended human-readable format.   
   
```
lscpu -e
```
