---
created: 1653554675466
desc: ''
id: wf37vjntme0oklsx52ycrn4
title: Docker
updated: 1661336470158
---
   
Topics::  [devops](../topics/devops.md)   
Related::  [cgroups](../devlog/cgroups.md)   
   
   
---   
   
   
- Docker is a platform for developers and sysadmins used to develop, deploy and run   
  containerized applications.   
   
- A container is a running process that encapsulates everything an application needs to   
  run (and only those things).   
   
- Docker makes it really easy to install and run software without worrying about setup or   
  dependencies.   
   
- An image is a standalone, isolated, lightweight and executable package that contains   
  all the required components (code, runtime, system tools, libraries, settings, etc)   
  necessary to run an application. An image is the actual, moveable artifact.   
   
- The container is the runtime instance of the image. From the same image, you can launch more containers.   
  Images for many applications can be found on [https://hub.docker.com](https://hub.docker.com)   
   
- An image "becomes" a container when we actually start an image. It creates a container environment.   
   
## Docker Architecture & Components   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657820835/wiki/gzkdopsbfapaqzzq2r5n.png)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657820890/wiki/yzkdx8fuqd6gyrmd9lug.png)   
   
## Install Docker   
   
[Docker Docs](https://docs.docker.com/engine/install/)   
   
## Docker Image vs Container   
   
Images can exist without containers, whereas a container needs to run an image to exist. Therefore, containers are dependent on images and use them to construct a run-time environment and run an application.   
   
The two concepts exist as essential components (or rather phases) in the process of running a Docker container. Having a running container is the final “phase” of that process, indicating it is dependent on previous steps and components. That is why docker images essentially govern and shape containers.   
   
Container is the running environment for(of) an image. Container has application image, a port binded to it(makes it possible for it to talk to the application running inside it), Containers has virtual FS.   
   
See also: [containers & images](../devlog/containers%20%26%20images.md)   
   
## Docker cli   
   
   
- Run `docker info`, `docker --version` or `docker version` to check it's version and if the client is able to communicate with the server.   
- The new way of running docker commands is:   
   
   
  - First comes the `docker` command followed by a `management command` and then a `sub command` with options   
  - Run `docker help` to find all commands, sub commands   
   
   
- To test docker run the `hello-world` container   
  - `docker container run hello-world`   
- To search for an image on docker hub   
  - `docker search mongo`   
- To pull an image   
  - `docker image pull redis` is same as `docker image pull redis:latest`   
  - `docker image pull redis:5.0.10` `:tag`(optional)   
- To list all images   
  - `docker images` or `docker image ls`   
- To run an container from(of) an image   
  - `docker container run redis`   
- To pull an image and run container   
  - `docker container run -P httpd` (`-P` to publish all exposed ports to random ports)   
- The above command executed in two steps   
   
   
  - `docker container create -p 80:80 httpd`   
  - `docker container start CONTAINER_ID`   
   
   
- To get a shell inside docker   
  - `docker container run -it centos`(if you run it without passing any commands it'll simply exit, `-it` is required for shell access of the container)   
- Get terminal of the container   
   
   
  - `docker exec -it CONTAINER_ID /bin/bash`   
  - `docker exec -it CONTAINER_ID /bin/sh`   
   
   
- To give your container a custom name(default is random)   
   
   
  - `docker run -d -p 6001:6379 --name redis-olderv redis:4.0`   
   
   
- To list all running docker containers   
  - `docker ps` or `docker container ls`   
  - `ps` stands for process status   
- To list all docker containers   
  - `docker ps -a` or `docker container ls -a`   
- To filter by status run   
  - `docker container ls -a -f status=exited`   
- To list only container IDs   
   
   
  - `docker container ls -a -f status=exited -q` -q comes from quiet   
   
   
- To remove image and the container   
  - First stop and then remove the container   
  - `docker container stop CONTAINER_ID`   
  - You don't have to write the entire container ID, the first few digits as long as they're unique   
  - `docker container rm CONTAINER_ID` to remove the container   
- To remove a running container `docker container rm -f CONTAINER_ID`   
- To remove using filter use command substitution   
  - `docker container rm $(docker container ls -a -f status=exited -q)`   
- To remove an image   
   
   
  - `docker rmi` or `docker image rm IMAGE_NAME` (`-f` to forcefully remove a still running container's image)   
  - If you try to remove an image that is stopped or running, it'll throw an error, you'll need to remove the container before removing it's image.   
   
   
- To view logs of a container(useful for debugging):   
  - `docker container logs CONTAINER_ID`   
  - `docker container logs -f CONTAINER_NAME` (`-f` to view them in realtime)   
- To view all the process running inside a container:   
  - `docker container top CONTAINER_NAME`   
  - `docker container top CONTAINER_ID`   
  - You can look for the same processes running on the host machine(even the process IDs are same)   
- To display realtime info about running containers:   
  - `docker container stats`   
  - `docker container stats CONTAINER_NAME` (for info about specific container)   
- To view more info about containers   
   
   
  - `docker container inspect CONTAINER_NAME/ID`   
  - Filter using [grep](../devlog/grep.md)   
  - `docker container inspect CONTAINER_NAME/ID | grep -i ipaddress`   
   
   
- To commit changes to a container's image:   
  - `docker commit -m "commit message" -a "author name" CONTAINER_ID repo_name/image_name:latest`   
  - You can now use the newly created image with your committed changes.   
- To add a custom tag to an existing image(**doesn't** create a new image, will point towards the image with the same ID):   
  - `docker image tag image_name repo_name/image_name:new_tag`   
  - `docker image tag repo_name/image_name:old_tag repo_name/image_name:new_tag`   
- To push the image to docker hub:   
  - The repo name used must match the username on docker hub   
  - `docker login`   
  - `docker image push repo_name/image_name:tag`   
- To rename an image (makes a copy, points to the same image ID)   
  - `docker tag my-app:1.0 new-my-app:1.1.0`   
   
## Docker Hub   
   
Image name follows the convention of `repository/image_name:tag` but official images don't follow this structure as they're at the root level.   
   
Image ID is used to identify docker images, a single image can have multiple tags pointing to the same image.   
Docker Image ID is a digest which contains the [sha256](/not_created.md) hash of the image.   
   
## Dangling Images   
   
   
- Docker images consist of multiple layers. Dangling images are layers that have no relationship to any tagged images.   
- To delete dangling images, stopped containers and networks not used by at least one container run:   
  - `docker system prune`   
- `docker system prune -a` to remove unused images as well   
- An image consists of multiple layers. They're read-only and each has an ID.   
- A layer is saved only once and can be used by more than one image. (This saves disk space and time when pulling images.)   
- They layers are stacked on top of each other.   
- When you run a container from an image, a new writeable layer is added on top of the image layers.   
- This writeable layer is often called "Container Layer" and allows you to make changes to the container since the lower layers on the image are read-only.   
- When we remove a container, we're in fact only removing the writeable layer.   
- To write data to the writeable layer of the container, docker uses "Storage Drivers"   
- `overlay2` is the default and recommended driver.   
- To view the layers of an image:   
  - `docker image inspect image_name`   
  - On disk, the layers are located at `/var/lib/docker/overlay2`   
- There are two different values under "SIZE" when `docker container ls` is run   
  - The first value represents the amount of data used for the writeable layer of each container.   
  - The "Virtual" size represents the amount of data for the read-only image layers plus the container's writeable layer's size   
- Multiple containers may share some or all read-only image data, and two containers started from same image share 100% of the read-only data.   
   
## Image ID   
   
A Docker image's ID is a digest, which contains an SHA256 hash of the image's JSON configuration object.   
   
## Container   
   
   
- A container when it starts executes a default command, as long as the container's default command is running it'll stay up. Once the command finishes execution, the container will also exit.   
- To get access to a shell of a container use `-it` flags, `i` for interactive and `t` for [tty](../devlog/tty.md).   
- To escape from a running container without stopping the container use `CTRL + P + Q`   
- To execute commands on a running container:   
  - `docker container exec -it CONTAINER_ID bash` or   
  - `docker container exec CONTAINER_ID cat /etc/shadow`   
   
## Persistent Data / Docker Volumes   
   
Containers have Virtual FS inside them.   
   
By default, all files created inside a container are stored on the writeable container layer. The data doesn't persist when the container no longer exists(stops, removed, restarted) and it can be difficult to get the data out of the container if another process needs it.   
   
Docker provides two options for the container to store data in the host machine, to make data persist.   
   
1. Volumes   
2. Bind Mounts   
   
Volumes are preferred over Bind Mounts. While **Bind Mounts** are dependent on the directory structure and the OS of the host machine. Volumes are completely managed by Docker. **A Volume is a persistent directory of a container. Its a mapping between a directory on the docker host and a directory on a container.** To create a volume you mount a physical folder from the host into the virtual file system of Docker. Data is written on the host dir.   
   
There are different ways of creating Docker Volumes:   
   
   
- We can create volume by defining it in the Dockerfile using the `VOLUME` instruction.   
- By using `-v` flag when starting(`docker run`) a container and mapping a host dir to a to a dir in the container. These are called **Host Volumes**   
- You don't specify which host dir should be mounted, its created by Docker itself inside `/var/lib/docker/volumes`. These are called **Anonymous Volumes**. For each container a folder is generated that gets mounted. Anonymous Volumes will have a hash as a name.   
- You can specify a name for an autogenerated volume by `docker run -v name:/var/lib/mysql/data`. There are called **Named Volumes**.   
- You can also create them when using `docker-compose` using the `volumes` definition under a declared container. You can also define a list of volumes you want that `docker-compose` file to create so you can reference the same volume on different containers.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657894394/wiki/cwwndvvg1gypnj1wx3p7.png)   
   
When you mount a volume, they can be named or anonymous. Anonymous volumes are not given an explicit name when they're first mounted into a container; docker gives them a random name that is guaranteed to be unique within a given docker host.   
   
   
- `docker volume create volumeName`   
- `docker volume ls` - to list all volumes   
- `docker volume inspect volumeName` - info about a volume, like where the data on the volume is physically located on the drive.   
- `docker volume rm volumeName`   
- `docker volume prune` (will remove all unused volumes)   
   
The directory on the host that is being used as the mount point can be found at `/var/lib/docker/volumes/`   
   
   
- Starting a container with a volume.   
   
`docker container run -d --name mywebapp -p 80:80 -v mysite:/usr/share/ngnix/html nginx`   
   
Your website's html is copied TO the container's `/usr/share/ngnix/html` (in the above example) for it to be served.   
   
## Docker Layers   
   
   
- Docker format gives assets unique identifiers called Docker Layers   
- Docker Layers == Assets   
- Assets can be **reused** for different components   
  - E.g. if two Docker Images use same layers, you’d have 2 components that share the layer as an asset.   
- A Docker Layer can be specific OS, referenced by multiple Docker Images.   
   
## Container Port VS Host Port   
   
Multiple containers(even same images) can run on your host machine. Host machine has certain ports that can be opened.   
   
A binding needs to be created between your host machine and the container.   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657823871/wiki/geibagpoa2uvx95wwaxg.png)   
   
You can specify the binding of the port along with the run command.   
   
`docker run -p HostPort:ContainerPort image`   
   
`docker run -p 6000:6379 redis`   
   
## Docker Network   
   
Docker creates it’s own isolated Docker Network where the containers are running. When you deploy two containers in the same Docker Network, they can talk to each other using the Container name.   
   
Applications outside of the Docker Network connect using localhost and port number.   
   
In production, this application running/developed outside of the Network is also added to the Network.   
   
`docker network ls` list networks (some are autogenerated)   
   
`docker network create mongo-network` to create a new network   
   
Make a container run inside a Network   
   
`docker run -p 27017:27017 -d mongo`   
   
## Docker Compose   
   
> The key difference between the Dockerfile and docker-compose is that the Dockerfile describes how to build Docker images, while docker-compose is used to run Docker containers.   
   
> The contents of a Dockerfile describe how to create and build a Docker image, while docker-compose is a command that runs Docker containers based on settings described in a docker-compose.yaml file.   
   
— via [Dockerfile vs docker-compose: What's the difference?](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Dockerfile-vs-docker-compose-Whats-the-difference)   
   
Docker Compose file is basically a bunch of docker commands structured nicely so you don’t have to run each of those docker run commands one by one.   
   
`docker-compose` is a `yaml` file.   
   
Docker compose creates a common network for all the containers mentioned inside it.   
   
```yaml
version:'3' # version of docker-compose
services: # here goes the containers
	mongodb: # name of a container
		image: mongo # name of the image
		ports:
			- 27017:27017 # HOST:CONTAINER
		environment: # env variables
			- MONGO_USERNAME=admin
			- ...
	mongo-express:
		image: mongo-express
		ports:
			- 8080:8080
		environment:
			- ME_CONFIG:value
```
   
   
Start Docker container using docker-compose file.   
   
`docker-compose -f mongo.yaml up`   
   
## Dockerfile   
   
   
- It is a text file that contains all the instructions needed to create an image. A recipe for creating docker images.   
- The syntax it uses is from Docker platform and uses statements to generate docker images.   
- It also runs bash commands (single line which uses `&&` to append commands and `\` backslash for a newline.)   
- To use a Dockerfile for a custom image, copy paste the instructions from an existing Dockerfile locally and remove the `COPY` instructions to adapt it for your custom image with your own instructions.   
- To build an image from the custom Dockerfile:   
  - `docker image build -t myimage:1.0 .`   
  - You should have a Dockerfile in the current working dir.   
   
The specific commands you can use in a dockerfile are:   
   
FROM, PULL, RUN, and CMD   
   
   
- FROM - Creates a layer from the ubuntu:18.04   
- PULL - Adds files from your Docker repository   
- RUN - Builds your container(you can use multiple of these)   
- CMD - Specifies what command to run within the container (entrypoint, only one)   
- ENV - to define environment variables   
   
## Private Docker Repository   
   
   
- Creating a private docker repository on [AWS ECR](/not_created.md)   
   
## Misc   
   
Docker for Mac creates a Linux VM and stores data there.   
   
## Examples   
   
   
- [Running a Web Server in a Docker Container](../devlog/running%20a%20web%20server%20in%20a%20docker%20container.md)   
- [Connecting a Nodejs application to a MongoDB Docker container](../devlog/Connecting%20a%20Nodejs%20application%20to%20a%20MongoDB%20Docker%20container.md)   
- [Docker repository on Nexus](../devlog/Docker%20repository%20on%20Nexus.md)   
- [Nexus as Docker container](../devlog/Nexus%20as%20Docker%20container.md)   
   
## Resources   
   
   
- [Play with Docker](https://labs.play-with-docker.com/)   
- [Docker Networking Security Basics | dockerlabs](https://dockerlabs.collabnix.com/advanced/security/networking/)   
- [Docker Compose Cheatsheet – Collabnix](https://collabnix.com/docker-compose-cheatsheet/)   
- [Docker Cheatsheet – Collabnix](https://collabnix.com/docker-cheatsheet/)   
   
## Look into   
   
   
- Container VS Process