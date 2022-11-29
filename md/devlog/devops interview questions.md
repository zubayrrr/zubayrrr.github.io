---
created: 1655882305714
desc: ''
id: 5eybx5vd339tjnkglx8igde
title: Devops Interview Questions
updated: 1656161299068
---
   
1. **EC2 instance is running out of disk space. What actions will you take to mitigate the issue?**   
   
   
- [aws.EC2](../devlog/aws.EC2.md) disk space typically refers to [AWS EBS](../devlog/AWS%20EBS.md) volume.   
- We'll first check if its a root volume or any other volume   
  - /root - OS   
  - /application - for all our applications   
- If its root volume then we'll first try to check logs(`/var/logs`) and clear some space if not the instance might shut down.   
- If its the application volume(learn the reason of high disk usage), then we'll use EBS feature to take the snapshot and increase disk space for the EC2 instance.   
   
2. **Explain different ways in which** [prometheus](../devlog/prometheus.md) **can get metrics?**   
   
## Getting metrics   
   
How does Prometheus collect metrics from the targets?   
   
**Pulling**   
   
Your application(regardless of technology) will have to expose a metrics HTTP endpoint and Prometheus will scrape from the endpoint. By default is is: `hostaddress/metrics`.   
   
Data available in the `/metrics` endpoint should be in the correct format that Prometheus understands.   
   
Some servers expose Prometheus endpoints by default so you don't really have to do extra work for it. But many services don't have native Prometheus endpoints in which case you'd need an **Exporter**   
   
**Exporter**   
   
It is basically a script/service that fetches metrics from your target and converts them in format Prometheus understands and exposes it's converted data at it's own `/metrics` endpoint where Prometheus can scrape them.   
   
Prometheus has a list of exporters for different services like [MySQL](../devlog/mysql.md), [Elasticsearch](../devlog/Elasticsearch.md), [linux](../topics/linux.md) servers, [build automation](/not_created.md), Cloud Platforms and so on.   
   
