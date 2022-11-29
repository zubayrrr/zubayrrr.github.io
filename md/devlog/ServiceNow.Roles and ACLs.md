---
created: 1663409747144
desc: ''
id: hdxt8s5ca4xtqjydlbwnz3u
title: Roles and ACLs
updated: 1663412962622
---
   
Roles are used to grant permissions to groups which contain users.   
   
A role is simply a record in the `sys_user_role` table.   
   
A group may contain 0 or many roles and roles may be part of one or more Access Control Rules(specific access to records).   
   
There are many out-of-the-box roles in ServiceNow.   
   
Popular roles   
   
   
- admin   
- security_admin   
- itil   
- itil_admin   
- impersonator   
- knowledge_admin   
- report_admin   
- catalog_admin   
- asset   
- ecmdb_admin   
   
Check [Base system roles](https://docs.servicenow.com/en-US/bundle/tokyo-platform-administration/page/administer/roles/reference/r_BaseSystemRoles.html) for more info on roles.   
   
## Access Controls   
   
Access controls are what define the actual permissions in the system.   
   
It is a record in the `sys_security_acl` table.   
   
These rules grant access to certain parts of the system.   
   
When creating an ACL you must specify:   
   
- Object and operation(CRUD)   
- Permissions required(Set of Roles or additional conditions)   
- `*` wilcard   
	- May be used in table or field selection which signifies ALL tables or ALL fields.   
- There are thousands of out-of-the-box access control rules that are mapped to the out-of-the-box rules.   
   
   
Access Controls  are assigned to Roles.   
Roles are assigned to Groups.   
Users are assigned to Groups.   
   
## Access Operations   
   
| Operation | Action                        |   
|-----------|-------------------------------|   
| execute   | Run app or script             |   
| create    | Insert records                |   
| read      | Display records               |   
| write     | Update records                |   
| delete    | Remove records                |   
| list_edit | Update records from list view |   
| report_on | Create reports                |   
   
## Access Controls Flowchart   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663410721/wiki/mwoddpezuk7qyoa4oiok.png)   
   
## Access Control Execution   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663410748/wiki/gwti48u17pbokpq6vqih.png)   
   
   
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/7628ca11fef64a0d830e2349c6612970" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>