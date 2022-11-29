---
category: '2022'
created: 2022-11-10 14:53:42.097000+00:00
id: 33f41767-2790-4247-9dad-0deeeaa21f8a
tags:
- devlog
title: GlideRecordSecure
updated: 2022-11-10 14:53:42.493000+00:00
---
   
   
- GlideRecordSecure is a class inherited from [GlideRecord](../devlog/GlideRecord.md)   
	- It has all the same methods as [GlideRecord](../devlog/GlideRecord.md)   
	- performs ACL checking so we don’t have to use methods like `canRead()`, `canWrite()`, `canUpdate()`, `canDelete()` etc   
- It is used to secure [ServiceNow.Script Includes](../devlog/ServiceNow.Script%20Includes.md) since they can be invoked from anywhere in ServiceNow.   
- It isn’t as important in places like [ServiceNow.Business Rules](../devlog/ServiceNow.Business%20Rules.md) where conditions are already defined or in a table that has ACLs defined.