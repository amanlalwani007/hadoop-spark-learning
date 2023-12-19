# hadoop-spark-learning

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



components in hadoop 
hive :- 