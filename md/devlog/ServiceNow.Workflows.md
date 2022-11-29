---
created: 1665629757097
desc: ''
id: ojvicw7yj131wd3zd2lsa4q
title: Workflows
updated: 1665629757097
---
   
> [!info]   
> The Workflow editor is an interface for creating and modifying workflows by arranging and connecting activities to drive processes. — ServiceNow Docs   
    
A workflow automates and visualizes a multi-step process as a sequence of activities.   
   
   
- Workflows are **server-side** Javascript.   
- There are different scopes in a workflow.   
- Workflow contexts are created when workflow conditions evaluate to true.   
- Versioning and checkouts(fork).   
   
**Scripting in Workflows**   
   
   
- Use scripts only when OOB features aren’t enough.   
- Activities that support scripting   
	- Approval activities   
	- *Run Script* activity   
	- If, Switch and Wait for conditions activities   
	- Create task activity   
	- Notification activity   
	- Scriptable Order Guide activity   
	- [REST Messages](../devlog/ServiceNow.Send%20REST%20calls.md), SOAP Message activities    
- Scope   
	- `current` record   
	- `workflow.scratchpad` object   
	- Activity specific variables   
	- Local variables   
   
   
**Use Cases:**   
   
   
- Dynamically assign approvals to specific group of users.   
- Trigger a web service call via a workflow activity.   
   
[Create a workflow | ServiceNow](https://docs.servicenow.com/bundle/tokyo-servicenow-platform/page/administer/workflow-administration/task/t_CreateAWorkflow.html)   
   
   
- Number of activities   
	- Approvals, Conditions, Notifications, Timers, Tasks, Utilities, more...   
- Workflows can take different paths(conditions) and call other workflows    
- Workflows are usually created against a table.   
- Workflow created/executed when an even is triggered is called a Workflow context.   
- Workflows in the “Published” state cannot be modified.   
- A workflow must be checked out my a user before  any changes can be made.   
- When you “checkout” a workflow, you’re essentially creating a fork/copy of it. Just like you do in [version control.git](../devlog/version%20control.git.md).   
- Once changes are made to the forked version, it may be published and then the system will use the newer version as opposed to the previous one.   
- They’re commonly used for [ServiceNow.Service Catalog](../devlog/ServiceNow.Service%20Catalog.md),  [ServiceNow.Change](../devlog/ServiceNow.Change.md) and [ServiceNow.Knowledge](../devlog/ServiceNow.Knowledge.md) but can be used for any record in the system.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665683484/wiki/s0blqtkk5qstd7j7x2bu.png)   
   
   
## Workflow Editor   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665683510/wiki/avpvhtm33vwvg68kgtvj.png)   
   
Service Catalog Item Request    
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665683593/wiki/oz2lrhmgbvso8igoulcv.png)   
   
   
Double click an activity to open it’s properties.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665684168/wiki/ht5ti3rvdoxbokraknxr.png)   
   
   
It cannot be edited as it is, you need to “checkout”  from the menu.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665683899/wiki/piurztucjp9mvs4x1vbv.png)   
   
   
Checkout the context menu for more options such as:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665684363/wiki/ql8pf1kwlbuodamf1qky.png)   
   
## Create New   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665685161/wiki/be7emryobwnibzivn3dx.png)   
   
Add an If condition by dragging and dropping it on the “line” as it turns blue.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665685425/wiki/stpnwpfbwtfqkotvz3za.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665685540/wiki/otkerwqcuq1orjgzmyoy.png)   
   
Add a notification for “Yes” and another for “No”   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665686426/wiki/bws5vsmpv3d01tdeizbf.png)   
   
Publish it   
   
Create 2 Dummy Incidents to test out the workflow   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665686633/wiki/gnjbo9lm00ltkzsrapzb.png)   
   
Go to Emails under **System Logs**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665686686/wiki/plelczeffsvkbwcgd1ho.png)   
   
On the All Workflows page under **Live Workflows**   
   
voilà!   
   
## Scheduled Workflows   
   
To schedule workflows. See: [ServiceNow.Scheduled Jobs](../devlog/ServiceNow.Scheduled%20Jobs.md)