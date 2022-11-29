---
created: 1653408009159
desc: ''
id: 4f08m6qrqyvpf6hfk1898vt
title: Containers & Images
updated: 1662813920150
---
   
## What is a Container?   
   
?   
A container is a way to package an application with all the necessary dependencies and configuration. It is a portable artifact that can be easily shared and moved around. [docker](../devlog/docker.md), [containerd](/not_created.md), [cri-o](/not_created.md) are some examples of container technologies. Containers have existed before Docker.   
   
Containerized applications are applications that run in isolated runtime environments called containers. Containers encapsulate an application with all its dependencies, including system libraries, binaries, and configuration files.   
   
An application packaged together with its dependencies that runs on top of an OS in an isolated instance and uses the kernel from the host OS.   
   
> Containers are often referred to as “lightweight,” meaning they share the machine’s operating system kernel and do not require the overhead of associating an operating system within each application. Containers are inherently smaller in capacity than a [VM](../devlog/vm.md) and require less start-up time, allowing far more containers to run on the same compute capacity as a single VM. This drives higher server efficiencies and, in turn, reduces server and licensing costs.   
   
Put simply, containerization allows applications to be “written once and run anywhere.” This portability is important in terms of the development process and vendor compatibility. It also offers other notable benefits, like fault isolation, ease of management and security, to name a few. — via [Containerization Explained - India | IBM](https://www.ibm.com/in-en/cloud/learn/containerization)   
   
## Where do containers live?   
   
?   
They're stored in a container repository. Public or Private repositories. DockerHub is a public repository. You can use [nexus](../devlog/nexus.md) as a private repository.   
   
## Container VS Image   
   
?   
Technically, a container is made up of images, layers of images stacked on top of each other.   
At the base of the image, you'd usually have a Linux as the Base Image. It could be `alpine` or any other distro of Linux, it is important for these Base Images to be small to make sure container stays small in size.   
   
The application image is usually the top layer.   
   
   
- An image is a standalone, isolated, lightweight and executable package that contains   
  all the required components (code, runtime, system tools, libraries, settings, etc)   
  necessary to run an application. An image is the actual, moveable artifact.   
   
- The container is the runtime instance of the image. From the same image, you can launch more containers.   
  Images for many applications can be found on [https://hub.docker.com](https://hub.docker.com)   
   
- An image "becomes" a container when we actually start an image. It creates a container environment.   
   
## Containers VS VM   
   
?   
![](https://res.cloudinary.com/zubayr/image/upload/v1657820046/wiki/rbvrr2wexsbxl8yuddgp.png)   
   
Docker virtualizes applications layer. Cannot run Linux based images on Windows kernel(which can be mitigated by install Docker Toolbox to abstract away the kernel layer).   
   
VM virtualizes both applications and OS kernel layer(entire OS). Can run on any host OS.   
   
## Docker Images   
   
**Docker image** is an immutable (unchangeable) file that contains the source code, libraries, dependencies, tools, and other files needed for an application to run.   
   
Due to their **read-only** quality, these images are sometimes referred to as snapshots. They represent an application and its virtual environment at a specific point in time. This consistency is one of the great features of Docker. It allows developers to test and experiment software in stable, uniform conditions.   
   
Since images are, in a way, just **templates**, you cannot start or run them. What you can do is use that template as a base to build a container. A container is, ultimately, just a running image. Once you create a container, it adds a writable layer on top of the immutable image, meaning you can now modify it.   
   
The image-base on which you create a container exists separately and cannot be altered. When you run a containerized environment, you essentially create a **read-write copy** of that filesystem (docker image) inside the container. This adds a **container layer** which allows modifications of the entire copy of the image.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657821563/wiki/pshjskltg9vpslfynuvj.png)   
   
You can create an unlimited number of Docker images from one **image base**. Each time you change the initial state of an image and save the existing state, you create a new template with an additional layer on top of it.   
   
Docker images can, therefore, consist of a **series of layers**, each differing but also originating from the previous one. Image layers represent read-only files to which a container layer is added once you use it to start up a virtual environment.   
   
## Docker Container   
   
A Docker container is a virtualized run-time environment where users can isolate applications from the underlying system. These containers are compact, portable units in which you can start up an application quickly and easily.   
   
A valuable feature is the standardization of the computing environment running inside the container. Not only does it ensure your application is working in identical circumstances, but it also simplifies sharing with other teammates.   
   
As containers are autonomous, they provide strong isolation, ensuring they do not interrupt other running containers, as well as the server that supports them. Docker claims that these units “provide the strongest isolation capabilities in the industry”. Therefore, you won’t have to worry about keeping your machine secure while developing an application.   
   
Unlike virtual machines (VMs) where virtualization happens at the hardware level, containers virtualize at the app layer. They can utilize one machine, share its kernel, and virtualize the operating system to run isolated processes. This makes containers extremely lightweight, allowing you to retain valuable resources.   
   
![Containers and Virtual Machines Together](/assets/images/containers%20and%20vms.png)   
Source ~ [What is a Container? - Docker](https://www.docker.com/resources/what-container/)   
   
## Resources   
   
   
- [Docker Image VS Container: What is the difference?](https://phoenixnap.com/kb/docker-image-vs-container)