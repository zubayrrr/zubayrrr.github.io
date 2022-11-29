---
aliases:
- ServiceNow.Send REST calls
- Send REST Calls
category: '2022'
created: 1666209900837
desc: ''
id: d95b3d5a-236b-4a49-848c-b9f1a86a9715
title: Send REST Calls
updated: 1666209900837
---
   
## POST   
   
**Sending Instance** requires   
   
   
- REST messages created   
- REST message methods   
- Authentication    
- Trigger - Business Rule/UI Action   
   
**Update Sets**   
   
A good practice is to have Update Sets created so that it will track all the changes you may do — which will be useful when moving the changes to Test. Prod instances.   
   
Note: **This is something we wouldn’t do in real life, this just for testing endpoints**, we’d instead rely on trigger the REST messages from UI Actions or Business rules scripts.   
   
**Create REST Message**   
   
   
- Basically we’re going to clone whatever incidents we make on instance \#1 to instance \#2(target).   
- The endpoint should be the target instance's URL or any other systems like IdentityNow   
- Authentication Type: Basic   
	- Basic auth profile: create a new one or use existing    
	- This newly created user should also be created on the Instance \#2   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666212969/wiki/jnrru6sexdlvgwhjupu0.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666213203/wiki/hpb9xgogvpccsldapgyh.png)   
   
Make sure to edit the role `rest_service`   
   
REST Message would look like:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666213410/wiki/rcr9ky1ciketureje7bv.png)   
   
A default HTTP method, GET will be created along with the REST message to “get” records from the instance \#2.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666213600/wiki/uvgkppnoiulyjz7m3wn0.png)   
   
Click on **Test** link BUT before you do that make sure the user `incident_cloner` on instance \#2 has `itil` role to make sure that it has access to the `incidents` table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666213976/wiki/jplyptq6uocceaafiyao.png)   
   
**Create a REST Method**   
   
A new POST method on our REST message to create an incident record in the target instance’s incident table.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666220016/wiki/motqz6jbzmh98zploduy.png)   
   
Fields on the target instance’s table to be mapped with our capture fields.   
   
```json
{
  "short_description": "${sd}",
  "description": "${desc}",
  "contact_type": "${ctype}"
}
```
   
   
**Create a Business Rule** (to trigger REST call)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666220325/wiki/zuv825nnxzysymtcvx1d.png)   
   
Under the “Advanced” tab we’ll be running our script that actually does the work.   
   
```js
(function executeRule(current, previous /*null when async*/) {

	var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "create_incident");
	req.setStringParameterNoEscape("sd", current.short_description);
	req.setStringParameterNoEscape("desc", current.description);
	req.setStringParameterNoEscape("ctype", current.contact_type);
	req.execute();

	var resBody = res.getBody();
	var resStatusCode = res.getStatusCode();

	gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");

})(current, previous);
```
   
   
Trigger Business Rule by creating an incident with “Application Development” for “Assignment group”.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666273012/wiki/lyqfjpzbnc3k1z2vqwrj.png)   
   
Go to instance \#2 to check if the incident was successfully cloned.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666273161/wiki/b4aakffsjb2moi34g8tn.png)   
   
Yay!! it worked.   
   
Check the logs to find what was received back (System Logs > All)   
   
   
---   
   
Updating an existing incident in instance \#1 will not update it on instance \#2 to be able to **UPDATE** an incident on instance \#2 we’ll have to  make a new HTTP method on our REST message and provide it with the `sys_id`, we’ll do this by parsing the response body for the `sys_id` and store it so it may be referenced later.   
   
Where do we store the `sys_id` that we get back from instance \#2? We’ll create  a new field (`Client Reference`) with string type on the **Create New Incident** form and update the field after every REST call.   
   
You will have to dot-walk the JSON object(response body) to get to the `sys_id`.   
   
Let’s start with creating the **Client Reference** field and then update the business rule logic.   
   
(Create New Incident Form > Form Layout)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666276875/wiki/ddqltl8qywdukcvm2woz.png)   
   
   
```js
(function executeRule(current, previous /*null when async*/) {

	var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "create_incident");
	req.setStringParameterNoEscape("sd", current.short_description);
	req.setStringParameterNoEscape("desc", current.description);
	req.setStringParameterNoEscape("ctype", current.contact_type);
	req.execute();

	var resBody = res.getBody();
	var resStatusCode = res.getStatusCode();

	var resObj = JSON.parse(resBody)
	current.u_client_reference = resObj.result.parent.sys_id;
	// current.update();

	gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");

})(current, previous);
```
   
   
   
