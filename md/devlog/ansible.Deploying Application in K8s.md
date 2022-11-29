---
created: 1661426936153
desc: ''
id: lx4nhbxh13394bk7srdb2y3
title: Deploying Application in K8s
updated: 1661435630275
---
   
Topics::  [kubernetes](../devlog/kubernetes.md)   
   
   
---   
   
Steps:   
   
   
- Create [kubernetes](/not_created.md) cluster on [terraform.Automate Provisioning EKS cluster](/not_created.md)   
- Configure Ansible to connect to that [aws.EKS](../devlog/aws.EKS.md) cluster.   
- Deploy a simple deployment and service components inside cluster.   
   
**Create EKS cluster**   
   
Use the Terraform code from [feature/eks](https://gitlab.com/zubayrrr/terraform-learn/-/tree/feature/eks).   
   
**Create a Namespace in EKS cluster**   
   
Using a community module named `k8s` to avoid having to use `kubectl` commands yourself. You could write the whole [kubernetes](../devlog/kubernetes.md) configuration files directly in your Ansible play.   
   
_When using the module, make sure the requirements are fulfilled for the local machine._   
   
Example: `python3 -c "import openshift"` and `python3 -c "import yaml"`   
   
The packages need to be installed for the USER not globally(system wide):   
   
   
- `pip3 install openshift --user`   
- `pip3 install PyYAML --user`   
   
```yaml
---
- name: Deploy app in new namespace
  hosts: localhost # we're connecting to a K8s cluster even though we're running Playbook locally.
  # We don't need K8s endpoint or worker node host
  tasks:
    - name: Create a k8s namespace
      community.kubernetes.k8s:
        name: my-app
        api_version: v1
        kind: Namespace
        state: present
        kubeconfig: ~/path/to/kubeconfig_myapp-eks-cluster
        # to provide context information, certificate, address
        # if not mentioned, it'll look for the default one from ~/.kube/config.json
    - name: Deploy nginx app
      community.kubernetes.k8s:
        src: ~/path/to/nginx-config.yaml
        state: present
        namespace: my-app
```
   
   
Make sure `inventory = hosts` in the `ansible.cfg` file.   
   
Run the playbook.   
   
Check if namespace was created by first `export KUBECONFIG=~/path/to/kubeconfig` - should be same as defined in the play.   
   
`kubectl get ns` to list namespaces.   
   
**Deploy an Ngnix app**   
   
**Environment variable for kubeconfig**   
   
`export K8S_AUTH_KUBECONFIG=~/path/to/kubeconfig`   
   
```yaml
---
- name: Deploy app in new namespace
  hosts: localhost
  tasks:
    - name: Create a k8s namespace
      community.kubernetes.k8s:
        name: my-app
        api_version: v1
        kind: Namespace
        state: present
    - name: Deploy nginx app
      community.kubernetes.k8s:
        src: ~/path/to/nginx-config.yaml # deployment config
        state: present
        namespace: my-app # so you don't have to hard code the value inside kubeconfig
```
   
   
To verify:   
   
   
- `kubectl get pod -n my-app`   
- `kubectl get svc -n my-app`