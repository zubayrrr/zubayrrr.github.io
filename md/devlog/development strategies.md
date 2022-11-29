---
created: 1660857342102
desc: ''
id: sabgbxemlulaw0wasgq489r
title: Development Strategies
updated: 1660857598825
---
   
Topics::  [devops](../topics/devops.md)   
   
   
---   
   
A deployment strategy is any technique employed by DevOps teams to successfully launch a new version of the software solution they provide. These techniques cover how [network traffic](https://en.wikipedia.org/wiki/Network_traffic#:~:text=From%20Wikipedia%2C%20the%20free%20encyclopedia%20Network%20traffic%20or,packets%2C%20which%20provide%20the%20load%20in%20the%20network.) in a production environment is transitioned from the old version to the new version. Based on the firm’s specialty, a deployment strategy can influence downtime and the company’s operational cost.   
   
## **Various Types of Deployment Strategies**   
   
Now that we understand what deployment strategies are, let’s explore the various types of deployment strategies.   
   
### **Blue/Green Deployment**   
   
In this type of deployment strategy, the new version of the software runs alongside the old version. Note that you can also refer to this as **red/black deployment strategy** in some cases.   
   
Here, the stable or the older version of the application is always **blue or red**, while the newer version is **green or black**.   
   
After the new version has been tested and certified to meet all the requirements, the load balancer automatically switches the traffic from the older version to the newer version.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-159Deployment-Methods-1024x318.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-159Deployment-Methods-1024x318.png)   
   
The major advantage of this strategy is that it avails a quick update or rollout of a new application version. However, its main disadvantage is that it is costly because you must run both the new and old versions concurrently. Engineers mostly use this method in mobile app development and deployment.   
   
### **Canary Deployment**   
   
In canary deployment, the deployment team sets up the new version and then gradually shifts the production traffic from the older version to the newer version. For example, at a point in time during the deployment process, the older version might retain 90% of all traffic for the software while the newer version hosts 10% of the traffic. This deployment technique helps the DevOps engineers test the stability of the new version. It uses live traffic from a subset of the end-users at different levels that varies as production occurs.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-160Deployment-Methods-931x1024.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-160Deployment-Methods-931x1024.png)   
   
Canary deployment enables better performance monitoring. It also aids in a faster and better rollback of the software if the new version fails. However, it has a slow nature and a more time-consuming deployment cycle.   
   
### **Recreate Deployment**   
   
In this deployment strategy, the dev team shuts down the old version of the application entirely, deploys the new version, and then reboots the whole system. This deployment technique creates a system downtime between shutting down the old software and booting the new one.   
   
It is cheaper and mainly used when the software firm wants to change the application from scratch. It doesn’t require a load balancer as there’s no shifting of traffic from one version to another in the live production environment.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-161Deployment-Methods-962x1024.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-161Deployment-Methods-962x1024.png)   
   
But this strategy dramatically affects the end users due to the downtime. Users must wait until the application goes live again to use the software. As a result, not many developers use this strategy unless they have no other choice.   
   
### **Ramped Deployment**   
   
The ramped deployment strategy gradually changes the older version to the new version. Unlike canary deployment, the ramped deployment strategy makes its switch by replacing instances of the old application version with the instances from the new application version one instance at a time. You can also call this method the **rolling upgrade deployment strategy**.   
   
When developers replace all instances of the older version, they shut down the older version. The new version then controls the whole production traffic.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-162Deployment-Methods-1024x862.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-162Deployment-Methods-1024x862.png)   
   
This strategy gives zero downtime and also enables performance monitoring. Nevertheless, the rollback duration is long in case there is an unexpected event. This is because the downgrading process to the initial version follows the same cycle, one instance at a time.   
   
### **Shadow Deployment**   
   
In this deployment strategy, developers deploy the new version alongside the old version. However, users can’t access the new version immediately. Just as the name suggests, the latest version hides in the shadows. Developers send a fork or copy of the requests the old version receives to the shadow version to test how the new version will handle the requests when live.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-163Deployment-Methods-1024x467.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-163Deployment-Methods-1024x467.png)   
   
This technique is very complex, and as such, the DevOps engineer should be careful so that the forked traffic does not create a duplicate live request since two versions of the same system are running.   
   
Shadow deployment lets engineers monitor system performance and conduct stability tests. But it’s expensive and complex to set up and can create serious issues.   
   
### **A/B Testing Deployment**   
   
In A/B testing deployment, developers deploy the new version alongside the older version. However, the new version is only available to a subset of users. These users are selected based on specific conditions and parameters the engineers choose. These parameters can be the user’s location, type of device, UI language, and operating system.   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-164Deployment-Methods-1024x740.png)   
   
![](https://1ohvy81v7br01wtgnj4bf0ek-wpengine.netdna-ssl.com/wp-content/uploads/2022/05/Asset-164Deployment-Methods-1024x740.png)   
   
This method measures the effectiveness of the application’s new functionality. After gathering statistics from performance monitoring, developers roll out the version that yielded the best results to all users.   
   
Real-time statistical data can help developers make important and favored decisions about their software. However, A/B testing is very complex to set up. It also requires a highly intelligent (and pricey) load balancer.   
   
> — via [Deployment Strategies: 6 Explained in Depth - Plutora](https://www.plutora.com/blog/deployment-strategies-6-explained-in-depth)