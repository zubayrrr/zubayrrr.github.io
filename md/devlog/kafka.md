---
created: 20211128153249908
desc: ''
id: 70j0z3fabx73iaz9nx3895y
title: Kafka
updated: 1653318643782
---
   
Topics::  [Data Engineering](/not_created.md)   
   
   
---   
   
   
- Apache Kafka is a distributed publish-subscribe (pub sub) messaging system   
- It was originally developed at LinkedIn and later on became part of Apache Project   
- Kafka is fast, scalable, durable, fault-tolerant and distributed by design   
   
### Kafka terminologies   
   
#### Topic   
   
A topic is a category or feed name to which records are published, a topic is always a multi subscriber, a topic can have zero, one or multiple subscribers that can subscribe to the topic and consume data written to it.   
   
#### Producer   
   
A producer can be any application that can publish messages to a topic.   
   
#### Consumer   
   
A consumer can be any application that subscribes to a topic and consumes the messages, a consumer can subscribe to one or more  They label themselves with a Consumer Group Name and each record published to a topic is delivered to one consumer instance within each subscribing consumer group. It can only be consumed once by a single consumer group. Consumer instances can be separate processes or separate machines.   
   
#### Partition   
   
Topics are broken up into ordered commit logs called partitions, paritions allows you to parallelize a topic by splitting data across multiple brokers. Each partition can be placed on separate machines to allow multiple consumer to read from a topic parallely   
   
#### Broker   
   
Kafka cluster is a set of servers, each of which is called a broker. A broker is a single machine in the kafka cluster.   
   
#### Zookeeper   
   
Zookeeper is used for managing and coordinating Kafka broker, it stores the metadata about Kafka cluster such as broker info, topic details etc. Zookeeper helps in managing Kafka cluster.