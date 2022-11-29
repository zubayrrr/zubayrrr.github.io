---
created: 1665628082282
desc: ''
id: d00mmullx5lkxp6dh05k8f4
title: Incident
updated: 1665628082282
---
   
> “The goal of Incident Management is to restore normal service operation as quickly as possible, while minimising impact to business operations and ensuring quality is maintained.” — ServiceNow Docs   
   
It is used for logging incidents, it is the most popular application of ServiceNow platform. Any user create an incident(record an incident table). You can classify incidents by **impact** and **urgency** (fields used to calculate priority).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665496173/wiki/cvltlxv7ym7wydpwft9w.png)   
   
## [Incident Management](../devlog/Incident%20Management.md) Features   
   
   
- Incidents may be created from different triggers such as “Create New” module/option under “Incidents” application, [ServiceNow.Service Portal](../devlog/ServiceNow.Service%20Portal.md)(via Incident Record Producer), email, different integrations.   
- There are many out-of-box configurations that can be applied to Incidents application. Modifying contextual search, data lookups.   
- There are a number of related records on the Incident form.   
- Incident Management also utilises the built-in email/SMS notification system.   
- It also leverages [ServiceNow.SLAs](../devlog/ServiceNow.SLAs.md)   
   
   
---   
   
## Incident Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665498370/wiki/x7bxtcm392dqbafmphht.png)   
   
## Incident Form   
   
The “New Record” Incident form.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665498481/wiki/ty8cy8mywbdhy1k54xbh.png)   
   
### Number Maintenance   
   
“Number” field’s dictionary entry   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665499427/wiki/oeanuuevollrljydo2fq.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665499602/wiki/xgkj03sevtaf1qfqpq47.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665499620/wiki/humixm7al0nbzhpvv7im.png)   
   
### Caller   
   
The caller field is a reference field to a `sys_user` table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665500069/wiki/e6i9cwk2licriezfnq4r.png)   
   
Column label doesn’t always match the column name.   
   
It references user table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665500891/wiki/karhhykyqtyao0d2zic9.png)   
   
## Dependent field   
   
The “subcategory” field depends on “category” field for contextual values.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665501117/wiki/eprohqrqbmytqlkzbufw.png)   
   
### Service   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665501410/wiki/nvzxjr1rir84sydwo2tq.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665501580/wiki/dzfdfyjg8t0zxtctdqlh.png)   
   
### Reference qualifier   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665502182/wiki/oc60595d6ae2sox9w9zq.png)   
   
## Priority Data Lookups (Matrix)   
   
This logic can be modified by an Admin.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665502631/wiki/meuyglzj0oyqnddopbgx.png)   
   
## Contextual Search   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665502836/wiki/zws3x71yxrahxhhyawgn.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665502879/wiki/irqnyql0susxn0nafiug.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665502964/wiki/tj3c2skfgddsob3i79mv.png)