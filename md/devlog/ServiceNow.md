---
created: 1663221760484
desc: ''
id: zid89nkfnk5p1prroup8hfx
title: ServiceNow
updated: 1663500675981
---
   
Related::  [ITSM](../devlog/ITSM.md), [ITIL](../devlog/ITIL.md)   
   
   
---   
   
ServiceNow is a cloud-based software platform for IT Service Management ([ITSM](../devlog/ITSM.md)) which helps to automate IT Business Management. It is designed based on [ITIL](../devlog/ITIL.md) guidelines to provide service-orientation for tasks, activities, and processes. It uses machine learning to leverage data and workflows to help businesses become faster and scalable.   
   
It offers the flexibility, power, and dependability to achieve the goals of the incident and problem management. Moreover, users are free to select their most comfortable support interface. It provides all the information to the technician to diagnose and repair issues while removing the dependency on spreadsheets and emails.   
   
ServiceNow is a SaaS; licensed on a subscription basis. You don't have to install anything, you simply license it and get started. It can be accessed from any modern browser. All the applications and data is stored in the ServiceNow data centers. It started as [ITSM](../devlog/ITSM.md) suite which includes applications like Incident, Problem & Change. Incident is ServiceNow's most popular application. You can even create custom applications on the Now platform by leveraging powerful components like Business Rules and Workflows to create business applications.   
   
ServiceNow ticketing tool offers ranges of products which are designed according to the specific user’s needs.   
   
## Who uses Service Now?   
   
Following stakeholders use Service Now tool to achieve their business goals:   
   
   
- **Employees** – Use it to request their related IT business services.   
- **IT support Team**– Use it to manage service requests or incidents.   
- **Administrators** – ServiceNow helps administrators with user access, roles & privilege management   
- **Implementers** – Use it to deploy process applications and platform features which fulfills an organisation’s business needs.   
- **Developers** – Create new functionality with scripts to extend standard configurations.   
   
## Why use Service Now?   
   
Here are the prime reasons for using ServiceNow software:   
   
   
- All stakeholders including employee and customer make changes to the same platform which streamlines operations and provides a single version of the truth   
- Allows your employee to perform better, and the service levels will eventually improve   
- Helps to reduce ITSM costs up to 60%   
- Helps you to replace unstructured work patterns/business processes with intelligent workflows   
- It offers many ways to get help including forms, questionnaires, chat, email, etc.   
- Web services and email actions handle events from various monitoring tools and external sources.   
- ServiceNow technology will help you work very quickly which makes your work process smarter and faster.   
- Being SaaS, you do not need to worry about configuration, deployment, updates, and maintenance.   
- You can offer a customer friendly self-service portal with your branding.   
   
## Key Features of ServiceNow   
   
   
- Ease of customisation   
- Better Support to your customers with low maintenance cost   
- Real time analysis and reporting   
- Data confidentiality and integrity   
- Improved operational tracking   
- On-demand IT Service Management   
- Instance-based implementation   
- Low configuration requirement to quickly get up and running within an enterprise   
   
