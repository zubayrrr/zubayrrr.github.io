---
created: 1663326587082
desc: ''
id: brw2hzx5wlzx7b7ki8sfdfb
title: Data Policies
updated: 1663329487848
---
   
You can think of Data Policies as UI Policies but for the backend. Data Policies restrict data on the server side as opposed to UI Policies which restrict the data on the client side.   
   
If you're using Web services or import sets, Data Policies are used to put restrictions on the data coming through.   
   
**Use cases**   
   
1. Require the **Type** field on the Change form, for web services.   
2. Require the **Close notes** on an Incident before changing the status to 1/**Resolved**.   
   
It'll completely prevent the update if the requirements are not satisfied.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663329527/wiki/j4ft6alnm8m0mh7l1ncz.png)   
   
Example:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663330576/wiki/ulblsydin3m58xdizdx3.png)   
   
We can even convert this Data Policy to a UI Policy.   
   
   
Example, a knowledge article cannot be created unless a knowledge base is supplied.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1663330683/wiki/ghxvwnswjeimqausddqv.png)