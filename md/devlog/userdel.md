---
created: '2021-10-26T00:00:00.000Z'
desc: ''
id: scwvo57inos5x480bcrj2vl
title: userdel
updated: 1652815514934
---
   
Topics::  [linux](../topics/linux.md)   
   
   
---   
   
`userdel` is used to delete a user, it also deletes the group with the same name as the user, if no other user belongs to that group.   
   
   
- Deleting a user   
  - `sudo userdel james` account will be removed but the home dir will stay   
- Deleting a user along with it's home dir   
  - `sudo userdel -r james`   
- If the group `james` was not the primary group of that user, it will not removed by default   
- Other files belonging to `james` will not be deleted, will have to be removed manually   
- Just like [adduser](/not_created.md) for [useradd](../devlog/useradd.md), [Debian](/not_created.md) and [Ubuntu](/not_created.md) have a friendlier command line utility [deluser](/not_created.md) that uses userdel as backend.