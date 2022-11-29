---
aliases:
- ServiceNow.Import Sets
- Import Sets
category: '2022'
created: 1665687089000
desc: ''
id: 4a97da14-f72b-4f8b-ad69-3ca13467f1dc
title: Import Sets
updated: 1665687089000
---
   
   
- Import data into a staging table and transform (cleanse) the data before stored in the desired target table.   
- Powerful & flexible   
- Data sources   
	- Database connectors(JDBC, ODBC, web services, CSV, XML, Excel, FTP, REST or SOAP Integrations and more.   
- Transform mapping (transform data from the source table to target table)   
- They can leverage scripts for more advance functionality.   
- The data coming in can either be stored in a staging table or if there is not need to transform the data, it can directly be stored on the target table.   
   
## Import Process   
   
**Load Data** — will create an Import Set automatically for us. It uses columns in the document and creates related fields in the staging table.   
   
**Create Transform Mapping** and  configure mapping for each data point from it’s source table to it’s target table. Transform maps may be created before the data is loaded into the system(if you already have the understanding of fields being imported).   
   
**Transform Data** from source table to it’s target table.    
   
## System Import Sets Application   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665687705/wiki/xgytdbblvqnwvngl0t3r.png)   
   
## Create an Import Sets   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665690958/wiki/ksxzhgmfczcbnum4wluq.png)   
   
We’ll use this sheet as our data to be loaded, then transformed (transform map).   
   
**Load Data** module   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665691816/wiki/nvfi07amngt8e6vjsvnf.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665691842/wiki/yp4awpr3cloykk6abxjz.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665691894/wiki/ekziwsjnvlfcpxwtpl9l.png)   
   
Click on **Loaded data** link will take you to newly created staging table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665692016/wiki/rafpqjbb2pc1ljqlimki.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665692046/wiki/ifrfikadhbqrc4h6z1c7.png)   
   
**Create Transform Map**   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665692273/wiki/hccdhb0meygz71yzt8yg.png)   
   
Go to the newly created Transform Map form view.   
   
Click on **Auto Map Matching Fields** under Related Links to auto populate fields.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665692395/wiki/td4stup1uwjbzremndxp.png)   
   
For the 6th field, create one using the New button or use **Mapping Assist**.   
   
You can define mapping between source and target fields.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665692500/wiki/mxgjacr1uwpkrtoyhjhi.png)   
   
   
If we were updating EXISTING records, we can use **Coalesce** field to find a record for the defined field from the target table and update it accordingly. If it doesn’t find it, you can specify to ignore or create a new record.   
   
**Run Script**   
   
Use scripts to perform logic on every row in the source table.   
   
**Transform Script**   
   
Run a script **onStart**, **onReject**, **onForeignInsert**, **onComplete**, **onChoiceCreate**, **onBefore**, **onAfter** — transforming a record.   
   
**Run Business Rules**   
   
When selected, when the new records are inserted into the target table, it will run business rules on that target table. (typically you won’t)   
   
On **Table Transform Map** click on **Transform** link under Related Links, choose the import set and transform.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665693422/wiki/ydneeufywgc08prjryfg.png)   
   
This will finally insert out records in the target table from the staging table.   
   
You can check the **Transform History** for additional information.   
   
Check `sys_user` table to confirm your user import.   
   
`sys_user.list` and sort by created.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665693553/wiki/pnpcu6hje29vphz1iv42.png)   
   
## Data Sources   
   
You can make connections to Data Sources instead of uploading files.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665693714/wiki/eqaanadxeg1bft9qsp5u.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665693840/wiki/pkjvywmixbrx77y1dd3t.png)   
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1665693864/wiki/h1xv2xh5ujh1xdumjkyi.png)