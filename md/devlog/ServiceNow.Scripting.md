---
category: '2022'
created: 2022-11-04 13:20:29.281000+00:00
id: 1a129f0f-62d5-4089-a690-a74cc130a1c2
tags:
- devlog
title: Scripting
updated: 2022-11-04 13:20:29.609000+00:00
---
   
> [!info]   
> The ServiceNow Glide Class exposes JavaScript APIs that enable you to conveniently work with tables using scripts. Using the Glide APIs, you can perform database operations without writing SQL queries, display UI pages and define UI actions.   
   
**When is scripting necessary?**   
   
   
- Follow the 80/20 rule   
- Only use scripting when you cannot accomplish the same with other options such as UI Policies, Workflows, New tables and fields.   
- Scripting is required for:   
	- Integrations   
	- Complex business rules   
	- Client scripts   
	- UI Actions   
	- Complex transform maps   
	- Serivce Portal   
	- Custom Apps   
   
**Client Side VS Server Side**   
   
| Client                          | Server                 |   
|:------------------------------- |:---------------------- |   
| User’s browser                  | ServiceNow data center |   
| Makes request                   | Returns response       |   
| Access to:                      |                        |   
| `current` form, fields & values | Database               |   
| UI elements(DOM)                |                Server-side APIs        |   
| Client-side APIs                | Script includes                       |   
   
The time it takes for a packet to leave the client and reach ServiceNow data center and return with a response is called a **Round Trip Time**.   
   
The programming language developers use on the ServiceNow platform is [languages.javascript](../devlog/languages.javascript.md).   
   
Usually on server-side [Nodejs](../devlog/Nodejs.md) as runtime environment for executing Javascript but SNOW uses [Mozilla Rhino](../devlog/Mozilla%20Rhino.md).   
   
## Scripts - background   
   
It is similar to a browser’s console. You can run Javascript using SNOW’s Scripts - background feature. You’ve access to SNOW APIs with this. They should be used with caution due to performance impacts and possible data loss.   
   
## ServiceNow Studio   
   
   
- It is an IDE used for development in SNOW.   
- Studio is only available for scoped applications and cannot be used in the **Global** scope.   
- It is a one stop shop for all configuration records.   
   
## Misc   
   
   
- Variable naming conventions:   
	- `hello_world` - underscores    
	- `helloWorld` - Camel case   
- The `sys_id`    
	- 32 character GUID   
	- Every record in the system has one   
- Field display value VS field value   
	- Most fields are actually objects, not strings.   
	- Use `getDisplayValue()` for accessing a field’s display value.   
   
```javascript
var field = {
	value: 'help_desk',
	displayValue: "Help Desk"
}
```
   
   
   
---   
   
## Scripting Locations   
   
   
- [ServiceNow.Business Rules](../devlog/ServiceNow.Business%20Rules.md)   
- [ServiceNow.Client Scripts](../devlog/ServiceNow.Client%20Scripts.md)   
- [ServiceNow.Script Includes](../devlog/ServiceNow.Script%20Includes.md)   
- [ServiceNow.UI Actions](../devlog/ServiceNow.UI%20Actions.md)   
- [ServiceNow.UI Policies](../devlog/ServiceNow.UI%20Policies.md)   
- [ServiceNow.Scheduled Jobs](../devlog/ServiceNow.Scheduled%20Jobs.md)   
- [ServiceNow.Workflows](../devlog/ServiceNow.Workflows.md)   
- [ServiceNow.Transform Maps](/not_created.md)   
- [ServiceNow.Web Services](/not_created.md)   
- [ServiceNow.UI Pages and Macros](/not_created.md)   
- [Service Portal Widgets](../devlog/ServiceNow.Service%20Portal.md)   
   
## When to do Scripting   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1667919631/wiki/jzsqzfrbtppkowmj9juw.png)