---
created: 1661426677502
desc: ''
id: ezzlniu0fuqwupwrmew0td8
title: Create EKS cluster with AWS Management Console
updated: 1662482548398
---
   
Related::  [kubernetes](../devlog/kubernetes.md)   
   
   
---   
   
**Overview/steps**   
   
1. Create [aws.IAM](../devlog/aws.IAM.md) Role for EKS service   
   
2. Create a VPC   
   
This is where our worker nodes will run.   
   
3. Create EKS Cluster (Control Plane)   
   
These will be a set of master nodes that are managed by AWS.   
   
4. Connect to the cluster using `kubectl`   
   
To connect to this cluster from our local machine.   
   
5. Create IAM Role for EC2 service   
   
To give EC2 service the permissions to call AWS API and configure, create stuff in our AWS account. Essentially to create worker nodes for the EKS cluster.   
   
6. Create Node Group, attach it to EKS cluster   
   
Node Group is a group of EC2 instances that are gonna run as worker nodes in the EKS cluster(master nodes).   
   
7. Configure Auto Scaling   
   
This is created so that the number of EC2 instances are intelligently scaled up/down to match resource requirement.   
   
8. Deploy an application to EKS cluster   
   
   
---   
   
## 1. Create IAM Role   
   
We’re creating a new Role so the EKS service(attached) has the permissions/policies to create things in AWS account. To allow AWS to create and manage components on our behalf/on our account.   
   
You can give Roles from your account to another AWS account.   
   
IAM components are not scoped to a region but are Global.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656319924/wiki/y1xcw9jn85hmsnyy6ckw.png)   
   
Choose “EKS - Cluster” as use case, a policy will automatically be selected.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656319963/wiki/uier1mhwdqxdkzrkugc3.png)   
   
Policy is automatically selected.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656320002/wiki/vrof1roeuovsnm9xbzef.png)   
   
Trusted entities basically informs what services you’ve attached the role to and Policies inform what exactly the service(Role) can do.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1656320059/wiki/otyhdlqylbuzgrry5jj8.png)   
   
## 2. Create a [aws.VPC](../devlog/aws.VPC.md)   
   
Why are we creating a new VPC even though we’ve a default VPC.   
   
We are creating a new VPC because EKS cluster needs specific networking configuration for it to work properly. It needs [kubernetes](../devlog/kubernetes.md) and AWS specific networking rules, worker node specific firewall configuration. It is necessary for master nodes to communicate with them and manage them.   
   
Default VPC is not optimized for EKS cluster(not the best practice either).   
   
Examples of rules:   
   
Firewall rules (of subnets) that are configured by Network ACLs, inside the subnet you’ve EC2 instances. EC2 instances have their own firewall rules that are defined by security groups.   
   
It is a best practice to create/configure subnets in worker node VPC, i.e creating **public** subnets and **private** subnets(creating external load balancer).   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662394123/wiki/zipqz1eanat00scyfvpx.png)   
   
Through IAM Role you give Kubernetes permissions to change VPC configuration(Nodeport service; to open ports on our behalf in our VPC etc).   
   
**How do we create this VPC with all its configurations?**   
   
You can use templates provided by AWS instead of creating the VPC by ourselves.   
   
Using [aws.CloudFormation](../devlog/aws.CloudFormation.md) template for creating VPC. You’ll create the entire stack(whatever components your VPC needs) from the CF template.   
   
Docs - [Creating a VPC for your Amazon EKS cluster - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/creating-a-vpc.html)   
   
Create a stack and use a template given in the docs, if you need to make any adjustments to the template, download and make the changes and upload the template when creating a stack.   
   
`https://s3.us-west-2.amazonaws.com/amazon-eks/cloudformation/2020-10-29/amazon-eks-vpc-private-subnets.yaml`   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662396006/wiki/ji5b1qlg3xkblnpokc9v.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662396171/wiki/espltkwvbovhjzm8obar.png)   
   
Once created, you’ll need the information under “Outputs” tab for creating Control Plane.   
   
## Create EKS Cluster(Control Plane)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662397479/wiki/uxdggwfwap1hlkrmmqpf.png)   
   
You can enable “Secrets encryption” to encrypt all your Secrets conveniently without having to install additional software on your K8s cluster.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662397713/wiki/f0gwcw8fwm6ukkuivgxc.png)   
   
Select the EKS Worker Nodes Security group.   
   
**Cluster endpoint access**   
   
API Server is the entrypoint to the cluster.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662397846/wiki/eesupwpi2iz7apmhdcpk.png)   
   
If you want to access API Server externally, from a dashboard, `kuebctl`, from outside the VPCs, enable Public endpoint.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662398028/wiki/vfcavb4x8qdinddqekgd.png)   
   
We’re going with Public and private as that is ideal and optimal. We’ll need to install `kubectl` on one of our Worker Nodes.   
   
## Connect to the Cluster   
   
`aws configure list` check if you’ve configured the same region as the region in which you created the cluster.   
   
`aws eks update-kubeconfig --name <cluster-name>` will create a `kubeconfig` file locally inside `~/.kube/config`.   
   
`kubectl get nodes` will return nothing as no Worker Nodes have been configured as of yet.   
   
`kubectl cluster-info`   
   
