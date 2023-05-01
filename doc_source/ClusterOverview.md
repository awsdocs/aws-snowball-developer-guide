# Clustering overview<a name="ClusterOverview"></a>

For the AWS Snowball service, a cluster is a collective of Snowball Edge devices used as a single logical unit for local storage and compute purposes\.

A cluster offers two primary benefits over a standalone Snowball Edge device for local storage and computing:
+ **Increased durability** – The data stored in a cluster of Snowball Edge devices enjoys increased data durability over a single device\. In addition, the data on the cluster remains as safe and viable as it was previously, despite possible Snowball Edge outages in the cluster\. Clusters can withstand the loss of one device in clusters of 3 and 4 devicess and up to two devices in clusters of 5 to 16 devices before the data is in danger\. You can also add or replace nodes\.
+ **Increased storage for compute\-optimized devices** – For compute\-optimized Snowball Edge devices with Amazon S3 compatible storage on Snow Family devices, the total available storage is up to 31 terabytes of data per node in a cluster, depending on the device used\. Thus, in a sixteen\-node cluster, there are up to 501 terabytes of available storage space\. In contrast, there are about 39\.5 terabytes of available storage space in a standalone Snowball Edge compute\-optimized device\.<a name="cluster-table"></a>


**Amazon S3 compatible storage on Snow Family devices cluster fault tolerance and storage capacity**  

| Cluster size | Fault tolerance | Storage capacity of Snowball Edge Compute Optimized \(with AMD EPYC Gen1\) with up to 52 vCPUs in TB | Storage capacity of Snowball Edge Compute Optimized \(with AMD EPYC Gen2\) with up to 104 vCPU in TB | 
| --- | --- | --- | --- | 
|  3  |  Loss of up to 1 node  |  83  |  38  | 
|  4  |  Loss of up to 1 node  |  125  |  57  | 
|  5  |  Loss of up to 2 nodes  |  125  |  57  | 
|  6  |  Loss of up to 2 nodes  |  167  |  76  | 
|  7  |  Loss of up to 2 nodes  |  209  |  95  | 
|  8  |  Loss of up to 2 nodes  |  250  |  114  | 
|  9  |  Loss of up to 2 nodes  |  292  |  133  | 
|  10  |  Loss of up to 2 nodes  |  334  |  152  | 
|  11  |  Loss of up to 2 nodes  |  370  |  165  | 
|  12  |  Loss of up to 2 nodes  |  376  |  171  | 
|  13  |  Loss of up to 2 nodes  |  418  |  190  | 
|  14  |  Loss of up to 2 nodes  |  459  |  209  | 
|  15  |  Loss of up to 2 nodes  |  495  |  225  | 
|  16  |  Loss of up to 2 nodes  |  501  |  228  | 

A cluster of Snowball Edge devices is made of leaderless nodes\. Any node can write data to and read data from the entire cluster, and all nodes are capable of performing the behind\-the\-scenes management of the cluster\.

## Snowball Edge cluster quorums<a name="clusterquorums"></a>

A *quorum* represents the minimum number of Snowball Edge devices in a cluster that must be communicating with each other to maintain a read/write quorum\.

Suppose that you upload your data to a cluster of Snowball Edge devices\. With all devices healthy, you have a *read/write quorum* for your cluster\. If one or two of those nodes goes offline, you reduce the operational capacity of the cluster\. However, you can still read and write to the cluster\. In that sense, with the cluster operating all but one or two nodes, the cluster still has a read/write quorum\. The number of nodes that can go offline before the operational capacity of the cluster is affected is found in [this table](#cluster-table)\.

Finally, quorom may be breached if a cluster loses more than the number of nodes indicated in [this table](#cluster-table)\. When a quorom is breached, the cluster is offline and the data in the cluster is unavailable\. You might be able fix this, or the data might be permanently lost, depending on the severity of the event\. If it is a temporary external power event, and you can power the three Snowball Edge devices back on and unlock all the nodes in the cluster, your data is available again\.

**Important**  
If a minimum quorum of healthy nodes doesn't exist, contact AWS Support\.

You can determine the quorum state of your cluster by determining your node's lock state and network reachability\. The `snowballEdge describe-cluster` command reports back the lock and network reachability state for every node in an unlocked cluster\. Ensuring that the devices in your cluster are healthy and connected is an administrative responsibility that you take on when you create the cluster job\. For more information about the different client commands, see [Commands for the Snowball Edge Client](using-client-commands.md)\.

## Considerations for cluster jobs for Snowball Edge devices<a name="clusterconsiderations"></a>

Keep the following considerations in mind when planning to use a cluster of Snowball Edge devices:
+ We recommend that you have a redundant power supply to reduce potential performance and stability issues for your cluster\.
+ As with standalone local storage and compute jobs, the data stored in a cluster can't be imported into Amazon S3 without ordering additional devices as a part of separate import jobs\. If you order additional devices as import jobs, you can transfer the data from the cluster to the import job devices\. 
+ To get data onto a cluster from Amazon S3, create a separate export job and copy the data from the devices of the export job onto the cluster\.
+ You can create a cluster job from the console, the AWS CLI, or one of the AWS SDKs\. For a guided walkthrough of creating a job, see [Getting Started](getting-started.md)\.
+ Cluster nodes have node IDs\. A *node ID* is the same as the job ID for a device that you can get from the console, the AWS CLI, the AWS SDKs, and the Snowball Edge client\. You can use node IDs to remove old nodes from clusters\. You can get a list of node IDs by using the `snowballEdge describe-device` command on an unlocked device or the `describe-cluster` on an unlocked cluster\.
+ The lifespan of a cluster is limited by the security certificate granted to the cluster devices when the cluster is provisioned\. By default, Snowball Edge devices can be used for up to 360 days before they need to be returned\. At the end of that time, the devices stop responding to read/write requests\. If you need to keep one or more devices for longer than 360 days, contact AWS Support\.
+ When AWS receives a returned device that was part of a cluster, we perform a complete erasure of the device\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.