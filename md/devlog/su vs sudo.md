---
category: '2022'
created: 2022-11-23 21:30:54.022000+00:00
id: 7a0de8e2-a406-402f-bc18-81ce501221aa
tags:
- devlog
title: Su Vs Sudo
updated: 2022-11-23 21:30:54.590000+00:00
---
   
Topics:: [Linux](../topics/linux.md)   
   
   
---   
Both su and sudo elevate privileges assigned to the current user. The main difference between the two is that **su requires the password of the target account, while sudo requires the password of the current user**. Therefore, it is much safer to use sudo since it doesn't include exchanging sensitive information.