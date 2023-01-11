---
category: '2023'
created: 2023-01-10 15:55:54.276000+00:00
id: 89bb0a23-d7e8-4706-80e7-caf34c2e891e
tags:
- devlog
title: Password Protect External Storage In Linux
updated: 2023-01-10 15:55:54.676000+00:00
---
   
Topics:: [Linux](../topics/linux.md)   
   
   
---   
   
To password protect an external hard drive on Linux, one can use the Linux Unified Key Setup (LUKS) encryption system<sup class="text-zinc-500"><a href="https://opensource.com/article/21/3/encryption-luks" target="_blank" rel="noopener noreferrer">[1]</a></sup>. This involves finding the drive, clearing it, formatting it for LUKS and then opening the LUKS volume<sup class="text-zinc-500"><a href="https://opensource.com/article/21/3/encryption-luks" target="_blank" rel="noopener noreferrer">[1]</a></sup>. To do this, open Disks from the Application menu<sup class="text-zinc-500"><a href="https://www.technewstoday.com/how-to-password-protect-external-hard-drive" target="_blank" rel="noopener noreferrer">[2]</a></sup>, select the drive and click 'Unlock' to enter a password<sup class="text-zinc-500"><a href="https://superuser.com/questions/1576354/protecting-documents-on-external-hdd" target="_blank" rel="noopener noreferrer">[3]</a></sup>. It is not possible to password protect a drive without encryption<sup class="text-zinc-500"><a href="https://www.linuxquestions.org/questions/linux-hardware-18/password-protect-external-hard-drive-4175693571" target="_blank" rel="noopener noreferrer">[4]</a></sup>.