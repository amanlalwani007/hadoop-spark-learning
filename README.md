# hadoop-spark-learning
link for revision :- https://youtu.be/Tyg1FVNq40g?si=dhtsmVfnR_7I7w_p

hadoop has two projects , mainly below 2 are main components , others are extension developed by different companies 
1 . hdfs :- derived from google file system 
2. map reduce  :- google map reduce 

FAQ
1. what is File system ?
used to read and write from  and to hd. it is a layer used between software and hardware  ex:- ntfs(new technology file system used in windows) , ext(extensible file system used in linux), macfs(used in mac), hdfs, s3 . 
ntfs , ext :- standalone file system 
hdfs and s3 :- distributed file system

2. What is Block?
NTFS spilts data into partition before storing  into drive , that partition called blocks . benefit of blocking that readigg will be faster  , in ntfs(windows) block size is 16kb and in ext(linux) its 512 kb.

3. Client and Server ?
 facebook.com is server and our browser machine is client 

4. Types of File system ?
standalone :- ntfs, ext 
distributed :- hdfs , s3, cfs

5. Types of distributed system ?
  master and slave:-  in this master communicate to slaves and there is no communication between slaves. Framework use this architecture :- Haddop , Spark , Storm  , its have single point of communication(SPOC) and Single point of Failure(SPOF).
  peer to peer :- is is slaveess architecture , all nodes are interconnected if any of node goes  down all other down get to know abot it , used in Cassandra .

6. what is process ?
 a program is execution is called process . 

7. Cluster vs Node 
Node :- indivisual physical or virtual machine 
cluster :- group of nodes 

HDFS Block size :- 64mb(default) by version 1  it changes to 128 mb in version 2 


Replication :- 
if you want to store 1 gb of data then need 3 gb of storage,  1 block of data cannot be store multiple time in same node  . 


Hadoop concepts :
 Edge node is a oncept using which user will not able to connect to master and slave nodes directly 
 medatadata is stored when you send request to upload a file on hdfs  EX:- how many blocks will be created like for 1gb filr its 1gb/64 mb and then in which nodes they wil be stored and their replica also. 

 for every 2 second master will communicate to slave, if it does not communicate then master will think slaVe is down
 hadoop works on automatic failover if one of the node goes down  then haddop make the replica in new node again . 

 till version 1 there is no avaiability of HA(high availability ). In version 1 if master goes down then everything goes down.

job process  in hadoop 
jp1 - Name Node 
jp2 :- Data node 
Jp3 :- Secondly Name Node 
Jp4 :- Job Tracker(v1) / Resoouce  manager(>v1)
jp5 :- Task Tracker(v1)/Node manager(>v1)
Jp4 and jP5 used in mapreduce


 how they implement HA(High availability) in version 2?
 in hadoop  they have active name nodes and  can have multiple passive name nodes. 
 only active name node will do read and write on data nodes and passive name nodes only receive heartbeat from data nodes .
 All metadata is written on zonal node and it can also be multiple  .  
 Zookeeper maintains all name nodes and he is responsible to choosing which passive name nodes will become actina name node if  active name node goes down.

 Zookeeper works on leader follower mechanism if any leader goes down then next follower become leader.


Quo Types of Nodes 
V1 
1. master  node 
Name node + job tracker 
2. Slave Node 
Data Node + task tracker
3. Checkpointing (Secondary name node)



v2(without HA)
1. master node 
name node+resource manager 
2. slave node 
 data node +node manager
3. Secondary name node



Types of cluster
1. Single Node (pseudo node):- means all daemon in single node (name node , data node, task tracker , job tracker, secondary name node), there wil no distribution and no replication .

2. Distributed Cluster:- you should at least 5 node . 1 master 1 secondary name node and 3 data node

v2(with HA):- 1 active name node 1 passive name node (resouce maneger will run on same node or you can have multiple nodes for that also). 3 zookeeper and 3 journal node and multiple datanode+nodemanager nodes.

with ha passive name node work like secondary name node


hdfs is  inspired from gfs (google file system)
hadoop map reduce inspired from google map reduce 



