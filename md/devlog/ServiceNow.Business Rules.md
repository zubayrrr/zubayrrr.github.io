---
created: 1663325294889
desc: ''
id: v7tmv2j849a7b1g1kshsjy0
title: Business Rules
updated: 1663325449403
---
   
> [!INFO]   
> A business rule is a server-side script that runs when a record is displayed, inserted, updated or deleted, or when a table is queried. — ServiceNow Docs   
   
Like [ServiceNow.UI Policies ](/not_created.md) and [ServiceNow.UI Actions](../devlog/ServiceNow.UI%20Actions.md), Business Rules run off of a specific table and are triggered by database operations.   
   
It contains Javascript that is executed on the server-side.   
   
   
- There are ~2,400 OOB business rules   
- You’ve access to:   
	- Current object (`current`)   
	- Previous object (`current`)   
	- Scratchpad (`g_scratchpad`)   
   
   
- Runs on a specific table   
- 2 execution conditions   
	- Database operations   
	- Custom conditions(Filter conditions)   
   
When creating a business rule there are two important conditions to keep in mind:   
   
   
- Configure _when_ to run   
	- Before   
	- After   
	- Display   
	- Async   
- During _what_ operation   
	- Insert   
	- Update   
	- Delete   
	- Query   
   
**Example**   
   
1. User sends request to server for specific incident (query)   
2. Application server requests record from database server   
3. Database server responds to application server with record   
4. Application server checks for display business rules, then sends response back to client   
5. User modifies incident record via form and sends update request   
6. Application server receives update, checks for before business rules, then sends to database server   
7. Database server updates record   
8. Application server checks for after business rules   
   
**Use cases**   
   
1. Create an associated CI(record) when a new asset(record) is created on the asset table.   
2. When an incident is reopened, increment the reopen count.   
   
You can find Business Rules by searching it on the application navigator search under “System Definition”   
   
OR   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663324221/wiki/kksdrrqlrtrzzuyg3xa0.png)   
   
From All Incident List view’s context menu > Configure > Business Rules.   
   
It’ll show you all the business rules associated with the Incident table.   
   
Click on “Change state on closed Insert” to get inside the Business rule in Form view.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663324377/wiki/pvlzkrf6lwzxjsdjyj6i.png)   
   
Since “Insert” is selected under the “When to run” tab; it’ll only run when new records are inserted into the Incident table.   
   
Checking “Advanced” checkbox will also enable “When” is it ran(before, after etc), order it is ran and “Delete”, “Query” checkboxes also appear.   
   
Under the “Actions” tab, we can set field values on the Incident.   
   
Check the “Advanved” checkbox to find the Advanced tab; where you can specify a condition and write a script. Most of the time you’ll be writing Business Rules as scripts because actions(When to run) can be limited.   
   
**Create business rule**   
   
When the state of an incident is set to “New”; when we make modifications to the form and save that incident, we want that state to automatically change the state to “In Progress”.   
   
Click on “New” button on Business rules List view for the Incident table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663325004/wiki/fki0278i81lhgbcggnvi.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663325025/wiki/v5f3minucw1qbsuptk1m.png)