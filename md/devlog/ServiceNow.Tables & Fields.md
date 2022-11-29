---
created: 1663383465869
desc: ''
id: pnqqc0tgi0qmcg0mr2cjlzp
title: Tables & Fields
updated: 1663383700641
---
   
**Overview**   
   
   
- There are over 2,000 tables out-of-the-box in a ServiceNow instance.   
- The majority of these tables directly relate to the applications inside ServiceNow.   
- Each application may have one or more tables.   
- Tables may extend other tables.   
- There are 100s of CMDB tables for the Configuration Management application.   
- The naming convention in ServiceNow for tables is `lower_case`. However, tables have labels which may contain capitalisation and spaces.   
- With admin role, we can create and modify tables.   
   
**The Database, Tables & Fields**   
   
   
- Each DB may contain many tables.   
- Each table contains many fields.   
- Records are stored in tables.   
- Each row in a table can be called as a Record and each column in a row as a Field.   
   
**Major Tables**   
   
   
- Task [task]   
	- It is a parent table for a number of tables such as: Incident, Problem, Change Request tables.   
	- It stores common values such as number field, short description field, assigned to.   
	- These fields are “inherited” but tables that extend it.   
- Incident [incident]   
- Problem [problem]   
- Change [change_request]   
- User [sys_user]   
	- All the users are stored on this table, if you needed to create a new user, you’d be creating a record on this table.   
- Group [sys_user_group]   
- Role [sys_user_role]   
- Location [cmn_location]   
- Company [core_company]   
- Knowledge [kb_knowledge]   
- Knowledge Category [kb_category]   
- Knowledge Base [kb_knowledge_base]   
- Service Catalog [sc_catalog]   
- Catalog Items [sc_cat_item]   
- Configuration Item [cmdb_ci]   
- Server CI [cmdb_ci_server]   
   
**Data Dictionary Tables**   
   
When we make modifications to a table or field, the changes are stored in Data Dictionary Tables.   
   
   
- It contains metadata about tables.   
- sys_db_object record represents a table.   
- sys_dictionary record represents a field on the table.   
- sys_documentation record represents a field label, etc.   
   
To go to a specific table, type the name inside the application navigator search bar as `<table_name>.list` for list view of the table.   
   
`sys_db_object.list` > Label for Incident   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663385139/wiki/ov6zvhl3gz7mnqli5rnm.png)   
   
Incident table   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663385231/wiki/smh4aprbvykpketakoqg.png)   
   
## Fields   
   
and field types in ServiceNow   
   
   
- Each table contains many fields.   
- Where each field maybe one of many different field types.   
	- Free form text field  AKA string field   
	- Choice fields   
	- Integer field    
- Each field may have number of properties like Calculated fields   
	- Calculated fields provide the ability to calculate the value of a field based on certain logic.   
- Field attributes add filters, restrictions and special UI attributes to field.   
- Default values — default values when inserting a record.   
- Dictionary overrides   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663385661/wiki/hgkzzhykhfjacigcn2n3.png)   
   
**Field Types**   
   
   
- String   
- Date   
- Time   
- Choice   
- True/False   
- List   
- HTML   
- Script   
- Reference   
   
There are certain metadata fields that are automatically created whenever a new table is created like:   
   
   
- Created    
- Updated   
- Created by   
- Updated by (reference field to the User table)   
- sys_id — unique identifier    
- Updates field — stores an integer value on how many times the record has been updated.   
   
   
**GUID (Globally Unique Identifier**   
   
   
- Referred to as `sys_id`.   
- A unique 32 character hexadecimal string.   
- Every record has a sys_id   
- sys_id’s are automatically generated for all records.   
   
**Reference Fields**   
   
Reference fields reference other tables within the DB, providing a relationship among the records. They play an important part in the structure of the DB. ServiceNow uses [mysql](../devlog/mysql.md) as it’s RDBMS.   
   
Almost every table in ServiceNow has reference fields. They store related record’s `sys_id` and not the value itself.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387178/wiki/zkohk1pu6nf1us0cs9nv.png)   
   
   
Dictionary Entry Record   
   
Right click on Category    
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387277/wiki/qtplffy7st5ay9ex9mzn.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387237/wiki/r7rmj2favj1ubkmekuk5.png)   
   
You can also reach it from Incident Table   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387358/wiki/rqawxl0o7zoymtplbdqe.png)   
   
Or by going into `sys_dictionary` table filtering by “incident” and “category” for column name.   
   
Field with reference type — being referenced from another table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387612/wiki/rh5udxctictxqdsocaa8.png)   
   
This field has Dictionary overrides as it is associated with the Tasks table, it is inherited by all the tables that extend the Tasks table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387787/wiki/j3dnz2bhr0twprelqeul.png)   
   
Assignment group field — once populated with a certain group, the Assigned to field will only accept Users from that Assignment group.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663387978/wiki/uxtux1h2qe3w0mfhqcgp.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663388024/wiki/pbnyfiw8t9snvjqykfdc.png)   
   
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/9d643a2152fa4567acaaab3b76cc818e" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>   
   
## Field Attributes   
   
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/852b9062e23f4611b3e9cf2dfffe38ce" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>   
   
## Number Maintenance   
   
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/2ffba30e6238473da3f19cd2572fbd61" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>