---
created: 1655889024932
desc: ''
id: z1szfep23mzeolyvhmcpb2u
tags:
- tidbits
title: Wget Hacks
updated: 1655889609594
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
**Change user-agent**   
   
Me: [wget](../devlog/wget.md) [URL]   
Server: 403 FORBIDDEN   
Me: wget -U Mozilla/5.0 [URL]   
Server: 200 OK   
   
Via - [(Ryan Castellucci on Twitter](https://twitter.com/ryancdotorg/status/1539168895059349504)   
   
[`wget -U Googlebot` is like multipass for rate limiting](https://twitter.com/ryancdotorg/status/1539168895059349504)