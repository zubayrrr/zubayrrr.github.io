---
created: 1662243853853
desc: ''
id: 8eczvf96b9dd9s5ghqwyaxu
title: Microservices
updated: 1662323862221
---
   
Introduction to [microservices](../devlog/microservices.md) in [kubernetes](../devlog/kubernetes.md).   
   
**Overview**   
   
   
- Benefits of having Microservices.   
- Microservices in a K8s cluster.   
   
K8s emerged as a Platform for Microservices Applications.   
   
The traditional monolith applications that evolved into multiple smaller applications that can be developed, deployed and managed independently. Each business functionality is encapsulated into its own Microservice. This results in cleaner code, less interconnected logic, more fault tolerance.   
   
**How do Microservices communicate?**   
   
1. Service-to-Service API calls(interfaces).   
2. Third-party Message Broker application.   
   
   - Lesser code complexity.   
   - Redis   
   - RabbitMQ   
3. Service Mesh architecture.   
   
   - Instead of having a centralized message broker that handles all the communication, each MS has it's own helper program([SideCar Container](/not_created.md)) that handles the communication for that MS.   
   - Istio   
   
   
---   
   
**A DevOps engineer's responsibility in regards to MS**   
   
   
- You might get tasks like deploying an existing(already developed) MS application in a K8s cluster.   
- You need to have information about the MS to be able to deploy, you'll get this information from the Devs.   
  - How many total MS that you need to deploy?   
  - Which MS is talking to which MS?   
  - How are they communicating with each other?   
    - If they're using API calls, Message Broker or a Service Mesh.   
      - What application are they using to get this done?   
  - What DBs are they using or if there are any third-party services involved?   
  - On which Port does each MS run?   
- Using the information you can:   
  - Prepare the K8s env.   
  - Create Secret, ConfigMaps   
  - Deploy third-party services/apps.   
  - Create Deployment & Service manifest files for each MS.   
  - Decide which namespaces are the MS going to belong?