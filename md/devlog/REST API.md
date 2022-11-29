---
created: 1655201145936
desc: ''
id: uyh79om67wv7vcvrot3u481
title: REST API
updated: 1655713433309
---
   
REST APIs (Representational State Transfer Application Programming Interface) is a data source’s frontend that allows users to create, retrieve, update, and delete data items. An API is frequently a portal to the rest of the world for developer teams.   
   
A REST API is a set of HTTP-based standards that control how different applications communicate with one another. There are 4 basic methods, which are also referred to as CRUD operations:   
   
   
- POST: Create a record.   
- GET: Read a record.   
- PUT: Update a record.   
- DELETE: Delete a record.   
   
REST APIs add no new capability to [HTTP API](../devlog/HTTP%20API.md)s. But it is an architectural style that was created in tandem with HTTP and most typically employs HTTP as its application layer protocol. However, REST isn’t always linked to HTTP. You can use other transfer protocols, such as FTP, SMTP, etc. and your API can still be RESTful.   
   
The majority of HTTP APIs are on the verge of becoming completely RESTful. But not all HTTP APIs are REST APIs. To be termed a REST API, the API must meet the following architectural requirements:   
   
   
- **Client-Server:** A server oversees the application’s data and state in REST applications. The server connects with a client, which is responsible for handling user interactions. The two components are separated by a clear separation of responsibilities. As a result, you’ll be able to update and upgrade them in separate tracks.   
   
   
- **Stateless:** Client state is not maintained by servers; instead, clients handle their own application state. All of the information needed to process the client’s requests are contained in the requests to the server.   
   
   
- **Cacheable:** Servers must indicate whether or not their responses are cacheable. To boost performance, systems and clients might cache replies when it is convenient. They also get rid of non-cacheable data, so no client has to deal with stale data.   
   
   
- **Uniform Interface:** REST’s most well-known characteristics are that the emphasis on a uniform interface between components is the primary aspect that distinguishes the REST architectural style from other network-based approaches. Data is provided as resources through REST services, which have a consistent namespace.   
   
   
- **Layered System:** The system’s components can’t look beyond their own layer. This limited scope makes it simple to add load-balancers and proxies to increase authentication security and performance.   
   
Via - [HTTP API vs REST API: 3 Critical Differentiators - Learn | Hevo](https://hevodata.com/learn/http-api-vs-rest-api/)   
   
```json
//request
GET api/customers/10

//response
            {
           "customer":{
              "id":"10",
              "name": "customer name",
              "age": "28"
           }
        }
```
