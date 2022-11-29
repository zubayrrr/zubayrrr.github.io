---
aliases:
- ServiceNow.Receive REST calls
- Receive REST Calls
category: '2022'
created: 1666209858329
desc: ''
id: dcebd48d-42ab-43c7-9f09-abfc72d56092
title: Receive REST Calls
updated: 1666209858329
---
   
**Receiving instance** requires    
   
   
- Authentication (user)   
- Authorization (role)   
- Table API (or)   
- Import Set API (or)   
- Scripted API    
   
## Receive REST Calls (using Postman)   
   
**In ServiceNow REST API Explorer**   
   
   
- POST method to create a new record   
- Choose “Incident” table    
- Under “Request Body”, use Builder to create Short description and Description json.   
- For auth, create a new user with the role `rest_service` assigned.   
   
**In Postman**   
   
   
- Set username and password in the Authorization tab with the user you created with the required role.   
- Set the URL endpoint   
- Content-Type “application/json” in the Headers   
- Paste the string you generated in ServiceNow in the Body “raw” section.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209208/wiki/elopohez0ldzmbweqli4.png)   
   
Send the POST request   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209172/wiki/mhof9lflzi7ohyh9fcdo.png)   
   
Incident created successfully using a POST request    
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209395/wiki/ifr6l4gzqmq3bkwdxyex.png)   
   
We can modify a previously created record using PUT method, you’ll need `sys_id` for that though.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209600/wiki/whabnjnod7jfsay5uqep.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209689/wiki/sym8qmth13bkgcw3bdfx.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666209707/wiki/w3efjcqca5p3e8xkloz4.png)