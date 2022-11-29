---
created: 1662813879982
desc: ''
id: ko38y5s6xjrjg7ymyfli1jf
title: OCI
updated: 1662814132697
---
   
Related::  [docker](../devlog/docker.md), [containers & images](../devlog/containers%20%26%20images.md)   
   
   
---   
   
The OCI format is a specification for container images based on the Docker Image Manifest Version 2, Schema 2 format. Container Registry supports pushing and pulling OCI images.   
   
Following Docker's release, a large community emerged around the idea of using containers as the standard unit of software delivery. As companies started using containers to package and deploy their software more and more, Docker's container runtime did not meet all technical and business needs that engineering teams could have. In response to this, the community started developing new runtimes with different implementations and capabilities. Simultaneously, new tools for building container images aimed to improve on Docker's speed or ease of use. To make sure that all container runtimes could run images produced by any build tool, the community started the Open Container Initiative — or OCI — to define industry standards around container image formats and runtimes.   
   
— via [Docker and OCI: what is a container and how do they work?](https://www.padok.fr/en/blog/container-docker-oci#oci)