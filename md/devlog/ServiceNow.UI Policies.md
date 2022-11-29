---
created: 1663325367606
desc: ''
id: eq8hmdx8h79hq3gzhqvsnus
title: UI Policies
updated: 1663325369856
---
   
> [!info]   
> UI Policies offer an alternative to client scripts for dynamically changing information a form. Use UI Policies to define custom process flows for tasks. — ServiceNow docs   
   
   
- UI Policies run on the **client-side**, they are shipped where the UI events are triggered and policies are executed.   
- They offer a substitute to scripting. Even though you can apply scripting logic to a UI Policy its rarely required.   
- UI Policies are for form controls, such as setting fields as mandatory, read-only or hiding them based on certain conditions.   
   
Example: say you've a requirement to change the incident form if a user marks the "State" as "resolved"; the incident "Close code" is required and the user cannot close the incident until it is set. An alert popup box should show up informing the user to add a Close code. This is an example of setting a field as mandatory based on certain conditions.   
   
**Examples**   
   
1. Set an incident's **Short description** field to read-only if the incident state is **Closed**.   
2. Hide an incident's **Resolution notes** field if the state is **Open**.   
   
   
---   
   
Navigate into a specific incident; from Form context menu > Configure > UI Policies. It'll bring up the policies for the Incident table and the table it extends(Tasks table).   
   
Select any policy by clicking on it to view the UI Policy in form view.   
   
The conditions for a policy are set under "When to Apply" section.   
   
Under the "UI Policy Actions", select a UI Policy Action by it's field name to configure that field.   
   
Click on "Advanced View" from related links to find the Script tab where you can apply logic via scripts.   
   
**Add a policy**   
   
Click the "New" button on the UI Policies page to get started.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663317499/wiki/oqadbmmdzqsocq0ftzww.png)   
   
When the field Category is selected as “Database” run this policy.   
   
Save the record and scroll down to UI Policy Actions and create one.   
   
Select the field you want to interact with   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663317610/wiki/yb0povcvzvba78b3nbyp.png)   
   
Click Submit to save.   
   
Create another one   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663317659/wiki/nch1spjsdqg41s6a51ed.png)   
   
Here, we’re setting the Business Service field to Mandatory.   
   
Go to an Incident to test out the changes   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663317758/wiki/p556ydul1rcaor0m7jb0.png)