If you want to monitor a Linux server, see: [Monitoring Linux host metrics with the Node Exporter | Prometheus](https://prometheus.io/docs/guides/node-exporter/)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656150261/wiki/xfe8c37gmzogdoin3wtx.png)   
   
Exporters are also available as Docker images. SO   
   
If you want to monitor [mysql](../devlog/mysql.md) container in a [kubernetes](../devlog/kubernetes.md) cluster, you can deploy a sidecar container of MySQL exporter that will run inside the pod with MySQL container, connect to it and start sending MySQL metrics for Prometheus and making them available at it’s own `/metrics` endpoint.   
   
**Monitoring your own applications?**   
   
   
- How many requests your applications are receiving.   
- How many exceptions are occurring.   
- How many server resources your application is using.   
   
For this you can use Client Libraries for different languages using which you can expose `/metrics` endpoint for metrics that are relevant to you.   
[Client libraries | Prometheus](https://prometheus.io/docs/instrumenting/clientlibs/)   
   
   
   
3. **What is Kubernetes kOps?**   
   
[kubernetes](../devlog/kubernetes.md) [kOps](../devlog/kOps.md) is an automation tool used to setup Kubernetes cluster. It is an alternative to `kubeadmin`.   
   
kOps can help you spin a test cluster or a small dev cluster quickly. It is not something that will help you setup managed Kubernetes cluster([aws.EKS](../devlog/aws.EKS.md)). It can create, destroy, upgrade, maintain production-grade, high availability clusters and also provision necessary cloud infrastructure(only recommended if you cannot afford managed service).   
   
It supports many cloud providers.   
   
4. **What is instance fleet in AWS?**   
   
Instance fleet in [AWS](../devlog/aws.md) refers to a configuration - information to launch a fleet or a group of [aws.EC2](../devlog/aws.EC2.md) instances, in a single API call. A fleet can launch multiple instance(mixed set) types across multiple Availability Zones using On-Demand Instance, Reserved Instance and Spot Instance purchasing options together.   
   
In the configuration you can define:   
   
   
- Separate capacity targets and maximum amount you're willing to pay per hour for On-Demand, Spot instances.   
- Specify the instance types that work best for your applications.   
- Specify how EC2 should distribute your fleet capacity within each purchasing options.   
   
The instance fleet configuration for [AWS EMR](../devlog/AWS%20EMR.md) lets you select wide variety of provisioning options for Amazon EC2 instances and helps you develop a flexible and elastic resourcing strategy for each node type in your cluster.   
   
5. **How do you pass “message” for your git commit**   
   
Use the flag `-m [message]` for your [version control.git](../devlog/version%20control.git.md) commit. Although you can commit without passing a message.   
   
`git commit -m "🔥 commit message"`   
   
6. **What application server are you familiar with?**   
   
[web server & application server](../devlog/web%20server%20%26%20application%20server.md)   
   
For Java applications, we have [tomcat](../devlog/tomcat.md) but there are different application servers for applications based on different technologies.   
   
7. **How to check logs of a Docker container/filter last 200 lines from the logs.**   
   
`docker container logs <container_name>`   
`docker container logs --tail 200 <container_name>`   
   
8. **What happens to container logs if it is restarted?**   
   
You won’t lose any logs for restarting a container but since containers are stateless, you will lose the logs if a container is **deleted**. If you want to persist logs you can use external persistent storage. You can also push the container logs to something like [AWS CloudTrail](/not_created.md) or [splunk](../devlog/splunk.md)   
   
9. **Horizontal Scaling VS Vertical Scaling**   
   
**Horizontal scaling** means scaling by adding more machines to your pool of resources (also described as “scaling out”); something like [AWS Auto Scaling Group](../devlog/AWS%20Auto%20Scaling%20Group.md), creating replicas(think [kubernetes](../devlog/kubernetes.md)). If you are hosting an application on a server and find that it no longer has the capacity or capabilities to handle traffic, adding a server may be your solution.   
   
Whereas **vertical scaling** refers to scaling by adding more power (e.g. CPU, RAM) to an existing machine (also described as “scaling up”). For instance, if your server requires more processing power, vertical scaling would mean upgrading the CPUs. You can also vertically scale the memory, storage, or network speed.   
   
See: [Horizontal Vs. Vertical Scaling: How Do They Compare?](https://www.cloudzero.com/blog/horizontal-vs-vertical-scaling)   
   
10. **ReplicationController in Kubernetes**   
   
A ReplicationController is responsible for running the specified number of pod copies(replicas) across the cluster.   
   
ReplicationController is not auto scale.   
   
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx
spec:
  replicas: 3
  selector:
    app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```
   
   
11. **What is helm?**   
   
   
Helm is a Kubernetes deployment tool for automating creation, packaging, configuration, and deployment of applications and services to Kubernetes clusters.   
   
[Kubernetes](../devlog/kubernetes.md) is a powerful container-orchestration system for application deployment. There are multiple independent resources to deal with, and each requires a dedicated [languages.YAML](../devlog/languages.YAML.md) manifest file.   
   
Helm deploys packaged applications to Kubernetes and structures them into charts. The charts contain all pre-configured application resources along with all the versions into one easily manageable package.   
   
Helm streamlines installing, upgrading, fetching dependencies, and configuring deployments on Kubernetes with simple CLI commands. Software packages are found in repositories or are created.   
   
Unlike Homebrew or Aptitude desktop package managers, or Azure Resource Manager templates (ARMs) / Amazon Machine Images (AMIs) that are run on a single server, Helm charts are built atop Kubernetes and benefit from its cluster architecture. The main benefit of this approach is the ability to consider scalability from the start. The charts of all the images used by Helm are stored in a registry called Helm Workspace, so the DevOps teams can search them and add to their projects with ease.   
   
Kubernetes objects are challenging to manage. With helpful tools, the Kubernetes learning curve becomes smooth and manageable. Helm automates maintenance of [languages.YAML](../devlog/languages.YAML.md) manifests for Kubernetes objects by packaging information into charts and advertises them to a Kubernetes cluster.   
   
Helm keeps track of the versioned history of every chart installation and change. Rolling back to a previous version or upgrading to a newer version is completed with comprehensible commands.   
   
   
## Helm Chart   
   
Helm charts are Helm packages consisting of [languages.YAML](../devlog/languages.YAML.md) files and templates which convert into Kubernetes manifest files. Charts are reusable by anyone for any environment, which reduces complexity and duplicates. Folders have the following structure:   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655905668/wiki/f0iewhj44stf8t90qnfr.png)   
   
 **Name**                         | **Type**  | **Function**                                                                                                                               
   
----------------------------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------   
 **charts/**                      | Directory | Directory for manually managed chart dependencies.                                                                                         
 **templates/**                   | Directory | Template files are written in Golang and combined with configuration values from the values.yaml file to generate Kubernetes manifests.    
 **Chart.yaml**                   | File      | Metadata about the chart, such as the version, name, search keywords, etc.                                                                 
 **LICENSE (optional)**           | File      | License for the chart in plaintext format.                                                                                                 
 **README.md (optional)**         | File      | Human readable information for the users of the chart.                                                                                     
 **requirements.yaml (optional)** | File      | List of chart’s dependencies.                                                                                                              
 **values.yaml**                  | File      | Default configuration [values](https://phoenixnap.com/kb/helm-get-values) for the chart.                                                   
   
   
Via - [What is Helm? Helm and Helm Charts Explained](https://phoenixnap.com/kb/what-is-helm)   
   
## Resources   
   
   
- [What is Helm? Helm and Helm Charts Explained](https://phoenixnap.com/kb/what-is-helm)
   
   
12. **Which Python module would you use to write a simple program to test API code?**   
   
The code should just check if the API endpoint is working or not.   
   
**Answer:**   
   
I would use the **request** module in [languages.python](../devlog/languages.python.md). It has the `get()` function wherein you'd pass pass the API endpoint and fetch status/http code `.status_code`.   
   
If it returns `200` - API endpoint is working fine.   
   
13. **Which HTTP responses would you monitor and for which would you trigger alerts?**   
   
Example of API endpoints:   
   
```
/this-is-an-endpoint
/another/endpoint
/some/other/endpoint
/login
/accounts
/cart/items
```
   
   
HTTP response status codes indicate whether a specific HTTP request has been successfully completed. Responses are grouped in five classes:   
   
   
- Informational responses (100–199)   
- Successful responses (200–299)   
- Redirection messages (300–399)   
- Client error responses (400–499)   
- Server error responses (500–599)   
   
   
- If HTTP response is in the 400 or 500 range we'll trigger an alert by writing a script of setting up a monitoring service.   
   
14. **Can we run a Jenkins agent inside a docker container along with our test?**   
   
   
- Running Jenkins agent inside a [Docker](../devlog/docker.md) container is (one of) the standard way of implementing pipelines.   
- This question is focusing on isolation of pipeline steps.   
- Here the code is expected to run inside a docker container which can use a custom test image if required.   
- This is the best way to perform testing without having every [Jenkins](../devlog/jenkins.md) agent needing to have packages installed.   
- To use any kind of Docker containers, I'd add it as a part of the agent. We can call any kind of images(from DockerHub or Custom), whatever stages and test steps we mention as part of our pipeline will run inside that docker container. Multi node Jenkins setup.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1655971387/wiki/m9mcgppau59fyaewl0uw.png)   
   
15. **What are some of the ways of setting up alerts?**   
   
It is not feasible to have multiple alerting methods in one org. Alerts notifications can be Emails, Phone calls, Slack messages, etc. This ties into the [on-call](../devlog/on-call.md) management.   
   
Some of the open source methods:   
   
   
- [prometheus](../devlog/prometheus.md) -> Alertmanager   
- [aws.CloudWatch](../devlog/aws.CloudWatch.md) -> SNS   
- Nagios -> Alerting   
   
16. **Help repository to store/access helm charts**   
   
Helm repositories are a common practice to store helm charts, which can be access by our [kubernetes](../devlog/kubernetes.md) cluster as part of a deployment. This helps with versioning our helm charts, rollbacks, upgrade etc.   
   
   
- Cloudsmith   
- Jfrog Artifactory   
- [aws.S3](../devlog/aws.S3.md)   
- Google Cloud Storage   
- Artifact Hub(Open Source)   
   
17. **Jenkins multi-node setup, how to add new slave/follower to master?**   
   
Having only one node is usually not enough(availability) for any organization so a multi-node setup is required for scaling. You can add a slave/follower for a master on "Manage [Jekins](/not_created.md)" page and the option "Manage Nodes and Clouds". You will provide node info such as the IP Address, username, password etc and get it registered. We can also add slaves dynamically, you'd need an auto scaling group by your Cloud Provider.   
   
18. **How do you block an IAM user from accessing a specific S3 bucket?**   
   
It is difficult to manage bucket level policies using IAM policy. We can achieve this using [aws.S3](../devlog/aws.S3.md) bucket policy, you'd use the IAM user's ARN and “deny” the user.   
   
19. **Is a large docker image a cause of concern? How would you tackle it?**   
   
Applications can be large if they're complex and do a lot of things but if it is a simple application...large size is not warranted and can be mitigated.   
   
   
- Bigger docker image would result in longer build time.   
- Docker image downloaded(from DockerHub) may throw errors or cause API rate limit issues.   
- Application will be bulkier and harder to debug and scale.   
   
To resolve this:   
   
   
- Smaller Base Image(Alpine images).   
- Introduce Multi-stage build - from the Base image you build up your image and discard your previous image builds.   
- Remove package binaries after installing and don't install packages that are not necessary.   
- Lock your package/dependencies versions.   
   
20. **Are you aware of AWS IAM policies/can you read them?**   
   
Policy evaluation logic   
   
Example   
   
```json
{
  "Version": "2012-10-17", // version is fixed
  "Statement": [
    {
      "Sid": "AllowS3ListRead", // high level ALLOW action
      "Effect": "Allow",
      "Action": [
        "s3:GetBucketLocation", // explicitly defining what actions are allowed
        "s3:GetAccountPublicAccessBlock",
        "s3:ListAccessPoints",
        "s3:ListAllMyBuckets"
      ],
      "Resource": "arn:aws:s3:::*"
    },
    {
      "Sid": "AllowS3Self", // high level ALLOW action
      "Effect": "Allow",
      "Action": "s3:*", // everything is allowed but only limited to the below two buckets
      "Resource": ["arn:aws:s3:::carlossalazar/*", "arn:aws:s3:::carlossalazar"]
    },
    {
      "Sid": "DenyS3Logs", // high level DENY action
      "Effect": "Deny",
      "Action": "s3:*", // everything is denied for any bucket with the suffix "logs"
      "Resource": "arn:aws:s3:::*log*"
    }
  ]
}
```
   
   
Example via - [Policy evaluation logic - AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html)   
   
21. **What role does `pv` and `pvc` play in Kubernetes?**   
   
PV stands for PersistentVolume   
PVC stands for PersistentVolumeClaim   
   
Pod gets it's storage using PVC which would in turn get hold of PV which will utilize an NFS or [AWS EBS](../devlog/AWS%20EBS.md) volume.   
   
PVC will define what kind of volume and the storage amount it needs and it will search of PVs(which you'd have provisioned) and choose from those.   
   
PV can exist independently from a Pod, you don't need to have a Pod for a PV to be created.   
   
22. **When creating RDS using Terraform, how do you save DB username and password securely?**   
   
Since DB username and password are considered secrets, they cannot be saved in plaintext on a repository along with the Terraform code.   
   
You can use Hashicorp's Vault, store your secrets on your Vault.   
   
Integrate it with Terraform. In your `main.tf` you can reference it as a Data Block. Mention Vault provider in the Provider section.   
   
You can also use other secret stores/managers like [AWS Secrets Manager](../devlog/AWS%20Secrets%20Manager.md) etc. Or you can also use environment variables.   
   
23. **Have you support any DBs?**   
   
You don't need to be a DB expert but you have to have clear understanding of different kinds of DBs used, their use cases and pick one based on your experience and profile.   
   
   
- Key-value DB   
  - [Redis](../devlog/Redis.md), etcd   
- Column DB   
  - Cassandra   
- NoSQL/Document/Schemaless DB   
  - [mongoDB](../devlog/mongoDB.md)   
  - [AWS DynamoDB](../devlog/AWS%20DynamoDB.md)   
- Relational DB   
  - [mysql](../devlog/mysql.md)   
  - [AWS Aurora](../devlog/AWS%20Aurora.md)   
  - [PostgreSQL](../devlog/PostgreSQL.md)   
   
24. **How do you ensure certain packages are installed on all your EC2 instances and are persisted?**   
   
HashiCorp's [Packer](../devlog/Packer.md) is the solution. Packer is an open source tool that enables you to create identical machine images for multiple platforms from a single source template which can be written in JSON. You can use it in your multi-cloud setup or On-prem infra too.   
   
A common use case is creating "Golden Images" that teams across an organization can use in cloud infrastructure.   
   
We could also use custom [AWS AMI](../devlog/AWS%20AMI.md) images too but is limited to Cloud.   
   
25. **Differentiate Managed, Customer Managed and Inline IAM policies.**   
   
   
- Managed: Created and maintained by AWS.   
- Customer Managed: Created and maintained by customer. Custom policies created by an organization using [terraform](../devlog/terraform.md). It can be attached to multiple users or groups.   
- Inline: Created and attached directly to IAM User, Group or Role. It is created for that specific Role, User, Group ...if the Role, User or Group is destroyed, the policy is also deleted.   
   
26. **What build tools are you familiar with?**   
   
## Building Java Applications   
   
   
- Install IntelliJ IDEA.   
- Install Java(or use IDEA to Download SDK).   
- Setup JDK, SDK (make sure Java executable is added to [path](/not_created.md) or `%PATH%`, respectively.)   
- Set `JAVA_HOME` as an [environment variable](../devlog/environment%20variable.md) (Maven prerequisite).   
- Use SCM to clone(`git clone`) your Java application's repository.   
   
   
- Build a [maven](../devlog/maven.md) project.   
   
   
  - Open source code of your Java application in IntelliJ IDEA.   
  - Wait for IDEA to index the source code.   
  - IDEA will automatically detect the `pom.xml` and resolve all the dependencies.   
  - Run the application(preview in the "Run" tab).   
  - Download [Maven](https://maven.apache.org) and add it's `/bin`'s path to `$PATH` or `%PATH%`.   
  - Use `mvn` commands and profit!   
  - After building, `.jar` or `.war` files can be found in the `./target` folder.   
   
   
- Build a [gradle](../devlog/Gradle.md) project.   
   
   
  - Open source code of your Java application in IntelliJ IDEA   
  - If it has a gradle wrapper(folder) inside the repo, you don't need to install gradle   
  - Make sure the JVM configured is compatible with gradle wrapper's version.(`JAVA_HOME`)   
  - Run the application to check if everything is working fine   
  - Build with `./gradlew build`   
  - After building, `.jar` or `.war` files can be found in the `./build` folder.   
   
To run a `.jar`: `java -jar name-of-the-app-SNAPSHOT.jar`   
   
   
   
26. **Ingress and Egress**   
   
[ingress](/not_created.md) and [egress](/not_created.md)   
   
In IT they refer to:   
   
Ingress: Incoming/Inbound traffic   
Egress: Outgoing/Outbound traffic   
   
They're mostly associated with security groups([firewall](../devlog/firewall.md)). They're also associated with VPCs and subnets where we control the incoming traffic from the internet and routing the traffic between subnets.   
   
Eg: Allowing or denying ports for certain traffic([ssh](../devlog/ssh.md), [http](../devlog/http.md)). In prod, you'd usually lock it in the VPC IP Range.   
   
27. **Differentiate Docker Image and Docker Layer.**   
   
   
- Docker Layers are not separate components, you cannot have a single Docker Layer and use it. They're a subcomponent of a Docker Image.   
- But an Image can consist of a single Layer(that's often the case when running `squash` command)   
- Each Layer is an Image by itself.   
- They're generated when you run `docker container` commands.   
- Each Layer stores the changes compared to the image it's based on `docker history` can fetch you info on it's Layers.   
- Each instruction in a Dockerfile results in a layer.   
   
28. **What is bastion host or gateway server and what roles do they play?**   
   
   
A Bastion Host/Server is used to manage access to an internal or private network from an external network. It is also known as a Gateway Server or a Jump Box or a Jump Server.   
   
It basically helps with security - monitoring incoming and outgoing traffic. Bastion Host has clear user rules defined; who can access what.   
   
User will first sign into Bastion Host and get validated and proceed with SSHing into other machines. If we want to cut off all the external access to our internal servers, all we'd have to do is destroy the Bastion Host.
   
   
29. **How do you troubleshoot an Auto Scaling Group that is facing issues provisioning new nodes(it is using spot instances)?**   
   
Having an [AWS Auto Scaling Group](../devlog/AWS%20Auto%20Scaling%20Group.md) full of only spot instances is not a good idea unless the application can bear a little bit of downtime or have a back up ASG.   
   
There could be two of many causes for this:   
   
   
- Increase in spot price   
- EC2 quota limit   
   
Spot instances an be taken away from you if there is a change in bid price. Bidding high doesn't guarantee yous spot instances.   
   
There is a soft limit set of every account on how many EC2 instances you can spin up. It can be mitigated by going to AWS Support and raise a ticket for increasing quota limit.   
   
30. **Troubleshoot a Pod that is unable to access a volume due to access error.**   
   
Volumes are handled/provisioned in Kubernetes as a part of PVs.   
   
AccessMode of volume - see that your PVC or your volume supports `ReadWriteMany` permission for multi-pod access.   
   
The access modes are:   
   
   
- `ReadWriteOnce` the volume can be mounted as read-write by a single node. ReadWriteOnce access mode can still allow multiple pods to access the volume when the pods are running on the same node.   
- `ReadOnlyMany` the volume can be mounted as read-only by many nodes.   
- `ReadWriteMany` the volume can be mounted as read-write by many nodes.   
- `ReadWriteOncePod` the volume can be mounted as read-write by a single Pod. Use ReadWriteOncePod access mode if you want to ensure that only one pod across whole cluster can read that PVC or write to it. This is only supported for CSI volumes and Kubernetes version 1.22+.   
   
   
- [NFS](../devlog/NFS.md) allows `ReadWriteMany`.   
- [AWS EBS](../devlog/AWS%20EBS.md) only allows `ReadWriteOnce`.   
   
31. **How to setup K8s in AWS?**   
   
You can set them up directly on [aws.EC2](../devlog/aws.EC2.md). Using either `kops` commands or `kubeadmin`. Or you can go with [aws.EKS](../devlog/aws.EKS.md).   
   
If you want to set it up locally you'd go for `minicube`.   
   
In prod we look for stability of our environment, hence the safest bet would be to go with a managed service such as EKS. For development you can go with [kOps](https://github.com/kubernetes/kops) clusters.   
   
Code deployment should be taken care by [helm](../devlog/helm.md).   
   
32. **Explain Load Balancers in AWS.**   
   
   
What is a Load Balancer? A load balancer acts as the “traffic cop” sitting in front of your servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximizes speed and capacity utilization and ensures that no one server is overworked, which could degrade performance.   
   
If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it.   
   
## Types of Load Balancers – Based on Functions   
   
Several load balancing techniques are there for addressing the specific network issues:   
   
**Network Load Balancer / Layer 4 (L4) Load Balancer:**   
   
Based on the network variables like [IP address](../devlog/ip%20address.md) and destination ports, Network Load balancing is the distribution of traffic at the transport level through the routing decisions. Such load balancing is TCP i.e. level 4, and does not consider any parameter at the application level like the type of content, cookie data, headers, locations, application behavior etc. Performing network addressing translations without inspecting the content of discrete packets, Network Load Balancing cares only about the network layer information and directs the traffic on this basis only.   
   
**Application Load Balancer / Layer 7 (L7) Load Balancer:**   
   
Ranking highest in the [OSI model](../devlog/osi%20model.md), Layer 7 load balancer distributes the requests based on multiple parameters at the application level. A much wider range of data is evaluated by the L7 load balancer including the HTTP headers and SSL sessions and distributes the server load based on the decision arising from a combination of several variables. This way application load balancers control the server traffic based on the individual usage and behavior.   
   
**Global Server Load Balancer/Multi-site Load Balancer:**   
   
With the increasing number of applications being hosted in cloud data centers, located at varied geographies, the GSLB extends the capabilities of general L4 and L7 across various data centers facilitating the efficient global load distribution, without degrading the experience for end users. In addition to the efficient traffic balancing, multi-site load balancers also help in quick recovery and seamless business operations, in case of server disaster or disaster at any data center, as other data centers at any part of the world can be used for business continuity.   
   
## Types of Load Balancers – Based on Configurations   
   
Load Balancers are also classified as:   
   
**Hardware Load Balancers:**   
   
As the name suggests, this is a physical, on-premise, hardware equipment to distribute the traffic on various servers. Though they are capable of handling a huge volume of traffic but are limited in terms of flexibility, and are also fairly high in prices.   
   
**Software Load Balancers:**   
   
They are the computer applications that need to be installed in the system and function similarly to the hardware load balancers. They are of two kinds- Commercial and Open Source and are a cost-effective alternative to the hardware counterparts.   
   
**Virtual Load Balancers:**   
   
This load balancer is different from both the software and hardware load balancers as it is the combination of the program of a hardware load balancer working on a virtual machine.   
   
Through virtualization, this kind of load balancer imitates the software driven infrastructure. The program application of hardware equipment is executed on a virtual machine to get the traffic redirected accordingly. But such load balancers have similar challenges as of the physical on-premise balancers viz. lack of central management, lesser scalability and much limited automation.   
   
## Load Balancing Methods   
   
All kinds of Load Balancers receive the balancing requests, which are processed in accordance with a pre-configured algorithm.   
   
**Industry Standard Algorithms**   
   
The most common load balancing methodologies include:   
   
   
- Round Robin Algorithm:   
  It relies on a rotation system to sort the traffic when working with servers of equal value. The request is transferred to the first available server and then that server is placed at the bottom of the line.   
   
   
- Weighted Round Robin Algorithm:   
  This algorithm is deployed to balance loads of different servers with different characteristics.   
   
   
- Least Connections Algorithm:   
  In this algorithm, traffic is directed to the server having the least traffic. This helps maintain the optimized performance, especially at peak hours by maintaining a uniform load at all the servers.   
   
   
- Least Response Time Algorithm:   
  This algorithm, like the least connection one, directs traffic to the server with a lower number of active connections and also considers the server having the least response time as its top priority.   
   
   
- IP Hash Algorithm:   
  A fairly simple balancing technique assigns the client’s IP address to a fixed server for optimal performance.   
   
Via - [Load Balancer | Types of Load Balancers | Benefits of Load balancer](https://www.appviewx.com/education-center/load-balancer-and-types/)
   
   
   
Elastic Load Balancing supports the following types of load balancers: Application Load Balancers, Network Load Balancers, and Classic Load Balancers. Amazon ECS services can use these types of load balancer. Application Load Balancers are used to route HTTP/HTTPS (or Layer 7) traffic. Network Load Balancers and Classic Load Balancers are used to route [TCP](../devlog/TCP.md) (or Layer 4) traffic.   
   
**Classic Load Balancer**   
   
   
- Uses Round Robin traffic routing   
- Will be deprecated from Aug 2022   
   
**Application Load Balancer**   
   
   
- Path based routing - if you have path `/home` or `/mobile` serving different pages from different ASGs.   
- Multiple ASG balancing.   
   
**Network Load Balancer**   
   
   
- Streaming service(packet transmission)   
- Uses network layer (TCP protocol) (makes this LB faster)   
   
**Gateway Load Balancer**   
   
   
- GWLB Target groups support the Generic Networking Virtualization Encapsulation(**GENEVE**) on port: 6081.   
- Runs within one Availability Zone.
   
   
33. **Have you used sonarqube?**   
   
   
SonarQube® is an automatic code review tool to detect bugs, vulnerabilities, and code smells in your code. It can integrate with your existing workflow to enable continuous code inspection across your project branches and pull requests.   
   
   
- [SonarLint](https://www.sonarlint.org/) – SonarLint is a companion product that works in your editor giving immediate feedback so you can catch and fix issues before they get to the repository.   
- [Quality Gate](https://docs.sonarqube.org/latest/user-guide/quality-gates/) – The Quality Gate lets you know if your project is ready for production.   
- [Clean as You Code](https://docs.sonarqube.org/latest/user-guide/clean-as-you-code/) – Clean as You Code is an approach to code quality that eliminates a lot of the challenges that come with traditional approaches. As a developer, you focus on maintaining high standards and taking responsibility specifically in the New Code you're working on.   
- [Issues](https://docs.sonarqube.org/latest/user-guide/issues/) – SonarQube raises issues whenever a piece of your code breaks a coding rule, whether it's an error that will break your code (bug), a point in your code open to attack (vulnerability), or a maintainability issue (code smell).   
- [Security Hotspots](https://docs.sonarqube.org/latest/user-guide/security-hotspots/) – SonarQube highlights security-sensitive pieces of code that need to be reviewed. Upon review, you'll either find there is no threat or you need to apply a fix to secure the code.   
   
Via - [SonarQube Docs](https://docs.sonarqube.org/latest/)
   
   
34. **Best practices for Incident Management.**   
   
Applications expose metrics, metrics are collected using monitoring system, we have alert rules to trigger a phone call, Slack notification or email to the [on-call](../devlog/on-call.md) engineer.   
   
The organization should have a proper:   
   
   
- Monitoring system   
  - [aws.CloudWatch](../devlog/aws.CloudWatch.md)   
  - [prometheus](../devlog/prometheus.md)   
- Alerting system   
  - SNS   
  - AlertManager   
   
Postmortem: Understand what went wrong and how to mitigate in the future.   
   
35. **How to validate variables during terraform plan time, for example format of the variable?**   
   
In [terraform](../devlog/terraform.md) you can define a `validation` block and specify a condition for the variable.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656067537/wiki/heqtzp8ccvxdlfsaqsbx.png)   
   
Scenario: String may not contain a /.   
   
```json
variable "string_may_not_contain" {
  type = string
  default = "test"

  validation {
    error_message = "Value cannot contain a \"/\"."
    condition = !can(regex("/", var.string_may_not_contain))
  }
}
```
   
   
Example via - [Terraform: Variable validation with samples](https://dev.to/drewmullen/terraform-variable-validation-with-samples-1ank)   
   
36. **Explain/Differentiate `CMD` and `ENTRYPOINT` in Docker.**   
   
The CMD command​ specifies the instruction that is to be executed when a Docker container starts. This CMD command is not really necessary for the container to work, as the echo command can be called in a RUN statement as well. The main purpose of the CMD command is to launch the software required in a container.   
   
CMD commands are ignored by Daemon when there are parameters stated within the docker run command.   
   
CMD. Sets default parameters that can be overridden from the Docker Command Line Interface (CLI) when a container is running.   
   
You can pass input from CMD to ENTRYPOINT.   
   
```bash
# CMD
FROM ubuntu:latest
CMD["echo", "Hello World!"]
```
   
   
ENTRYPOINT   
   
It is a directive or instruction that is used to specify the executable which should run when a container is started from a Docker image. It has two forms, the first one is the ‘exec’ form and the second one is the ‘shell’ form. If there is no entrypoint or CMD specified in the Docker image, it starts and exits at the same time that means container stops automatically so, we must have to specify entrypoint or CMD so that when we will start the container it should execute or it'll stop.   
   
We can override the ENTRYPOINT instruction while starting the container using the ‘–entrypoint’ flag. Also if we have multiple ENTRYPOINT instructions mentioned in Dockerfile then the last ENTRYPOINT will have an effect.   
   
You can run shell scripts using ENTRYPOINT and pass it's output to CMD   
   
```bash
FROM ubuntu
RUN apt-get update && apt-get install -y nginx
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```
   
   
Both run during docker container runtime. Using either one of them is best practice but they can be combined too.   
   
37. **Troubleshoot EC2 instance in an ASG that are getting terminated.**   
   
If EC2 quota and pricing is not the issue:   
   
EC2 instances get terminated if they're unhealthy.EC2 instances can become unhealthy if:   
   
   
- Disk space being full.   
- High CPU usage.   
- No memory left.   
   
To debug   
   
   
- Run [top](../devlog/top.md) command to see CPU utilization, check what process/application is using up the resources. Take this up with your developer.   
- Disk space EBS volume could be full and and OS might be running out of all disk space.   
- Run [free](../devlog/free.md) command to check if any swap memory is left or not, you might want to increase it.   
   
See: [create and use swap file on linux](../devlog/create%20and%20use%20swap%20file%20on%20linux.md)   
   
38. **How to control of deployment of pods on nodes that are going to be used explicitly for those pods?**   
   
   
- We can achieve this by using **Taints and Tolerance** in K8's.   
- A taint when attached to a node, will ripple pods from getting provisioned or getting accepted.   
- We can add a taint to a pod `kubectl taint nodes nodex key=value:Effect`   
- Taints are properties of nodes that push pods away if they don't tolerate this taint.   
- Like labels, one or more Taints can be applied to a node. The node must not accept any pod that doesn't tolerate all of these taints.   
   
40. **You've 2 different servers with different ports and usernames, how do you use ansible runbook/playbook on both of the servers?**   
   
In our `ansible.conf` we can define different `ansible_user` and `ansible_port` in the hostfile.   
   
```conf
[webservers]
10.4.20.90 ansible_port=4000 ansible_user=roger
39.12.3.23 ansible_port=8001 ansible_user=liam
```
   
   
41. **What is Terraform state lock?**   
   
If supported by your backend, [Terraform](../devlog/terraform.md) will lock your state for all operations that could write state. This prevents others from acquiring the lock and potentially corrupting your state. State locking happens automatically on all operations that could write state.   
   
You won't see any logs of when/as this happens. If state locking fails, Terraform will continue.   
   
You can disable state locking for most commands with the `-lock` flag but it is not recommended. If acquiring the lock is taking longer than expected, Terraform will output a status message. If Terraform doesn't output a message, state locking is still occurring if your backend supports it.   
   
42. **How do you setup slack notifications on Jekins?**   
   
You can leverage Jenkins plugins, you can use the Jenkins - Slack plugin and use Slack webhook URL.   
Whenever a pipeline job fails:   
`slackSend color: "failure", message: "Pipeline failed, critical."   
   
43. **How do you see your trajectory as a DevOps Engineer?**   
   
There is always something to learn. You could mention some of the tools/technologies that you want to learn - some you want to better understand. Show them that you are someone who is looking to constantly improve himself/herself(themselves).   
   
You'd want to collaborate with your senior engineers to learn from them directly. Maybe you want to take up more responsibility in the organization etc.   
   
44. **How to ignore a certain part of our ansible playbook that might fail and cause our playbook to exit?**   
   
We can achieve this using `ignore_errors` sub arguments.   
   
```yaml
- name: Do not count this as a failure
  ansible.builtin.command: /bin/false
    ignore_errors: yes
```
   
   
45. **When making a change to existing code what is a `git` best practice?**   
   
Git clone the repo, checkout the respective branch. Make your change and commit your changes. To understand the motivation behind the change and the history, you can use `git blame`.   
   
The git blame command is used to examine the contents of a file line by line and see when each line was last modified and who the author of the modifications was. Basically gives you the history and the author of the file.   
   
46. **At a high level, create an shell script to automatically push certain logs to S3 at a particular time.**   
   
This is a Whiteboard design question.   
   
   
- Firstly, we'd make sure what we're using, IAM role or access keys.   
   
```bash
#!/bin/bash

# assign path-to-logs to a variable

# use aws CLI commands to copy files to S3

# aws s3 cp <path-to-logs> <s3-bucket>

# use cron job to execute the script at a particular time
```
   
   
47. **What is a package in Python?**   
   
The module is a simple Python file that contains collections of functions and global variables and with having a .py extension file. It is an executable file.To organize modules we have **Packages** in Python.   
   
Modules can have other modules inside them.   
   
Package(1) -> Modules(x) -> Fns(x)   
   
Example module:   
   
```py
#the os module provides an operating system interface from Python
import os
#prints the name of the operating system
print(os.name)
#prints the absolute path for the module
print(os.getcwd())
```
   
   
48. **What are your day to day responsibilities as a DevOps engineer?**   
   
Paint a brief picture of what your day to day work looks like.   
   
   
- A DevOps engineer works in collaboration other engineers(devs, testers, SRE, sales).   
- 9:00 AM -> 10:00 AM check Slack, update [Jira](/not_created.md) with your tasks.   
- 10:00 AM -> 10:30 AM daily standup, share progress with your team on the work you've done previous day and what you'll do today.   
- 10:30 AM -> 1:00 PM work on your Jira ticket.   
- 1:00 PM -> 2:00 PM lunch.   
- 2:00 PM -> 4:00 PM pair program with other engineers or meetings, design discussions.   
- 4:00 PM -> 5:00 PM learning new stuff that can benefit the org, share knowledge with other team members.   
   
## Credits   
   
   
- [50 DevOps Interview Questions & Answers - 2022 | Udemy](https://www.udemy.com/course/50-devops-interview-questions-answers/)