---
created: 1655890045974
desc: ''
id: jew452yotysgzsmcmgmzj6j
title: Web Server & Application Server
updated: 1655890767017
---
   
## Web Server   
   
A web server is a computer system that stores, processes, and delivers web pages to clients. The client is almost always a web browser or a mobile application. Depending on the setup, a web server can store one or more websites.   
   
This type of server only delivers static HTML content, such as:   
   
   
- Documents   
- Images   
- Videos   
- Fonts   
   
Traditionally, web servers do not deal with dynamic content or server-side programming. Web servers accept and fulfill Hypertext Transfer Protocol (HTTP or HTTPS) requests only. Optionally, you can add components for dealing with dynamic content.   
   
## Application Server   
   
An application server is a software framework that delivers content and assets for a client application. Clients include web-based applications, browsers, and mobile apps.   
   
Application servers provide clients with access to business logic. Through business logic, an app server transforms data into dynamic content and enables the functionality of the application. Examples of dynamic content are:   
   
   
- A transaction result   
- Decision support   
- Real-time analytics   
   
This server type is the main link between a client and server-side code. Typical tasks of an application server include:   
   
   
- Transaction management   
- Security   
- Dependency injection (DI)   
- Concurrency   
   
Application servers also handle processes such as clustering, fail-over, and load-balancing.   
   
## Comparisons   
   
When web browsers became the main application clients, the line between app and web servers got blurry.   
   
Most web servers have plugins for scripting languages (ASP, JSP, PHP, Perl, etc.) that enable dynamic content generation. For example, if we add a .NET plugin to an IIS environment, we can connect the web server to server-side code and serve clients with dynamic content.   
   
There is an overlap on the app server’s side too. Many application servers offer web server capabilities and use HTTP as a primary protocol.   
   
Because of the overlap in use cases and technology, most popular servers are hybrids of the two types. A hybrid solution that combines server capabilities ensures optimal system speed and functionality.   
   
   
- **Web servers and application servers have one thing in common – they need a dedicated server to run the software.**   
- **For an inexpensive way of hosting a static website, consider using** [Object Storage](../devlog/Object%20Storage.md).   
   
| **Web Servers**                                              | **Point of Comparison** | **Application Servers**                                                                                            |   
| ------------------------------------------------------------ | ----------------------- | ------------------------------------------------------------------------------------------------------------------ |   
| Hosts websites and responds to simple web requests           | Main purpose            | Hosts applications and delivers complex interactions through business logic                                        |   
| Only delivers static content via HTML                        | Type of content         | Delivers static and dynamic content                                                                                |   
| HTTP/HTTPS protocols only                                    | Protocols               | The client-server interaction can occur via several protocols, including HTTP/HTTPS                                |   
| No                                                           | Application connection  | Yes                                                                                                                |   
| Has access to a static database                              | Database connection     | Has access to the application database                                                                             |   
| Web browsers                                                 | Typical client          | Serves web and mobile applications, and web browsers                                                               |   
| Does not support multi-threading                             | Multi-threading         | Uses multi-threading to process multiple requests in parallel                                                      |   
| Facilitates traffic that does not consume a lot of resources | Resource consumption    | Facilitates resource-intensive processes                                                                           |   
| Web container only                                           | Containers              | Web container (Servlets, JSP, JSF, web services), EJB container (JTA), Application Client container (DI, security) |   
| Very low                                                     | Capacity                | High                                                                                                               |   
| A hypertext document that displays information on a browser  | Interaction result      | Files that contain data and serve a specific purpose depending on the client needs                                 |   
   
Via - [Web Server vs. Application Server: What Are the Differences?](https://phoenixnap.com/blog/web-server-vs-application-server)