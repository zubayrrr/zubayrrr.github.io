---
created: '2022-05-13T00:00:00.000Z'
desc: ''
id: 2gmedegxow41s8s2ek1ccra
title: inxi
updated: 1652815757443
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
It is a free and open source system information tool that can be used to identify and show information about various hardware components present in your Linux PC. `inxi` works on all major Linux distributions and it can be especially helpful in resolving hardware issues and optimizing performance of applications that target specific sets of hardware requirements.   
   
## Examples   
   
```
inxi --full
```
   
   
“-C” and “-G” switches for producing information about CPU and GPU units respectively   
   
```
inxi -C -G
```
   
   
```
inxi -full --output json --output-file "$HOME/info.json"
inxi -full --output xml --output-file "$HOME/info.xml"
```
   
   
```
inxi --recommends
```
