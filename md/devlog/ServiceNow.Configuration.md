---
created: 1665628082253
desc: ''
id: 9euxrud3pcm7wro7d7ztwze
title: Configuration
updated: 1665628082253
---
   
## Configuration Management   
   
> “Configuration Management is a process that tracks all of the individual **Configuration Items** (CI) in an IT system which may be as simple as a single server, or as complex as the entire IT department.”   
   
   
- CIs are records in the `cmdb_ci` table with hundreds of extending tables.   
- Hundreds of out-of-box [CMDB](../devlog/CMDB.md) tables.   
- Each CI class has it’s own table which allows us to form relationships.   
- CIs may have only a few relationships or they may have many relationships.   
- They’re connected to one another through **configuration relationships**.   
  - “\_**\_ service is supported by \_\_** server/service” (downstream)   
  - “\_**\_ service supports \_\_** server/service” (upstream)   
- Mature [CMDB](../devlog/CMDB.md)s support complex Dependency Views map which are visual maps that show all the relationships and incidents related to CIs.   
- CMDBs also help in troubleshooting.   
- Granularity of a CMDB varies by maturity.   
- Automated tools like [Discovery](https://docs.servicenow.com/en-US/bundle/tokyo-it-operations-management/page/product/discovery/reference/r-discovery.html)/ [Microsoft Endpoint Manager or SCCM](https://www.microsoft.com/en-us/security/business/microsoft-endpoint-manager) can also be used.   
   
## Configuration Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665587517/wiki/ngotpqgzkqf9wbrjdjcn.png)   
   
Configuration Application contains MANY modules — more than any other application. Nearly all of the out of the box classes(categories) have their own modules.   
   
## Application Servers   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665587645/wiki/bca0cgfkgm9icyoq9ig6.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665587676/wiki/m3zkhud1fi6ek41rrfao.png)   
   
Form View of a CI   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665587724/wiki/oli5e4arwdmer1pst8my.png)   
   
## Servers   
   
Records here represents more of physical servers as opposed to the abstraction of that application server.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665587806/wiki/d3kcyvezskm9yzxyxauf.png)   
   
## CI Class Manager   
   
Hierarchy of different CI classes and how they’re configured.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665588070/wiki/strwo9rjofgw1wpavk4k.png)   
   
## Misc   
   
   
- CMDB Groups   
- CMDB Query Builder   
- Health Preferences   
- CMDB Reports   
- CMDB Remediations   
- Business Services   
- Relatinships   
- CI Identifiers   
  - Each has it’s own table