---
category: '2022'
created: 2022-11-08 15:06:44.024000+00:00
id: 8a6b0b52-b59f-4e23-a733-09845a2346df
tags:
- devlog
title: GlideRecord
updated: 2022-11-08 15:06:48.348000+00:00
---
   
ServiceNow uses [mysql](../devlog/mysql.md) as its RDBMS.   
   
To interact with your data stored in an MySQL DB, instead of writing SQL queries, you can use GlideRecord API.   
   
It is accessible to the developer on the server side. It is used to perform CRUD operations. It generates SQL for the developer.    
   
You can think of GlideRecord has having 2 stages:   
   
   
- Building a query   
	- Select the DB and perform filtering   
	- Actual SQL is sent tot he DB and records are received back in response   
- Process records   
	- Perform actions on an ordered list of records   
   
You can use GlideRecord in a [ServiceNow.Client Scripts](../devlog/ServiceNow.Client%20Scripts.md) but it is deprecated and not recommended.   
   
## Example   
   
```javascript
// print a list of all priority 1 incidents to the screen


// instantiating object with new keyword along with the constructor GlideRecord with table name
var incidentGR = new GlideRecord('incident'); 

// calling addQuery method - similar to filter in GUI
incidentGR.addQuery("priority", 1);

// executes SQL query and returns data in JS object - stage 1 ends
incidentGR.query();

// looping through all returned records; next() method to determine if there are any other records in the array
while(incidentGR.next()) {
	gs.print(incidentGR.number); // using GlideSystem to print to screen
}
```
   
   
See also: [Dot-Walking](../devlog/Dot-Walking.md)   
   
   
---   
   
## GlideRecord API Diagram   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1668012318/wiki/hsutdooc3poqedjdzrcg.png)   
   
   
See also: [UML diagram](../devlog/UML%20diagram.md)   
   
## Common GlideRecord methods   
   
   
- query()   
- newRecord()   
- insert()   
- update()   
- deleteRecord()   
- addQuery()   
- addEncodedQuery()   
- hasNext()   
- next()   
- get()   
- orderBy()   
- orderByDesc()   
- canCreate()   
- canRead()   
- canDelete()   
   
## Options to Build Queries    
   
1. Chain Methods   
   
Add GlideRecord methods onto the current GlideRecord object.   
   
```js
var incidentGR = new GlideRecord('incident');
var onCond1 = incidentGR.addQuery('priority', '1');
orCond1 = incidentGR.addQuery('category', 'hardware');
incidentGR.addQuery('sys_created_on', '>', '2017-01-01 12:00:00');
incidentGR.addNotNullQuery('short_description');
incidentGR.query();
```
   
   
   
- addQuery()   
- addOrCondition()   
- addNullCondition()   
- addNotNullQuery()   
- addActiveQuery()   
- addInactiveQuery()   
   
2. Encoded Query   
   
Build query using condition builder, copy the query and add to `addEncodedQuery()`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1668014530/wiki/uolbctnt7xqftnt9yww1.png)   
   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addEncodedQuery("<copied-query>")
incidentGR.query();
```
   
   
## addQuery()   
   
   
- Accepts 2 or 3 arguments   
   
**2 Arguments**   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addQuery('<field_name>', '<field_value>')
```
   
   
**3 Arguments**   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addQuery('<field_name>', '<operator>' '<field_value>') 
```
   
   
## next()   
   
After we run the `query()` on a GlideRecord object, we receive an iterable object. A list of the records are inside the instantiated GlideRecord object(such as `incidentGR`) that you can iterate over using `next()`.   
   
## Accessing a Record’s Fields   
   
   
- Once `query()` method is executed and stage 2 begins, all fields are just a dot away.   
- Fields become GlideRecord properties.   
   
## get()   
   
Instead of writing multiple lines to just a specific record, you can `get()` method as a shortcut which is commonly used with the `sys_id` of the record.   
   
```js
var gr = new GlideRecord('incident');
//gr.get('<sys_id>') // or
gr.get('number', 'INC0000001');
gs.print(gr.short_description);
```
   
   
## CRUD   
   
**Create**   
   
1. Build GlideRecord   
2. query()   
3. newRecord()   
4. Set field values   
5. insert()   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.query();
incidentGR.newRecord();
incidentGR.short_description = 'Test 123'; // along with other fields
incidentGR.insert(); // record isn't saved until this is executed
```
   
   
**Read**   
   
1. Build GlideRecord   
2. Add filter conditions(optionally)   
3. query()   
4. next()   
5. Print or copy variables   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addQuery('priority', '1');
incidentGR.query();
while(incidentGR.next()){
	// Read record(s)
	gs.print(incidentGR.number)
}
```
   
   
**Update**   
   
1. Build GlideRecord   
2. Add filter conditions(optionally)   
3. query()   
4. next()   
5. Set field values   
6. update()   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addQuery('priority', '1');
incidentGR.query();
while(incidentGR.next()){
	// Update record(s)
	incidentGR.priority = '2';
	incidentGR.update();
}
```
   
   
**Delete**   
   
1. Build GlideRecord   
2. Add filter conditions(optionally)   
3. query()   
4. next()   
5. deleteRecord()   
   
```js
var incidentGR = new GlideRecord('incident');
incidentGR.addQuery('number', 'INC0000001');
incidentGR.query();
while(incidentGR.next()){
	// Delete record(s)
	incidentGR.deleteRecord();
}
```
   
   
   
---   
   
See also:: [GlideRecordSecure](../devlog/GlideRecordSecure.md), [GlideAggregate](../devlog/GlideAggregate.md)