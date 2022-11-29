---
created: 1663330786123
desc: ''
id: oog4sxena64vke2cxj6rlmt
title: Script Includes
updated: 1663331867438
---
   
> [!info]   
> Script includes are used to store Javascript that runs on the server. Create Script Includes to store Javascript functions and classes for use by server scripts. Each script include defines either an object class or a function. Script includes run only when called by a server script. — ServiceNow Docs   
   
You can think of it as a location in service now where you can store Javascript functions and classes(reuseable code) that can be invoked from pretty much everywhere within ServiceNow making your code [DRY](../devlog/DRY.md).   
   
They're not applied directly to a table or ran based on a trig.   
   
**Script includes are involved only when called.** They can be called from anywhere. They're stored on the server-side and are never shipped to the client-side. However, you may call script includes client-side using GlideAjax API.   
   
**Script Includes Characteristics**   
   
2 Types:   
   
   
- Classless   
	- Script include name = function name   
	- Server-side only   
- Class   
	- Typically extend another class   
	- Can be invoked via server-side or client-side   
- Important Attributes   
	- Script include name   
	- `type` property   
	- `prototype`   
   
**Extending Script Includes**   
   
   
- Any class may be extended, any script include can extend any other script include   
- `AbstractAjaxProcessor` is a commonly extended class used for GlideAjax    
   
```js
<className>.prototype = Object.extendsObject(<extendingClassName>, { /* your script* })
```
   
   
When Client callable checkbox is checked the system will automatically generate some of the code for `AbstractAjaxProcessor`   
   
**Use cases**   
   
1. Create commonly used helper functions.   
2. Call a custom function via GlideAjax.   
   
If you want place a trigger on the client-side(like when a user makes a selection, clicks a button) and you want to perform some logic or checking the value - you can store all of this in a Client script and the client script will call the server-side script asynchronously.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663331260/wiki/trzxkeoktn1cye1sm3ox.png)   
   
Select Script Includes under “System Definition” to list all the script includes.