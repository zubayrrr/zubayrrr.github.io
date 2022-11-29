---
created: 1655653910292
desc: ''
id: cwbupxqnwdcc2f9cfdsiqh9
title: AWS API Gateway
updated: 1655714012218
---
   
It is an AWS Service that enables you to create, publish, maintain, monitor and secure your own [REST API](../devlog/REST%20API.md) and [WebSockets API](../devlog/WebSockets%20API.md) [API](../devlog/API.md)s.   
   
A typical use case if for API Gateway to be the frontend to a Lambda function. A client can make an API request using HTTP and request triggers the Lambda function.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655708460/wiki/laayf5wg4dgagapwseku.png)   
   
It is like a service contract. An app gains programmatic access to AWS services or a website on the internet, through 1 or more APIs, which are hosted on API Gateway.   
   
The app is at the API’s frontend. The integrated AWS services and websites are located at API’s backend.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655708749/wiki/aruym5hykrw93hwi7lte.png)   
   
Once the app or client gains access to the website or service through API Gateway, they can use [HTTP](../devlog/http.md) GET or POST methods to access the backend data store.   
   
[REST API](../devlog/REST%20API.md) APIs provide one way communicate, applications send request through API Gateway and the service responds back synchronously. Request/Response model.   
   
[WebSockets API](../devlog/WebSockets%20API.md) APIs provide two way communication, the request and response happens but in addition to that - the backend services independently send communications through API Gateway to our frontend app. It can initiate communication(callback messages), not just send response to requests to connected clients. It supports real-time communications(like chat apps).   
   
## Users   
   
API Gateway users/developers are regular [aws.IAM](../devlog/aws.IAM.md) users.   
   
Application developers are not part of the organization hence don’t need to be IAM users. We can set them up using web identification federation techniques.   
   
## REST APIs VS HTTP APIs   
   
   
- HTTP APIs are cheaper & faster than REST APIs.   
- HTTP APIs don't have all the functionality of REST APIs.   
   
## API Gateway with [AWS Lambda](../devlog/AWS%20Lambda.md) Proxy Integration   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714141/wiki/h1jwimkyzmm7z9k5osi1.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714282/wiki/k6zm7d4i9uy3jjzxwoal.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714306/wiki/a0ngtbs5to0zmstgdwcb.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714325/wiki/om2w7oa4lv7crimstshc.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714339/wiki/bzyerzsy7aezdtcqtprk.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714417/wiki/s6wm48k762ksmp7utn4g.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655714565/wiki/mxyqn3fr2bwqd3fhbxll.png)