---
created: 1663404088284
desc: ''
id: 9m1hmb0ipc9jv5dxnr2dw9e
title: Users & Groups
updated: 1663404088284
---
   
## Users    
   
A User represents:   
   
   
- A ServiceNow account   
- A record in the `sys_user` table.   
- A user account correlates to one record in the `sys_user` table, users maybe part of 0 or more groups and may have 0 or more roles.   
- Users have a number of out-of-the-box fields and the admins may add more fields to the `sys_user` table.   
- Users may also have delegates.   
	- If an executive is on vacation, their assistants/delegates may approve tasks on their behalf.   
- By default, new users are not part of any groups and have no roles assigned.   
   
## Groups   
   
   
- A group is a record in the `sys_user_group` table.   
- You can think of groups as buckets that hold users who share a common purpose.   
- Roles are assigned to groups and place users in those groups rather than assigning roles directly to the users.   
- Groups may inherit other groups.   
- Groups contain 0 or more roles.   
- Groups are used in the location in ServiceNow; like assignment groups on task records, admin groups on CI records.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663404658/wiki/aemikklkzbu6w7qjddp5.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663404715/wiki/ucrd7u5nex3g3e2ugqsi.png)   
   
## Create a new User   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663408808/wiki/ueddh5ycu5sfs927uqhi.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663408908/wiki/nueehilldqaovwlp76pp.png)   
   
Add User to Group   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663408931/wiki/bcghs9tabdc1ljh9shi9.png)   
   
Add Delegate   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663409078/wiki/xhxtf7djqes8ubug1q3i.png)   
   
## Create a new Group   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663409189/wiki/ttcrbviim9dugez2s8fh.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663409321/wiki/ozh8nngwxub1hhvxkbpn.png)