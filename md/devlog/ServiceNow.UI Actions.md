---
created: 1663325327857
desc: ''
id: u81s5t8tgue56heed9gpn0z
title: UI Actions
updated: 1663325331927
---
   
> [!info]   
> UI Actions add buttons, links and context menu items on forms and lists, making the UI more interactive, customizable and specific to user activities. UI Actions can contain scripts that define custom functionality.   
   
They run on **server-side** but can optionally run [languages.javascript](../devlog/languages.javascript.md) on client-side.   
   
They’re typically configured for form views(of a record).   
   
An example of UI Action would be a “Copy Change” button within a Change request.   
   
**Form View: UI Actions**   
   
   
- Table   
- Show on insert/update   
- Client   
	- Run Javascript on client-side   
- Type of UI Action   
	- Form button   
	- Form context menu   
	- Form link etc   
- Condition   
- Script   
   
**Server-side UI Actions**   
   
   
- Access to:   
	- `current` object   
	- `GlideRecord` API   
	- `GlideSystem` API   
- Default behaviour   
- Runs server-side if **Client** checkbox is NOT checked.   
- Better performance.   
   
**Client-side UI Actions**   
   
   
- Check the Client checkbox   
- Provide the name of the Onclick method   
- Use `action.setRedirectURL()` to redirect user to another page.   
- To call another UI action on the current form, use one of the following:   
	- `gsftSubmit(gel(<ui_action_name>)`   
	- `gsftSubmit(null, g_form.getForElement(), <ui_action_name>)`   
   
   
**Run Both Client-side and Server-side**   
   
   
- When the user invokes an event via UI Action, the client-side code will run and then the server-side code.   
- Verifies the client-side code is complete:   
	- `if(typeof window == 'undefined')` - call a function after this statement or put it directly inside the if statement.   
   
**Examples**   
   
1. Trigger Salesforce integration, creating an associated Salesforce ticket.   
2. Reject and approval record.   
   
Maybe we have UI Action on an Incident record when clicked will send data on the incident’s record and will create a Salesforce ticket via REST API.   
   
You can get access to UI Actions from the context menu of a List view (configure) or from inside a Form view of an incident.   
   
Sometimes UI Actions are also present as links under “Related Links”.   
   
Additional UI Actions can be found by right clicking the header or by clicking the context menu in an Incident Form view.   
   
Configuring a UI Action:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663319954/wiki/r9deyyhzmnxh5allw3fd.png)   
   
Requires Role section is where you define Roles that are required to have accessibility to this UI Action.   
   
**Create a UI Action**   
   
Click on “New” button from the UI Actions List view.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663323648/wiki/t3ui3jdg1rjsaqiyndej.png)   
   
For “Onclick” declare a function name.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663323687/wiki/knygiv3hjbuycbh5nu8z.png)   
   
The “Hello” UI Action(Button) will now be available on the Incident Form view.