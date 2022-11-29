---
created: 1662238506752
desc: ''
id: rhdenjkpa6hsuaidh1zc5du
title: Authorization with RBAC
updated: 1662243251515
---
   
**Overview**   
   
   
- Authentication and Authorization in K8s   
- How to configure users, groups and their permissions.   
- Authorization with **R**ole **B**ased **C**ontrol (RBAC).   
- Which K8s resources to use define permissions in the cluster.   
   
## Why do you need Authorization?   
   
How do you manage permissions in a cluster? Admins need elevated access whereas Users have limited access.   
   
As a security best practice we should follow the Principle of least privilege.   
   
**RBAC** = Role Based Access Control   
   
## Role   
   
When you've multiple namespaces in your cluster where each developer team deploys applications in different namespace. How do you make sure that each team only has access to their namespace and the resources that belong to that namespace.   
   
   
- With Role component you can define namespaced permissions.   
- Role is bound to a specific namespace.   
- It defines what resources(Pod, Deployment, Service etc) you've access to in that namespace.   
- and what actions(list, get, update, delete etc) you can perform with/on those resources.   
   
For different developer teams, you can create a specific role and define permissions for it.   
   
Role doesn't define WHO gets these permissions. You need to attach Role definition to a person or team.   
   
## RoleBinding   
   
With RoleBinding you can basically link(bind) a Role to a User or a User Group.   
   
## CluserRole   
   
For Admins that usually do cluster-wide operations, Role cannot be used in this scenario as it is limited to a namespace and Admins need cluster-wide access. Enter ClusterRole.   
   
It defines what resources has what permissions - cluster-wide.   
   
## ClusterRoleBinding   
   
After creating a ClusterRole, you can bind the ClusterRole to a Group of Admins(Users) using ClusterRoleBinding.   
   
## Users and Groups   
   
**How do we create Users and Groups**   
   
   
- K8s doesn't manage Users natively.   
- Admins can choose different authentication strategies.   
- No K8s Objects exist for representing user accounts.   
- It relies on external sources for creating and managing Users, Groups.   
- This external source can be a static file with user details such as username and token.   
- It can also be certificates signed by K8s or by a 3rd party identity service like [LDAP](../devlog/ldap.md)   
   
A K8s Admin configures one of this external sources in the cluster and the API Server(Control Plane component) handles all the authentication requests coming in. It uses one of the configured authentication methods(sources).   
   
`kube-apiserver --token-auth-file=/users.csv [other-options]`   
   
```csv
# users.csv
05c2b1e0303d04a85521c8eb3a4a1019m, user_1, u1001
4e02489b29e13918506ffffe3cd5ce1e, user_2, u1002
c1b200529b999126865486bea54b77af, user_3, u1003
```
   
   
```csv
# users-group.csv
05c2b1e0303d04a85521c8eb3a4a1019m, user_1, u1001, group1
4e02489b29e13918506ffffe3cd5ce1e, user_2, u1002, group2
c1b200529b999126865486bea54b77af, user_3, u1003, group3
```
   
   
As for certificates, you'll have to manually create certs for different users or you(an Admin) can configure LDAP as authentication source for the API Server.   
   
## Service Accounts   
   
So far, we've seen how to configure permissions for Human Users. Let's see how we can configure permissions for Application Users.   
   
These applications can be inside the cluster or outside the cluster.   
   
An example for an internal application would be [prometheus](../devlog/prometheus.md). Microservices that might need access within their namespace. These applications could be communicating with other applications internally, or gathering information like a monitoring application.   
   
An example for external application could be a CI/CD Server deploying apps inside/to the cluster. An IaC tool like Terraform that configures the cluster itself.   
   
We want to make sure that applications only have permissions that they need to do their job properly.   
   
To define permissions for Application Users in K8s we've a K8s component that represents an Application User.   
   
**ServiceAccount**   
   
You create a ServiceAccount component for Application User with:   
   
`kubectl create serivceaccount sa1`   
   
You can then link(bind) this SA to a Role or ClusterRole with RoleBinding and ClusterRoleBinding respectively.   
   
## Example Config Files   
   
**Role**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
  - apiGroups: [""] # "" indicates the core API group
    resources: ["pods"]
    verbs: ["get", "watch", "list"]
```
   
   
**RoleBinding**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
# This role binding allows "jane" to read pods in the "default" namespace.
# You need to already have a Role named "pod-reader" in that namespace.
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
  # You can specify more than one "subject"
  - kind: User
    name: jane # "name" is case sensitive
    apiGroup: rbac.authorization.k8s.io
roleRef:
  # "roleRef" specifies the binding to a Role / ClusterRole
  kind: Role #this must be Role or ClusterRole
  name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
```
   
   
**ClusterRole**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: monitoring-endpoints
  labels:
    rbac.example.com/aggregate-to-monitoring: "true"
# When you create the "monitoring-endpoints" ClusterRole,
# the rules below will be added to the "monitoring" ClusterRole.
rules:
  - apiGroups: [""]
    resources: ["services", "endpoints", "pods"]
    verbs: ["get", "list", "watch"]
```
   
   
**CluserRoleBinding**   
   
```yaml
apiVersion: rbac.authorization.k8s.io/v1
# This cluster role binding allows anyone in the "manager" group to read secrets in any namespace.
kind: ClusterRoleBinding
metadata:
  name: read-secrets-global
subjects:
  - kind: Group
    name: manager # Name is case sensitive
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```
   
   
## Creating & Reviewing RBAC Resources   
   
You create these RBAC resources just like any other K8s component with `kubectl apply -f file.yaml` and view them using `kubectl get roles` or `kubectl describe role <role-name>`.   
   
## Checking API Access   
   
`kubectl` provides a `auth can-i` subcommand to quicky check if current user can perform a certain action.   
   
`kubectl auth can-i create deployments --namespace dev`   
   
Admins can also check permissions of other users.   
   
## Layers of Security   
   
We've two different levels of security in K8s.   
   
1. When receiving an incoming request, it'll check if the User has the permissions to even connect to the cluster.   
2. If authenticated, it'll check the user's authorization using RBAC after which it'll proceed with the User's request.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1662243285/wiki/wb6baytfe6kb2ebz88rz.png)