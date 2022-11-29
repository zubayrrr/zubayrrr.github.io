---
created: 1657925852407
desc: ''
id: kwbbvuw6u3l28epk3prcncf
title: Nexus as Docker container
updated: 1657927056094
---
   
Related::  [nexus](../devlog/nexus.md), [docker](../devlog/docker.md)   
   
   
---   
   
You can deploy Nexus on a standalone server like DigitalOcean Droplet or you can deploy it as a Docker container which is much faster and easier.   
   
1. Create a droplet (or a server) and ssh into it.   
2. Install only Docker (you don't need Java or anything else).   
3. Create persistent storage(volume).   
   
`docker volume create --name nexus-data`   
   
4. Start Nexus.   
   
`docker run -d -p 8081:8081 --name -v nexus-data:/nexus-data sonatype/nexus3`   
   
5. Check if Nexus(port) has started   
   
`netstat -lnpt` and `docker ps`   
   
Once port is open, you'll be able to send requests to the port, which'll forward it to the container.   
   
6. Open `http://serverIpAddress:port` on your browser to use Nexus, a new user would have been created inside the container; a service user.   
   
7. `docker inspect nexus-data` for information about the volume, you'll need this for checking password, backup etc. Alternatively you can check the container's FS.