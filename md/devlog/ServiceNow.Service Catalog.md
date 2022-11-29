---
created: 1665629757014
desc: ''
id: 54qm9mg0pwoc6uprt9rw6ps
title: Service Catalog
updated: 1665629757014
---
   
> “With the ServiceNow Service Catalog application, create service catalogs that provide your customers with self-service opportunities.” — ServiceNow Docs   
   
   
- Service Catalog allows an organization to provide it’s users an “Amazon like” experience for requesting services.   
- Service Catalog supports multiple catalogs and categories.   
- Think of catalog as department specific like HR, IT.   
- Users can track their requests.   
- The Service Catalog application is comprised of many tables.   
  - `sc_cat_item` stores the actual catalog item.   
  - `sc_cart` stores user cart records.   
  - `sc_request`   
  - `sc_req_item`   
  - `sc_task`   
   
## Service Catalog Features   
   
   
- Requests → Requested Items → SC Tasks   
- Record producers   
  - Used to create new records via a configurable form.   
  - It allows admins to create a “Raise a ticket” form. Much more user friendly than something like an [ServiceNow.Incident](../devlog/ServiceNow.Incident.md) Form View.   
- Order guides   
  - To group multiple catalog items in a single form view. Example: a new hire order guide.   
- Variable sets   
- Workflows   
  - Can be attached to each catalog item.   
  - Typically it is recommended to use a generic workflow for a group of catalog items.   
- User criteria   
   
## Service Catalog - Self Service   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665595680/wiki/zyl2wyyemlcuuclseizy.png)   
   
Order status page   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665595776/wiki/hf1ycfonixo2ueyfgsop.png)   
   
Request   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665596045/wiki/padbluztsprcc3xrb7wo.png)   
   
Request Workflow   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665596106/wiki/u27rzowedkeof5leitdk.png)   
   
Requested Item   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665596200/wiki/mywd0rzo2qi8hopvdsgn.png)   
   
RITM Workflow   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665596399/wiki/nvry9i6ge9p0o5mkwtri.png)   
   
Catalog Task   
   
SC Task - a task that needs to be completed before this request can be completed.   
   
Upon closing the task and the subsequent tasks - the RITM will be completed.   
   
## Service Catalog   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665597282/wiki/efreimbtlr6xqlyvd2gy.png)   
   
### Catalogs   
   
Categories of Catalog items   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665597314/wiki/gwtrfymn2oi2dg4apgu0.png)   
   
### Open Records   
   
   
- Requests   
- Request Items   
- (Service Catalog) Tasks   
   
### Catalog Definitions   
   
This is where we define and maintain the catalog structure.   
   
### Content Items   
   
To direct a user to different modules so as to guide them.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665602737/wiki/wjtsfrrhtosvfjojqhn8.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665602784/wiki/aw70mmvabw7zh2wxwoku.png)   
   
## Order Guides   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603116/wiki/fou5dtxfpzdsobx7na2j.png)   
   
New hire guide   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603178/wiki/jeb4yuinstepzgtsig9y.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603202/wiki/uvd2zoo2s9uthtebj0ul.png)   
   
New hire: order guides are wizards that are dynamic that helps an admin to get a new hire get started.   
   
Variables or questions being asked. Rule base are the logical changes that happen upon selecting certain options.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603501/wiki/hcnmd2hvun4w5wgmwfye.png)   
   
## Record Producers   
   
Power tool to create records on essentially any table in the system through a nicer, more user friendly form view.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603706/wiki/rbws94491so8i2mz4h05.png)   
   
Create Incident Record Producer   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603825/wiki/brjvbzgpvvsnmebvivak.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603862/wiki/cu8ephu4ilcgzamewoxb.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665603938/wiki/sinqlixsijutmwtughe4.png)   
   
## User Criteria   
   
User criteria is used to define a group of users on the platform and provide them roles.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665604017/wiki/kpqxazgncbqpb2r2wj0a.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665604108/wiki/zvndjqknnnedudaskwcv.png)   
   
## Variable Sets   
   
They help you with a group of catalog items that all share/use same variables. Instead of replicating the same variables/questions for 10 catalog items you can use variable sets instead.   
   
## Catalog Item   
   
   
- A catalog item is a good or service. If something can be ordered by itself it is a catalog item.   
- Use a catalog item to publish a service to your users. Add a service description, images and a workflow to determine the approval and fulfilment processes for the catalog item.   
- Use variables to present and gather information from the users. Catalog UI Policies and Catalog Client Scripts can also be added to control the item behaviour based on user input   
- It also supports request management.   
- Once you submit the order through catalog item:   
	- - Request → Requested Item (RITM) → SC Tasks   
   
## Types of Catalog Items   
   
   
- **Record Producers**: they can be used to provide alternate ways of adding information such as incidents via the service catalog.   
- **Order Guides**: to group multiple catalog item in one request.   
- **Content Items**: Catalog item which provide information instead of goods or services.   
   
## Variables of Catalog Item    
   
   
- Date   
- Container variables   
- Duration    
- Email    
- HTML   
- Label    
- List collector    
- Lookup Multiple Choice    
- Multiple Choice    
- URL   
   
   
## Catalog UI Policies   
   
   
- They control the behaviour of catalog item forms when presented to your users. Catalog UI Policies can be applied to catalog item or a variable set. it will be especially applicable to catalog items.   
   
## Client-side Scripts   
   
They can add dynamic effects and validation to forms. Scripts can be applied to service catalog items or variable sets, allowing administrators to use the same functionality that is available on other forms.