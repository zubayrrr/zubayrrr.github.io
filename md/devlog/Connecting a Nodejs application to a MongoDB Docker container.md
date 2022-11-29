---
created: 1657828890111
desc: ''
id: n0qgelqjpctzky75c80cflo
title: Connecting a Nodejs application to a MongoDB Docker Container
updated: 1657839199740
---
   
For our front-end, let's say we've a simple html front-end being served by express on port 3000(backend).   
   
To add persistent storage, we'll integrate the application with a DB, lets use MongoDB and MongoExpress as the UI of the DB, both as Docker containers.   
   
Create a new Docker Network and start the Mongo container inside that newly created network.   
   
`docker network create mongo-network`   
   
Running mongo container   
   
```bash
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb \
  --net mongo-network \
  mongo
```
   
   
Running mongo-express container   
   
```bash
docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  --net mongo-network \
  --name mongo-express \
  -e ME_CONFIG_MONGODB_SERVER=mongodb # container name
  mongo-express
```
   
   
Create a new DB from the mongo express UI (alternatively you can specify init DB as env variable)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657832258/wiki/kjuyn47bzyftrwrfuzro.png)   
   
Create a collection(like a table)   
   
![](https://res.cloudinary.com/zubayr/image/upload/v1657832418/wiki/ti6cf756ul3v2qjjmalg.png)   
   
Connect Nodejs server with MongoDB container.   
   
Using `MongoClient` to connect to mongodb `mongodb://admin:password@localhost:27017` or `mongodb://admin:password@mongodb:27017` or `mongodb://admin:password@mongodb`