## Worker Nodes   
   
You can either use EC2 instances or run the Pods using [aws.Fargate](../devlog/aws.fargate.md).   
   
Node Groups are EC2 instances that you manage yourself while Fargate gives you managed Worker Nodes.   
   
We’ll go with Node Groups.   
   
## Create EC2 IAM Role for our Node Group   
   
   
- Worker Nodes run worker processess.   
- `kubelet` is the main process - scheduling, managing Pods and communicate with other AWS services.   
- kubelet on Worker Node(EC2 instances) needs permissions.   
- Node Group needs a Role that has policies attached to it to make those API calls to other AWS services.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662399835/wiki/vkl8ibslws6h8byx6k3f.png)   
   
We need three policies:   
   
   
- `AmazonEKSWorkerNodePolicy`   
- `AmazonEC2ContainerRegistryReadOnly`   
- `AmazonEKS_CNI_Policy` - Container Network Interface   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662400104/wiki/hrmfg3mihvfimahzvnoh.png)   
   
## Add Node Group to EKS Cluster   
   
On EKS Add Node Group   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662400176/wiki/jtkraffljkzup7ufnlaw.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662400232/wiki/zvzbb2o6itknlsickc8o.png)   
   
Select on which Image the instances will be based on.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662400305/wiki/wgzl9fl8xocoxbuwtiw6.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662400341/wiki/mkf1f3vsgh8oqvvhk8o2.png)   
   
Once created, we wanna [ssh](../devlog/ssh.md) into them, so add a SSH key pair under “Specify networking” and set “Allow remote access from” to “All”.   
   
Once up and running, we need to make sure that the worker process are also installed.   
   
## Configure Autos Scaling   
   
An Auto Scaling group was created and attached when the cluster was created. It doesn't automatically-autoscale our resources. We need configure the K8s Autoscaler that will use the AWS's Auto Scaling group and together scale up or scale down the EC2 instances.   
   
Lets say we've a 10 instance cluster and if the K8s Autoscaler detects that the instances are being underutilized, it'll take the Pod from two instances and distributed them on the rest of them and stop the other instances.   
   
If the instances are on full capacity and there is a need for more, K8s Autoscaler will work in tandem with AWS Auto Scaling group and depending on "max" and "min" size to schedule a new Pod.   
   
We need three things for this to work:   
   
1. Auto Scaling group (already created)   
2. Create custom policy and attach a Node Group IAM Role.   
   
Custom policy that has:   
   
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "autoscaling:DescribeAutoScalingGroups",
        "autoscaling:DescribeAutoScalingInstances",
        "autoscaling:DescribeLaunchConfigurations",
        "autoscaling:DescribeTags",
        "autoscaling:SetDesiredCapacity",
        "autoscaling:TerminateInstanceInAutoScalingGroup",
        "ec2:DescribeLaunchTemplateVersions"
      ],
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662482617/wiki/kdel1sdey6zkaahaqnuv.png)   
   
Create the Policy (Managed Policy) and attach it to the existing Node Group IAM Role.   
   
3. Tags on Auto Scaling group.   
   
Tags are used by different services to read information from each other. There might be some existing tags on this Auto Scaling group.   
   
We want to K8s cluster Autoscaler to be able to interact with AWS Auto Scaling group. These tags should be created automatically.   
   
key - value pairs   
   
`k8s.io/cluster-autoscaler/<cluster-name>` - owned   
`k8s.io/cluster-autoscaler/enabled` - true   
   
4.  We need to deploy the K8s Autoscaler component in the cluster.   
   
`kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml`   
   
Or you can download the file and make the changes before applying it.   
   
Once applied, we need to make sure the selector tags are named correctly.   
   
`kubectl get deployment -n kube-system cluster-autoscaler`   
`kubectl edit deployment -n kube-system cluster-autoscaler`   
   
Add this line under  `annotations`:   
   
`cluster-autoscaler.kubernetes.io/safe-to-evict="false"`   
   
Change `<YOUR CLUSTER NAME>` placeholder to the actual cluster name under `spec -> containers`   
   
Other options:   
   
`- --balance-similar-node-groups` and  `- --skip-nodes-with-system-pods=false`   
   
Also make sure that the `cluster-autoscaler:v_._._` Image version is same as the Kubernetes running on the cluster.   
   
Save and exit.   
   
`kubectl get pods -n kube-system`   
   
`kubectl get pod cluster-autoscaler-name -n kube-system -o wide`   
   
`kubectl logs -n kube-system <cluster-autoscaler-name> > as-logs.txt`   
   
Autoscaler is setup, whenever you add more Pods, it’ll scale up and scales down when not need. It saves cost. But the trade off is that provisioning a new EC2 instance takes time.   
   
## Deploy application into cluster   
   
We’re going to deploy an Ngnix Deployment.   
   
```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 1
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```
   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662592492/wiki/onkc1ywsk4vep2ot2syz.png)   
   
AWS LoadBalancer needs at least 1 EC2 instances in at least 2 AZs.   
   
Find the finished code: [eks-cluster-autoscaler · zubayrrr / bootcamp-kubernetes](https://gitlab.com/zubayrrr/bootcamp-kubernetes/-/tree/master/eks-cluster-autoscaler)