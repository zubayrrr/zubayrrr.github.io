---
category: '2022'
created: 2022-11-08 16:07:18.976000+00:00
id: 8ba6fe8d-a43f-45c7-9a25-73b693a71e4a
tags:
- devlog
title: Dot-Walking
updated: 2022-11-08 16:07:19.320000+00:00
---
   
[ServiceNow](../devlog/ServiceNow.md) is based on a RDBMS, we use primary and foreign keys to form relationships between tables.   
   
`starting_table.reference_field.reference_field`   
   
## Example   
   
For a specific <u>incident</u>, find the <u>location</u> of a <u>caller</u>. This will include three separate tables inside ServiceNow.    
   
   
- Incident   
- `sys_user`   
- `cmn_location`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1668008447/wiki/goykwlanosuoiepketns.png)   
   
```javascript
var incidentGR = new GlideRecord("incident");
incidentGR.get("<incident-sys-id>");
gs.print(incidentGR.caller_id.location.name);
```
