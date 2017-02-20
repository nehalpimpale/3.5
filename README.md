# 3.5


HDFS High Availability (HA)

In Hadoop 1.x architecture Name Node was a single point of failure, which means if your Name Node daemon is down somehow, you don’t have access to your Hadoop Cluster than after. Hadoop 2.x is featured with Name Node HA which is referred as HDFS High Availability (HA).

Hadoop 2.x supports two Name Nodes at a time one node is active and another is standby node
Active Name Node handles the client operations in the cluster
StandBy Name Node manages metadata same as Secondary Name Node in Hadoop 1.x
When Active Name Node is down, Standby Name Node takes over and will handle the client operations then after
HDFS HA can be configured by two ways
Using Shared NFS Directory
Using Quorum Journal Manager