Via - [ServiceNow Tool Tutorial: What is, Use & Reporting Training](https://www.guru99.com/servicenow-tutorial.html)   
   
## ServiceNow Ecosystem   
   
   
- IT Service Management   
- IT Operations Management   
- IT Business Management   
- IT Asset Management   
- DevOps   
- Security Operations   
- HR Service Delivery   
- Customer Service Management   
- Governance, Risk and Compliance   
   
## ServiceNow ITSM core applications   
   
   
- Incident   
- Problem   
- Change   
- Service Catalog   
- Configuration   
   
## Environments   
   
When you license ServiceNow, you typically receive three environments. Development, Test and Production environments.   
   
You push changes from 1 instance to another. Once testing is complete, you push the changes to the Production environment. It is a best practice to "Clone Down" as frequently as possible and making sure Test environment is as close to Production as possible.   
   
## Releases   
   
ServiceNow introduces new changes to the platform in the form of feature releases, patch releases and hot-fixes. They typically follow 6-8 month release cycle.   
   
Feature releases contain new features, UIs and applications and are named after cities.   
   
Patch releases and hot-fixes are released ad-hoc. A patch release may contain many hot-fixes.   
   
   
---   
   
## Personal Developer Instance   
   
To get started create an account at [developer.servicenow.com](https://developer.servicenow.com/dev.do)   
   
and request a [Personal Developer Instance](https://developer.servicenow.com/dev.do#!/guides/sandiego/developer-program/pdi-guide/personal-developer-instance-guide-introduction)(PDI)   
   
Make sure to select **I need developer oriented IDE** after logging into the newly created account.   
   
   
---   
### Records   
   
A record is like a row in a spreadsheet. While a field is a column. A record is a collection of fields that make up a single entity.   
   
A database can have many tables such as an Incident Table, Problem Table, Change Table and so on.   
   
Each record has a unique key. It is called a `sys_id`. The `sys_id` is a 32 character, alphanumeric string that is used to identify an exact record. ServiceNow automatically generates this `sys_id` and provides us with tools to retrieve it.   
   
Records make up most things in ServiceNow like Users, Groups, Roles, Settings, Incidents, Problems and so on.   
   
### Lists & Forms   
   
Whether you're administering or developing within an instance, you'll spend majority of your time in a List or a Form view. Lists & Forms are two different ways to view Records.   
   
We "create" these views based on use case.   
   
| List View                                | Form View                             |   
| ---------------------------------------- | ------------------------------------- |   
| Multiple records per page                | Single record per page                |   
| Limited fields visibility                | Multiple fields visibility            |   
| Useful for filtering and sorting records | Useful for editing record information |   
| Multi-select                             | More control                          |   
| Edit cell directly                       | Button actions                        |   
   
**Lists**   
   
Displaying larger number of rows per page can effect performance. You can double click a cell to edit it(provided you've the Role that allows you to do so).   
   
Clicking on the "i" information icon will bring up a dialogue box from which you can open("drill into") the record in a Form view.   
   
**Forms**   
   
Forms can have more than one view, a view just defines what fields are displayed on the form.   
   
You can add additional fields to a table from the Form view.   
   
![](assets/images/2022-09-15-16-57-09.png)   
   
Priority field's accessibility depends on the values of Impact and Urgency field.   
   
### Filters & Search   
   
Within ServiceNow there are several Search bars, typically providing similar functionality although located in different places.   
   
![](assets/images/2022-09-15-17-17-16.png)   
   
### Search Conditions   
   
| Wildcard Syntax | Search Criteria  | Example  |   
| --------------- | ---------------- | -------- |   
| \*[term]        | contains         | \*Joe    |   
| !\*[term]       | does not contain | !\*Joe   |   
| =[term]         | equals           | =Doe     |   
| !=[term]        | does not equals  | !=Doe    |   
| [term]%         | starts with      | Hello%   |   
| %[term]         | ends with        | %goodbye |   
   
The Global Search bar will look for the searched term inside **Tasks**, **Live Feed**, **Policy**, **People & Places**, **Knowledge & Catalog**.   
   
### Condition Builder & Breadcrumbs   
   
It is a very powerful tool to define search criteria without needing to write SQL statements. You can access fields that are part of the record you're searching on. You can save conditions for later use or copy conditions.   
   
The format of the Condition Builder is: `<field> <operator> <value>`   
   
Example: If you're searching on the incident table you could reference related fields etc.   
   
![](assets/images/2022-09-15-17-32-49.png)   
   
The "funnel" or filter icon will load up the Condition Builder.   
   
The "Keywords" will list all the fields in a table. The fields with an arrow next to them are reference fields that basically reference a record in another table.   
   
The Operator will present a menu based on the field selected.   
   
You can chain **AND**,**OR** conditions.   
   
![](assets/images/2022-09-15-17-42-07.png)   
   
You can also have multiple sets of conditions; when run, will return either of the conditions depending on what matches.   
   
![](assets/images/2022-09-15-17-45-28.png)   
   
You can save a filter so you can load it in a future use.   
   
Right click on different columns to find various shortcuts.   
   
[Condition builder docs](https://docs.servicenow.com/bundle/quebec-platform-user-interface/page/use/common-ui-elements/concept/c_ConditionBuilder.html)   
   
**Breadcrumbs**   
   
Breadcrumbs go hand-in-hand with the Condition Builder, they'll show up on top of a List. They're dynamic. They change based on conditions inside the Condition Builder. You can remove a filter by clicking the "`>`" in the breadcrumb. Right click on the breadcrumb to copy the URL or the query and open it in a new window.   
   
Breadcrumb will update after a query is run.   
   
### Context Menus   
   
They appear in both List and Form views. It can be accessed by clicking the "hamburger" icon. An administrator can add/remove options from a context menu.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663257896/wiki/qcsoyi1yq0588nh4rsd6.png)   
   
A context menu on a List view of an Incident form.   
   
There are many different context menus that show up depending on the “context”.   
   
[Form context menu docs](https://docs.servicenow.com/bundle/sandiego-platform-user-interface/page/use/using-forms/concept/c_FormContextMenu.html)   
   
### Modifying Lists & Forms   
   
We can either **Personalise** or **Configure** Lists and Forms.   
   
When we **personalise** a List or Form that modification is specific to your User account. You can add/remove any field, reorder fields; to get started click on "Personalize List Columns" from List context menu. You can even personalise forms. Click on the adjust icon on the form to start.   
   
On the other hand, when we **configure** a List or Form, it’ll be applied globally(system wide). It can only be done by a System Administrator.     
To configure you'd select "List layout" from List context menu. To configure a form, you'd select main context menu > Configure > Form layout; you can add or remove fields on form, change order etc.   
   
**List Calculations** can be used to get averages of columns.     
**List Control** can be used to provide additional controls for the List view.   
   
**Form Design** will provide an interface(drag n drop) to build forms.     
Form context menu > Configure > Related Lists - to configure related lists.   
   
## Customisation   
   
on Client-side:   
   
   
- Client scripts   
- UI Policies   
- UI Actions   
   
on Server-side:   
   
   
- Business Rules   
- Script Includes   
- UI Actions   
- Data Policies   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663332040/wiki/bkv264gpxqjproqcc7sr.png)   
   
### Client-Side vs Server-Side   
   
Just like any other web application, ServiceNow follows a Client-Server model. The instance data is stored in ServiceNow data center.     
Any time you want to access data in ServiceNow, the client(browser) makes a request to the ServiceNow data center over the internet.   
   
The server-side ServiceNow application receives the request and communicates it to the database server where the data is stored. It then packages a response for your request and sends it back.   
   
The browser then processes this response and displays it on the screen.   
   
The time it takes for your request to reach ServiceNow's servers and back is called the round trip time. No matter how fast your internet is, there will always be some lag.   
   
## Customizations   
   
ServiceNow is very flexible, you can change (appearance) almost everything.   
   
Things you can customize:   
   
   
- Client scripts   
- Business Rules   
- Script Includes   
- UI Actions   
- UI Policies   
- Data Policies etc   
   
In addition, you can create custom applications, tables, pages for business needs that can interact with existing instance data.   
   
   
- [ServiceNow.UI Policies](../devlog/ServiceNow.UI%20Policies.md)   
- [ServiceNow.UI Actions](../devlog/ServiceNow.UI%20Actions.md)   
- [ServiceNow.Business Rules](../devlog/ServiceNow.Business%20Rules.md)   
- [ServiceNow.Client Scripts](../devlog/ServiceNow.Client%20Scripts.md)   
- [ServiceNow.Data Policies](../devlog/ServiceNow.Data%20Policies.md)   
- [ServiceNow.Script Includes](../devlog/ServiceNow.Script%20Includes.md)   
- [ServiceNow.Update Sets](../devlog/ServiceNow.Update%20Sets.md)   
- [ServiceNow.Plugins](../devlog/ServiceNow.Plugins.md)   
   
## Tables & Fields   
   
   
- [ServiceNow.Tables & Fields](../devlog/ServiceNow.Tables%20%26%20Fields.md)   
- [ServiceNow.Table Structure & Schema Maps](../devlog/ServiceNow.Table%20Structure%20%26%20Schema%20Maps.md)   
- [ServiceNow.Table Maintenance & Custom Apps](../devlog/ServiceNow.Table%20Maintenance%20%26%20Custom%20Apps.md)   
   
## User Administration   
   
   
- [ServiceNow.Users & Groups](../devlog/ServiceNow.Users%20%26%20Groups.md)   
- [ServiceNow.Roles and ACLs](../devlog/ServiceNow.Roles%20and%20ACLs.md)   
- [ServiceNow.LDAP  SSO  & Impersonation](../devlog/ServiceNow.LDAP%20%20SSO%20%20%26%20Impersonation.md)   
   
   
---   
   
## Core Applications   
   
   
- [ServiceNow.Incident](../devlog/ServiceNow.Incident.md)   
	- [ServiceNow.SLAs](../devlog/ServiceNow.SLAs.md)   
- [ServiceNow.Problem](../devlog/ServiceNow.Problem.md)   
- [ServiceNow.Change](../devlog/ServiceNow.Change.md)   
- [ServiceNow.Configuration](../devlog/ServiceNow.Configuration.md)   
	- [Configuration Item](../devlog/Configuration%20Item.md)   
- [ServiceNow.Service Catalog](../devlog/ServiceNow.Service%20Catalog.md)   
- [ServiceNow.Knowledge](../devlog/ServiceNow.Knowledge.md)   
- [ServiceNow.Service Portal](../devlog/ServiceNow.Service%20Portal.md)   
- [ServiceNow.Connect](../devlog/ServiceNow.Connect.md)   
- [ServiceNow.Visual Task Boards](../devlog/ServiceNow.Visual%20Task%20Boards.md)   
   
## System Administration   
   
   
- [ServiceNow.System Properties](../devlog/ServiceNow.System%20Properties.md)   
- [ServiceNow.Self-Service](../devlog/ServiceNow.Self-Service.md)   
- [ServiceNow.Mobile](../devlog/ServiceNow.Mobile.md)   
- [ServiceNow.System Diagnostics](../devlog/ServiceNow.System%20Diagnostics.md)   
- [ServiceNow.System Security](../devlog/ServiceNow.System%20Security.md)   
- [ServiceNow.Notifications](../devlog/ServiceNow.Notifications.md)   
- [ServiceNow.Workflows](../devlog/ServiceNow.Workflows.md)   
- [ServiceNow.Import Sets](../devlog/ServiceNow.Import%20Sets.md)   
- [ServiceNow.Reports](../devlog/ServiceNow.Reports.md)   
-  [ServiceNow.API](../devlog/ServiceNow.API.md)   
   
## Integrations   
   
   
- [ServiceNow.ServiceNow Okta Integration](../devlog/ServiceNow.ServiceNow%20Okta%20Integration.md)   
   
## Misc Notes   
   
### Dot walking   
   
Dot-walking provides access to fields on related tables from a form, list, or script. If the current table contains a reference to another table, any field on the referenced table can be accessed using dot-walking. Dot-walking references a field by building a chain of field names separated by dots (periods)   
   
### Affected CI   
   
CI stands for **Configuration Item**. CIs can be used to tie tickets to the services they pertain to. Incidents and RITMs/Tasks have fields that allow you to choose the affected CI.   
   
Affected: **The service or CI that the change/incident/project/problem is happening within**. Easy example: We pull a network router out of the wall. The Affected CI is the router, the Client Service is Network Services. Impacted: Services, CI's that the change will impact.   
   
### Coalesce   
   
Coalesce is **a field property that is used in transform map field mapping**. When you use coalesce on a field, you can use that field as a unique key. If a match is found coalesce field is found, the existing record will be updated with the imported information.   
   
### Upgrades   
   
   
- `stats.do` in application navigator for current version and other details   
- Request upgrades through ServiceNow HI   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665679005/wiki/g4svejkolbgb3bqb5hgd.png)   
   
   
### ServiceNow HI   
   
   
- HI(Service Now) abbreviate Hosted Instance.   
- Customer administration     
- ServiceNow for ServiceNow     
- [ServiceNow HI](https://hi.service-now.com)    
- Manage instances   
	- Request upgrades   
	- Request clones   
	- Create incidents     
- Access ServiceNow Knowledge Base   
   
### Security   
   
   
- Security properties   
	- Via the [ServiceNow.System Properties](../devlog/ServiceNow.System%20Properties.md)   
	- Max file attachment size, removing remember checkbox, enabling secure session cookies, configuring file types for attachments.   
- IP address access controls   
   
### Events   
   
   
- Triggered by   
	- User actions   
	- Scripts   
	- Time/Schedules     
	- Rejection/Approval   
	- Business rules   
	- Workflows   
- Event queue     
	- Events are processed, first in first out basis   
- Event registry     
	- A registered event is a record in the `sys_event` table   
	- Events may contain parameters   
   
See **System Logs** → **Events**   
   
[ServiceNow.Notifications](../devlog/ServiceNow.Notifications.md)   
   
   
---   
   
   
- [ServiceNow.Integrations](../devlog/ServiceNow.Integrations.md)   
   
## Scripting   
   
   
- [ServiceNow.Scripting](../devlog/ServiceNow.Scripting.md)   
   
   
---   
   
   
- [dylanlindgren.com](https://www.dylanlindgren.com/) \[blog\]   
- [blog.jacebenson.com](https://blog.jacebenson.com/) \[blog\] - a great aggregate resource for all things ServiceNow   
- [Knowledge '19 On Demand Library](https://community.servicenow.com/community?id=community_odl) \[resource\]   
- [ServiceNow Fundamentals](https://www.youtube.com/playlist?list=PLCOmiTb5WX3pf-cNef70bnbWq8Yo-JFv1) \[video collection\] - a great YouTube playlist of ServiceNow fundamentals videos   
- [ServiceNow Standards Framework](https://github.com/iamkalai/SNStandardsFramework) \[resource\] - ServiceNow framework to get you started on a number of different topics   
- [Interface Design Patterns for Script Includes](https://codecreative.io/servicenow/interface-design-patterns-for-script-includes) \[blog post\] - best practices around script include development   
- [Script Execution Order](https://docs.servicenow.com/bundle/jakarta-servicenow-platform/page/script/general-scripting/reference/r_ExecutionOrderScriptsAndEngines.html) \[article\] - excellent resource that exposes the ServiceNow execution order of scripts and various engines   
- [Script evaluation of fields by data type](https://docs.servicenow.com/bundle/jakarta-servicenow-platform/page/script/general-scripting/reference/r_ScriptingOfFieldTypes.html) \[article\] - another excellent resource which explores the evaluation of fields by data type in ServiceNow scripts   
- [Understanding GlideAjax](https://snprotips.com/blog/2016/2/6/gliderecord-client-side-vs-server-side) \[blog post\] - a deep dive into GlideAjax   
- [GlideAjax Examples](https://docs.servicenow.com/bundle/geneva-servicenow-platform/page/script/server_scripting/reference/r_ExamplesOfAsynchronousGlideAjax.html) \[tutorial/guide\] - more GlideAjax examples, because… who starts from scratch? 🙂   
- [GlideAjax Troubleshooting](https://codecreative.io/blog/glideajax-troubleshooting-guide/) \[blog post\] - having trouble with your script include? Checkout this blog post   
- [Using GlideRecordSecure](https://docs.servicenow.com/bundle/jakarta-application-development/page/script/glide-server-apis/concept/c_UsingGlideRecordSecure.html) \[article\] - product docs page on GlideRecordSecure   
- [Script Include Best Practices](https://www.caskllc.com/resources/the-mighty-script-include/) \[blog post\] - learn how to create script includes the proper way   
- [Bypass SSO](https://community.servicenow.com/community?id=community_question&sys_id=ca950beddbd8dbc01dcaf3231f96197c) \[community\] - general SSO information   
- [Glider](https://github.com/tltoulson/Glider.js) \[library\] - an interesting library with tons of awesome features   
- [Useful ServiceNow Snippets](https://github.com/markmilly/servicenow-snippets) \[snippets/code\] - a list of common ServiceNow snippets to help reduce frustrations   
- [Demystifying the ServiceNow Cloud](https://www.youtube.com/watch?t=2s&v=JTYWyw0v8R4) \[video\] - an interesting look into how ServiceNow manages their architecture
   
   
## Links   
   
   
- [Intelligent Test Automation Tool [2022] - testRigor Software Testing](https://testrigor.com/) - [testRigor](../devlog/testRigor.md)