---
category: '2022'
created: 2022-11-04 13:42:42.453000+00:00
id: 0be51961-21f9-4629-9e82-217d62819dc3
tags:
- devlog
- tidbits
title: Reinstall Python Packages
updated: 2022-11-04 13:42:42.909000+00:00
---
   
Topics:: [Python](/not_created.md)   
   
   
---   
   
Re-install all your Python packages that you accidentally uninstalled because you’re an idiot.   
   
```bash
sudo apt reinstall $(dpkg-query -W \*python\* | awk '$2 { print $1 }')    
```
