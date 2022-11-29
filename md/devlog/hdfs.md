---
created: 20211110214903030
desc: ''
id: kdddo1f7ltfsuwhexj4s535
title: HDFS
updated: 1653305294717
---
   
   
- Traditional filesystems are not designed for large files and fast streaming reads hence HDFS was introduced.   
- It is designed for "write once/read many" uses cases.   
- It is a distributed/spread out filesystem.   
- Requires low coherency/concurrency overhead   
  - No random file writes, one user writing at a time. (can be a restriction/constraint)   
- HDFS takes files and stripes them across different servers and then allows us to scan those files in parallel at the same time. Each chunk/slice is on a different server.   
- The goal is to **move computation to data**.   
- Uses a converged data-computation model; slice data file and place pieces on multiple computational nodes/servers.   
   
### NameNodes and Datanodes   
   
   
- HDFS uses a director/worker model.   
- The director or the daemon is called the NameNode and acts as a metadata server (data about data) or "data traffic cop".   
- NameNode keeps metadata in memory for performance.   
- Provides a single filesystem namespace that is managed by the NameNode.   
- The workers are DataNode(s)(at least one); Data is stored on these nodes.   
- A secondary NameNode checkpoints NameNode metadata to disk, but does not provide failover.   
   
### HDFS Roles   
   
   
- User client-layer talks with NameNode(transparent to user). Often called as **Edge Node**   
   
   
- NameNode keeps track of metadata and uses DataNodes for actual data storage.   
   
   
- Data flows from client node directly to/from DataNodes.   
   
   
- Secondary NameNode checkpoints the metadata to disk but is not failover.   
   
   
- ![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.zt918wn73hk.png)   
   
### The HDFS File System Namespace   
   
   
- Provides a hierarchical file system with files and directories.   
- Namespace path starts with `/` and provides user directories.   
- Users can create, remove, move, rename and copy files.   
- There are no <span class="underline">random reads or writes only appends</span>.   
- User must access HDFS through [hadoop](../devlog/hadoop.md) client layer, not directly on DataNodes or NFSv3   
- Features include: High Availability(multiple NameNodes), Federation(spread namespace across multiple NameNodes), Snapshots(instant read-only point-in-time copies), and NFSv3 mounts.   
   
### Replication in HDFS   
   
   
- Data is replicated (default is 3 copies).   
- Replication is used for both redundancy and better availability on busy clusters.   
- At 3x repliaction a 320 MB file requires 1 GB of space in HDFS.   
- HDFS V3 supports erasure coding for achived data (reduces storage space).   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.1eqf63vf4xu.png)   
   
### How The User "Sees" HDFS   
   
   
- HDFS is a separate file system from the host server(edge node).   
- All Hadoop processing happens in HDFS, but first:   
  - 1\. Data must be moved to edge node/server from user's source (local or web/cloud).   
  - 2\. Data must be moved from edge node to HDFS using put and get client commands.   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.yxr0gacpr2.png)   
   
   
---   
   
## HDFS cli   
   
#### Make a dir in HDFS   
   
`hdfs dfs -mkdir stuff` will create a dir in home dir(since no path was supplied, /users/hands-on) named "stuff"   
   
#### Copy files to HDFS   
   
`hdfs dfs -put war-and-peace.txt stuff`   
   
#### Copy files from HDFS   
   
Copy files back to your local file system   
   
`hdfs dfs -get stuff/war-and-peace.txt war-and-peace-copy.txt`   
   
#### Copy files within HDFS   
   
`hdfs dfs -cp stuff/war-and-peace.txt copy-of-war-and-peace.txt`   
   
#### Delete files within HDFS   
   
`hdfs dfs -rm copy-of-war-and-peace.txt`   
   
#### List files on HDFS (/user/hands-on)   
   
`hdfs dfs -ls`   
   
#### Delete a dir in HDFS   
   
`hdfs dfs -rm -r stuff`   
   
to skip the trash(if trash collection is enabled use `-skipTrash`)   
   
## HDFS Web Interface   
   
The HDFS web interaface: `http://127.0.0.1:50070`   
The [yarn](../devlog/yarn.md) Jobs web interface: `http://127.0.0.1:8088`   
Zeppelin Web Notebook: `http://127.0.0.9995`   
   
The HDFS web interace also features "Browse the file system" under the "Utilities" dropdown menu.