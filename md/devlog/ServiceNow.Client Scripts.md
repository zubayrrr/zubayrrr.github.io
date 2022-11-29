---
created: 1663325510261
desc: ''
id: oj9sysqs66ewevcqokiywwz
title: Client Scripts
updated: 1663326047492
---
   
> [!info]   
> Client scripts run on the client(web browser). You can use client scripts to define custom behaviours that run when events occur such as when a form is loaded or submitted, or a cell changes value. — ServiceNow Docs   
   
Client scripts allows us to write [languages.Javascript](../devlog/languages.javascript.md) and specify when they get executed.   
   
They're often used in Form view but may also be used in List view.   
   
They can be executed using the following triggers:   
   
   
- On page/form load   
- On field change   
- On form submission   
- On cell edit   
   
ServiceNow provides many helper methods and client scripts via [The GlideForm (g_form) Class](https://developer.servicenow.com/dev.do#!/learn/learning-plans/quebec/new_to_servicenow/app_store_learnv2_scripting_quebec_the_glideform_g_form_class) API.   
   
**How does it work?**   
   
You write your client scripts within SNOW and then when a form loads that has the client script it’ll get **shipped to the browser** and is triggered based on conditions(field changes),  it’ll sit in your browser’s memory until that **event**  occurs. Additional request-response to the server doesn’t happen because of this. The logic runs in realtime unless there are additional calls to the server.   
   
**Form view: Client Scripts**   
   
Fields required when creating a client script:   
   
   
- Table   
- UI Type   
	- Desktop, Mobile or Both   
- Type   
	- OnChange, onLoad, onSubmission   
- Field Name   
	- This field can be based on the **Type**   
- Script   
	- We’ve access to **JQuery** but its not recommended to manipulate DOM direclty with JQuery. Best practice is to use SNOW APIs when available.   
   
**Use cases**   
   
1. Highlight **Caller** field if user is a VIP.   
2. Run **Conflict checker** for Change Management.   
   
We'll explore Client scripts using the Change application.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326128/wiki/ruruk0fyu33zhjyu4p9u.png)   
   
Example “Notify Conflict”   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326175/wiki/lnirvilr2ol6wa23nggq.png)   
   
   
Example for “onChange” type   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326309/wiki/vahouaqdjzwdywghcqny.png)   
   
Example “GlideAjax” — Script includes   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326367/wiki/h5jfj2vhekgr7fqpddd1.png)   
   
**Create client script**   
   
When a field “State” changes from “New” to “Authorize” display a message.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326457/wiki/g5wzjejl81f9qtxiqkpk.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663326501/wiki/t1yn06mfwgn2dlnzx9rx.png)