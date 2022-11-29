---
created: 1663396501119
desc: ''
id: f72y4raggiy1bha4nx4x6r4
title: Table Maintenance & Custom Apps
updated: 1663400795143
---
   
## Create a table   
   
When creating a table, it is important to have  a relevant **Label** and **Table Name** with the right naming convention.   
   
All custom tables in the global namespace will be prefixed with a `u_` example: movie table will be `u_my_movies`   
   
Table names shouldn’t contain any spaces and should be lowercase.   
   
When creating a new table there are options to create a new module within an existing application or a new application.   
   
We can also create a Role for a table which will generate some ACLs for us.   
   
We can also provide fields at the same time.   
   
**Create a table in a  scope**   
   
It is a little different when creating a table in a scope.   
   
## Delete Table   
   
It is important to delete all the records in a table before deleting the table. It will prevent any cascade trouble or onDelete business rules.   
   
**We cannot delete tables that come out-of-the-box.** Only user created tables may be deleted.   
   
Deleting a table will also delete the related records of the table such as reports, forms, form sections, reference fields, ACLs.   
   
## Creating an Application   
   
An application in ServiceNow is basically a menu of one or more tables shown within application navigator.   
   
An application encompasses  all of the related records that are linked to the application’s tables such as any customizations, ACLs, Views.   
   
We can use a wizard the ServiceNow provides for creating an application.   
   
3 templates    
   
   
- Start from scratch   
- Create custom application   
- Start from template   
   
**Application scope**   
   
In order to make sharing and selling custom applications easier, ServiceNow introduced customer specific scope called Vendor Prefix.    
   
If I share a meeting manager application to another instance which also has another custom application with same name there will not be a conflict because of Vendor Prefix.   
   
Tables under System Definition   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663397649/wiki/tidceyclmlray6khtaah.png)   
   
We created a new table called “My movies”   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663397847/wiki/rxwddtsjkilj1k5xzzge.png)   
   
With two fields.   
   
Under Controls you’ll find a new user would’ve been created `u_my_movies_user`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663398114/wiki/hd6fojvduh03linxjjjq.png)   
   
We created some records.   
   
To delete the table, you must first delete all the records and then delete the table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663398243/wiki/p3xnx8fnmuhphpdu7ohy.png)   
   
## Creating applications   
   
On Application Manager   
   
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/3f6c509b8e114b959f2696da5b703431" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>   
   
The name of the table is `x_893618_my_movies_movies`, app scope + table name   
   
**Studio only works for scoped applications.**