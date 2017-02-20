# 3.5


1.Explain what is High availability of Namenode

2.Explain what is check pointing and how it is useful

3.Explain what is HDFS federation

4.What are the configuration files that are to be edited for sure while installing a hadoop cluster.




1.HDFS High Availability (HA)

In Hadoop 1.x architecture Name Node was a single point of failure, which means if your Name Node daemon is down somehow, you don’t have access to your Hadoop Cluster than after. Hadoop 2.x is featured with Name Node HA which is referred as HDFS High Availability (HA).

Hadoop 2.x supports two Name Nodes at a time one node is active and another is standby node Active Name Node handles the client operations in the cluster StandBy Name Node manages metadata same as Secondary Name Node in Hadoop 1.x When Active Name Node is down, Standby Name Node takes over and will handle the client operations then after HDFS HA can be configured by two ways 
Using Shared NFS Directory
Using Quorum Journal Manager

Hadoop 2.0 overcomes SPOF(Single point of failure) shortcoming by providing support for multiple NameNodes. It introduces Hadoop 2.0 High Availability feature that brings in an extra NameNode (Passive Standby NameNode) to the Hadoop Architecture which is configured for automatic failover.
The main motive of the Hadoop 2.0 High Availability project is to render availability to big data applications 24/7 by deploying 2  Hadoop NameNodes –One in active configuration and the other is the Standby Node in passive configuration. Both the active and passive (Standby) NameNodes have state-of-the-art metadata that ensures flawless failover for large Hadoop clusters indicating that there would not be any downtime for your Hadoop cluster and it will be available all the time.Hadoop 2.0 is keyed up to identify any failures in NameNode host and processes, so that it can automatically switch to the passive NameNode i.e. the Standby Node to ensure high availability of the HDFS services to the Big Data applications. With the advent of Hadoop 2.0


2.check pointing


HDFS metadata can be thought of consisting of two parts: the base filesystem table (stored in a file called fsimage) and the edit log which lists changes made to the base table (stored in a file called edits). Checkpointing is a process of reconciling fsimage with edits to produce a new version of fsimage. There are two benefits arising out of this: a more recent version of fsimage, and a truncated edit log.

fs.checkpoint.period controls how often this reconciliation will be triggered.  3600 means that every hour fsimage will be updated and edit log truncated. Checkpiont is not cheap, so there is a balance between running it too often and letting the edit log grow too large. This parameter should be set to get a good balance assuming typical filesystem use in your cluster.

fs.checkpoint.size is a size threshold, which, if reached by edits, will trigger an immediate checkpoint regardless of time elapsed since the last checkpoint. This is insurance from edit log getting too large under unusually heavy write traffic to the filesystem metadata.



 HDFS federation
 
 
 HDFS Federation improves the existing HDFS architecture through a clear separation of namespace and storage, enabling generic block storage layer. It enables support for multiple namespaces in the cluster to improve scalability and isolation. Federation also opens up the architecture, expanding the applicability of HDFS cluster to new implementations and use cases.
 
In order to scale the name service horizontally, federation uses multiple independent namenodes/namespaces. The namenodes are federated, that is, the namenodes are independent and don’t require coordination with each other. The datanodes are used as common storage for blocks by all the namenodes. Each datanode registers with all the namenodes in the cluster. Datanodes send periodic heartbeats and block reports and handles commands from the namenodes.

A Block Pool is a set of blocks that belong to a single namespace. Datanodes store blocks for all the block pools in the cluster.

It is managed independently of other block pools. This allows a namespace to generate Block IDs for new blocks without the need for coordination with the other namespaces. The failure of a namenode does not prevent the datanode from serving other namenodes in the cluster.

A Namespace and its block pool together are called Namespace Volume. It is a self-contained unit of management. When a namenode/namespace is deleted, the corresponding block pool at the datanodes is deleted. Each namespace volume is upgraded as a unit, during cluster upgrade.



4.What are the configuration files that are to be edited for sure while installing a hadoop cluster.


The four files that need to be configured explicitly while setting up a single node hadoop cluster are:

Core-site.xml
HDFS-site.xml
YARN-site.xml
xml

1.Settings that need to be done in Core-site.xml

Some of the important properties are:
Configuring the name node address
Configuring the rack awareness factor
Selecting the type of security

2.Settings To Be Done In HDFS-site.xml

The properties inside this xml file deals with storage procedure inside HDFS of Hadoop. Some of the important properties are:
Configure port access
Manages ssl client authentication
Controls Network interface
Changes file permission
Some of the overridden name attributes are dfs.namenode.name.dir, dfs.datanode.data.dir, blocksize, replication, etc.

3.Settings In yarn-site.xml

In Hadoop v1.x TaskTraker and JobTracker were present to handle the job of allocating resources to processes.
YARN has ResourceManager settings which effects resource allocation with node manager and application manager. Some of the important properties are:
WebAppProxy Configuration
MapReduce Configuration
NodeManager Configuration
ResourceManager Configuration
IPC Configuration
