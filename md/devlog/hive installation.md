---
created: 20211119191459070
desc: ''
id: gq0blan4ktw82wrac63bzr5
modified: 20211122214152764
title: Hive Installation
updated: 1653305310658
---
   
### Installing [hive](../devlog/hive.md)   
   
Taken from:   
<[https://drive.google.com/drive/folders/1XdPbyAc9iWml0fPPNX91Yq3BRwkZAG2M>](https://drive.google.com/drive/folders/1XdPbyAc9iWml0fPPNX91Yq3BRwkZAG2M>)   
   
    Steps for hive installation   
    Download and Unzip Hive   
    Edit .bashrc file   
    Edit hive-config.sh file   
    Create Hive directories in HDFS   
    Initiate Derby database   
    Configure hive-site.xml file   
   
    download and unzip Hive   
    =============================   
    wget [https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz](https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz)   
    tar xzf apache-hive-3.1.2-bin.tar.gz   
   
    Edit .bashrc file   
    ========================   
    sudo nano .bashrc   
    export HIVE_HOME= /home/hdoop/apache-hive-3.1.2-bin   
   
    export PATH=$PATH:$HIVE_HOME/bin   
    source ~/.bashrc   
    Edit hive-config.sh file   
    ====================================   
    sudo nano $HIVE_HOME/bin/hive-config.sh   
    export HADOOP_HOME=/home/hdoop/hadoop-3.2.1   
    Create Hive directories in HDFS   
    ===================================   
    hdfs dfs -mkdir /tmp   
    hdfs dfs -chmod g+w /tmp   
    hdfs dfs -mkdir -p /user/hive/warehouse   
    hdfs dfs -chmod g+w /user/hive/warehouse   
   
    Fixing guava problem – Additional step   
    =================   
   
    rm $HIVE_HOME/lib/guava-19.0.jar   
    cp $HADOOP_HOME/share/hadoop/hdfs/lib/guava-27.0-jre.jar $HIVE_HOME/lib/   
   
    Initialize Derby and hive   
    ============================   
    schematool -initSchema -dbType derby   
   
   
    hive   
   
    optional Step – Edit hive-site.xml   
    ===========   
    cd $HIVE_HOME/conf   
    cp hive-default.xml.template hive-site.xml   
    sudo nano hive-site.xml – change metastore location to above created hdfs path(/user/hive/warehouse)