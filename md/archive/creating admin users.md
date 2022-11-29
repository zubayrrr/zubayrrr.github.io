---
created: '2021-10-26T00:00:00.000Z'
desc: ''
id: qh05nhekoydzi8s33m16o05
tags:
- tidbits
title: Creating Admin users
updated: 1653683844830
---
   
## Creating Admin Users   
   
   
- A user has to be added to the [sudo](../devlog/sudo.md) [group](/not_created.md) or the `sudoer file` inorder for them to use `sudo` privileges, [usermod](../devlog/usermod.md) can be used to achieve this.   
  - `sudo usermod -aG sudo james`