Extension  in hadoop :-  
hive :- it is developed  by facebook . it gives sql support  for map reduce , kine of wrapper which converts your sql to java in backend . 

pig :- it is developed by yahoo , in this the language that is being used is piglatin, it  is same as of hive thay have writeen wrapper which converts piglatin to java in backend . 

scoop :- it is develop by group of community  members. it caontains set of commands that enable you to get data from rdbms to hdfs and  vice versa . 

oozie :- it is develop by yahoo .  it  is a scheduler , they wrote wrapper which enable you to write schedule configuration in xml but in backend it go as java . 


hive, pig, scoop and zoozie are Abstraction of map reduce

Hbase :- hadoop databse developed by facebook , it a non relational database  that runs on top of hdfs . 

mahout:- it is a data sciene component in hadoop used in machine learning . 

flume:- it is a messaging queue 

haddop is loosely coupled framework , you can remove any abov componnets but core logic will work . it can be connect with non big data componenets ex :- spark 

Hadoop single Node Setup :- 
1. install java 
2. download hadoop from https://archive.apache.org/dist/hadoop/common/hadoop-2.9.1/
3. set path for haddop installation in bashrc or zshrc  :
export HADOOP_HOME=/Users/I1447/hadoop-2.9.1
export HBASE_HOME=/Users/I1447/hbase-2.2.5
export HIVE_HOME=/Users/I1447/apache-hive-2.3.5-bin
export SPARK_HOME=Users/I1447/spark-2.4.6-bin-hadoop2.7
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HBASE_HOME/bin:$HIVE_HOME/bin:$SPARK_HOME/bin

4. Modigy hadoop configuration  files  
NAMENODE -> core-site.xml
Resource  manager -> mapperd-site.xml
secondarynamenode -> 
datanode-> slaves 
nodemanager  -> slaves & tarn-site.xml 

Installation steps :- https://github.com/Gowthamdataengineer/bigdata/wiki/Hadoop-Single-Node-Installation

Command to create namenode directory :- 
/Users/I1447/hadoop-2.9.1/bin/hadoop namenode -format

To run hadoop finally :- 
sbin/start-all.sh
<!--  to run haddop without entering local machine password again and again just add id_rsa.pub data in authorized_keys in .ssh folder -->

to stop hadoop 
sbin/stop-all.sh

To check running status :- 
➜  hadoop-2.9.1 jps
76530 ResourceManager
76404 SecondaryNameNode
76263 DataNode
76698 Jps
76141 NameNode
76636 NodeManager

Namenode Web ui :- http://localhost:50070/dfshealth.html#tab-overview
Resource manager web ui : - http://localhost:8088/cluster

to lost all files in haddop fs 
hadoop fs -ls /
make a dir :- 
➜  hadoop-2.9.1 hadoop fs -mkdir /data
copy command from local to hdfs 
➜  hadoop-2.9.1 hadoop fs -put ~/Downloads/machine-readable-business-employment-data-sep-2023-quarter.csv /sample_data.csv


HDFS Quotas
there are two types of quotas in hdfs 
Space quota: Limits the amount of space used by a directory. This is the number of bytes that can be used by all files in a directory.
Name quota: Limits the number of file and directory names used.

Commands 
hadoop dfsadmin -setSpaceQuota 100 /tech

hadoop dfsadmin -clrSpaceQuota /tech  

100 is in bytes 

hadoop dfsadmin -setQuota 3 /tech
hadoop dfsadmin -clrQuota /tech 


hive compaction :- when you do update on any record hdfs maintain both the data so to delete the old data we need to give caompaction 

MAp Reduce  
FAQ :

what is map reduce?
processing framework 

What language used in MR?
Java by default 

Advantage of using MR ?
cluster monitoring 
resource allocation 
cluster management 
scheduling 
execution  
speculative execution 

Aim of MR ?
parallelism

Abstraction of MR ?
Hive , pig , sqoop , oozie

Alternate of MR ?
spark  

Daemon of MR ?
jobtracker and tasktracker - V1
Resource manager and node manager - V2


