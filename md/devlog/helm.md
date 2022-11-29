---
created: 1655905182867
desc: ''
id: 5uu4351w46y16xtyufz0fy4
title: Helm
updated: 1655905656371
---
   
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