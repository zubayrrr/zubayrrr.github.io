---
created: 20211119191141548
desc: ''
id: qmso3cnm29wqblm5x47se8v
tags:
- Add
- Hadoop
- Add
- Add
- Add
- Add
- Add
title: Hadoop installation procedure
updated: 1652622337032
---
   
`/hadoop-3.3.1/etc/hadoop/hadoop-env.sh` should contain `JAVA_HOME` variable pointing to the path of your JDK   
   
`sudo nano /etc/ssh/sshd_config` check this file if you get SSH related errors such as `Permission denied (publickey,password).` Run   
`cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys` if you get such an error   
   
To set up ssh   
   
    mkdir -p $HOME/.ssh   
    chmod 0700 $HOME/.ssh   
# and   
    ssh-keygen -t rsa   
   
Actually make sure to name the PATH variable as `HIVE_HOME` and nothing else   
   
For   
`Unable to instantiate org.apache.hadoop.hive.ql.metadata.SessionHiveMetaStoreClient`   
   
cd into Hive home dir, run `rm -rf metastore_db`   
and `schematool -initSchema -dbType derby`   
   
check if hive is working properly with either   
   
`show databases;`   
or   
`show tables;`   
   
   
---   
   
Taken from:   
<[https://drive.google.com/drive/folders/1XdPbyAc9iWml0fPPNX91Yq3BRwkZAG2M>](https://drive.google.com/drive/folders/1XdPbyAc9iWml0fPPNX91Yq3BRwkZAG2M>)   
   
    Prerequisite Test   
    =============================   
    sudo apt update   
    sudo apt install openjdk-8-jdk -y   
   
    java -version; javac -version   
    sudo apt install openssh-server openssh-client -y   
    sudo adduser hdoop   
    su - hdoop   
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa   
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys   
    chmod 0600 ~/.ssh/authorized_keys   
    ssh localhost   
   
    Downloading Hadoop   
    ===============================   
    wget [https://downloads.apache.org/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz](https://downloads.apache.org/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz)   
    tar xzf hadoop-3.2.1.tar.gz   
   
   
    Editng 6 important files   
    =================================   
    1st file   
    ===========================   
    sudo nano .bashrc -  here you might face issue saying hdoop is not sudo user   
    if this issue comes then   
    su - aman   
    sudo adduser hdoop sudo   
   
    sudo nano .bashrc   
`{_obsidian_pattern_tag_Add}` below lines in this file   
   
`{_obsidian_pattern_tag_Hadoop}` Related Options   
    export HADOOP_HOME=/home/hdoop/hadoop-3.2.1   
    export HADOOP_INSTALL=$HADOOP_HOME   
    export HADOOP_MAPRED_HOME=$HADOOP_HOME   
    export HADOOP_COMMON_HOME=$HADOOP_HOME   
    export HADOOP_HDFS_HOME=$HADOOP_HOME   
    export YARN_HOME=$HADOOP_HOME   
    export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native   
    export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin   
    export HADOOP_OPTS"-Djava.library.path=$HADOOP_HOME/lib/nativ"   
   
   
    source ~/.bashrc   
   
    2nd File   
    ============================   
    sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh   
   
`{_obsidian_pattern_tag_Add}` below line in this file in the end   
   
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64   
   
    3rd File   
    ===============================   
    sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml   
   
`{_obsidian_pattern_tag_Add}` below lines in this file(between "<configuration>" and "<"/configuration>")   
       <property>   
            <name>hadoop.tmp.dir</name>   
            <value>/home/hdoop/tmpdata</value>   
            <description>A base for other temporary directories.</description>   
        </property>   
        <property>   
            <name>fs.default.name</name>   
            <value>hdfs://localhost:9000</value>   
            <description>The name of the default file system></description>   
        </property>   
   
    4th File   
    ====================================   
    sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml   
   
`{_obsidian_pattern_tag_Add}` below lines in this file(between "<configuration>" and "<"/configuration>")   
   
   
    <property>   
      <name>dfs.data.dir</name>   
      <value>/home/hdoop/dfsdata/namenode</value>   
    </property>   
    <property>   
      <name>dfs.data.dir</name>   
      <value>/home/hdoop/dfsdata/datanode</value>   
    </property>   
    <property>   
      <name>dfs.replication</name>   
      <value>1</value>   
    </property>   
   
   
   
    5th File   
    ================================================   
   
    sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml   
   
`{_obsidian_pattern_tag_Add}` below lines in this file(between "<configuration>" and "<"/configuration>")   
   
    <property>   
      <name>mapreduce.framework.name</name>   
      <value>yarn</value>   
    </property>   
   
    6th File   
    ==================================================   
    sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml   
   
`{_obsidian_pattern_tag_Add}` below lines in this file(between "<configuration>" and "<"/configuration>")   
   
    <property>   
      <name>yarn.nodemanager.aux-services</name>   
      <value>mapreduce_shuffle</value>   
    </property>   
    <property>   
      <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>   
      <value>org.apache.hadoop.mapred.ShuffleHandler</value>   
    </property>   
    <property>   
      <name>yarn.resourcemanager.hostname</name>   
      <value>127.0.0.1</value>   
    </property>   
    <property>   
      <name>yarn.acl.enable</name>   
      <value>0</value>   
    </property>   
    <property>   
      <name>yarn.nodemanager.env-whitelist</name>   
      <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PERPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>   
    </property>   
   
   
    Launching Hadoop   
    ==================================   
    hdfs namenode -format   
   
   
    ./start-dfs.sh