An alternative would be to make the business rule run `before` and not have `current.update()` but it might be slow as it would wait for response back from the instance \#2.   
   
Best practice is to use an `async` business rule on **When to run**. **DO NOT USE** `current.update();` inside your business rule as it’ll lead to a loop.   
   
A more efficient way of having this functionality is to use a script include instead.   
   
```js
var incident_cloner = Class.create();
incident_cloner.prototype = {
    initialize: function() {
    },
	
	triggerCreate :function(incGR){
		var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "create_incident");
	req.setStringParameterNoEscape("sd", incGR.short_description);
	req.setStringParameterNoEscape("desc", incGR.description);
	req.setStringParameterNoEscape("ctype", incGR.contact_type);
	var res = req.execute();
	var resBody = res.getBody();
	var resStatusCode = res.getStatusCode();
	var resObj = JSON.parse(resBody);
		
	var incUpdateGR = new GlideRecord("incident");
		incUpdateGR.addQuery("sys_id", incGR.sys_id);
		incUpdateGR.query();
		if(incUpdateGR.next()){
			incUpdateGR.u_client_reference = resObj.result.sys_id;
			incUpdateGR.setWorkflow(false); // doesn't trigger any other business rules, only updates client reference #
			incUpdateGR.update();
		}

	gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");
	},
    type: 'incident_cloner'
};
```
   
   
Script include trigger inside business rule:   
   
```js
(function executeRule(current, previous /*null when async*/) {

	new incident_cloner().triggerCreate(current);

})(current, previous);
```
   
   
Create a new incident record and it should be automatically copied to the instance \#2.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666290030/wiki/mixjahdphr6mz4cnmh7f.png)   
   
The client reference field should also be filled. But currently you’re not using the appropriate endpoint for updating the record.   
   
Go to REST message and create a new PUT method with the endpoint with `sys_id`   
   
Add this function to script include   
   
```js
		triggerUpdate :function(incGR){
		var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "update_incident");
	req.setStringParameterNoEscape("sd", incGR.short_description);
	req.setStringParameterNoEscape("desc", incGR.description);
	req.setStringParameterNoEscape("ctype", incGR.contact_type);
	req.setStringParameterNoEscape("client_sysid", incGR.sys_id);
	var res = req.execute();
	var resBody = res.getBody();
	var resStatusCode = res.getStatusCode();
	var resObj = JSON.parse(resBody);


	gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");
	},
```
   
   
Duplicate the business rule to use the new function:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666291111/wiki/qpnbydyndafzdrpyqbei.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1666291220/wiki/vs8ztptmxaexkihnic76.png)   
   
Okay that shit worked after a few adjustments.   
   
   
---   
   
HTTP Query Parameters for `update_incident` PUT method:   
   
```json
{
  "short_description": "${sd}",
  "description": "${desc}",
  "contact_type": "${ctype}"
}
```
   
   
The script includes that actually worked:   
   
```js
var incident_cloner = Class.create();
incident_cloner.prototype = {
    initialize: function() {},

    triggerCreate: function(incGR) {
        var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "create_incident");
        req.setStringParameterNoEscape("sd", incGR.short_description);
        req.setStringParameterNoEscape("desc", incGR.description);
        req.setStringParameterNoEscape("ctype", incGR.contact_type);
        var res = req.execute();
        var resBody = res.getBody();
        var resStatusCode = res.getStatusCode();
        var resObj = JSON.parse(resBody);

        var incUpdateGR = new GlideRecord("incident");
        incUpdateGR.addQuery("sys_id", incGR.sys_id);
        incUpdateGR.query();
        if (incUpdateGR.next()) {
            incUpdateGR.u_client_reference = resObj.result.parent.sys_id;
            incUpdateGR.setWorkflow(false); // doesn't trigger any other business rules, only updates client reference #
            incUpdateGR.update();
        }

        gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");
    },

    triggerUpdate: function(incGR) {
        var req = new sn_ws.RESTMessageV2("Clone Incidents to another Instance", "update_incident");
        req.setStringParameterNoEscape("sd", incGR.short_description);
        req.setStringParameterNoEscape("desc", incGR.description);
        req.setStringParameterNoEscape("ctype", incGR.contact_type);
        req.setStringParameterNoEscape("client_sysid", incGR.u_client_reference);
        var res = req.execute();
        var resBody = res.getBody();
        var resStatusCode = res.getStatusCode();
        var resObj = JSON.parse(resBody);


        gs.log("Response Body: " + resBody + "\nStatus Code: " + resStatusCode, "Clone Incidents");
    },
    type: 'incident_cloner'
};
```
