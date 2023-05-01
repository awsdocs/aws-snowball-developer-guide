# Administering a cluster<a name="administerclusterfortpoint"></a>

## Reading and writing data to a cluster<a name="transfer-to-cluster"></a>

After you unlock a cluster, you're ready to store and access data on that cluster\. You can use the Amazon S3 compatible endpoint to read from and write data to a cluster\.

To read from or write data to a cluster, you must have a read/write quorum with no more than the allowed number of unavailable nodes in your cluster of devices\.

## Reconnecting an unavailable cluster node<a name="reconnectingclusternodefortpoint"></a>

A *node*, or device within a cluster, can become temporarily unavailable due to an issue like power or network loss without damaging the data on the node\. When this happens, it affects the status of your cluster\. A node's network reachability and lock status is reported in the Snowball Edge client by using the `snowballEdge describe-cluster` command\.

We recommend that you physically position your cluster so you have access to the front, back, and top of all nodes\. This way, you can access power and network cables on the back, shipping labels on the top for node IDs, and LCD screens on the front of the devices for the IP addresses and other administrative information\.

When you detect that a node is unavailable, we recommend that you try one of the following procedures, depending on the scenario that caused the node to become unavailable\.

**To reconnect an unavailable node**

1. Ensure that the node is powered on\.

1. Ensure that the node is connected to the same internal network that the rest of the cluster is connected to\.

1. If you need to power up the node, wait up to 20 minutes for it to finish\.

1. Run the `snowballEdge unlock-cluster` command or the `snowballEdge associate-device` command\. For an example, see [Unlocking Snowball Edge devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#setting-up-client)\.

**To reconnect an unavailable node that lost network connectivity, but didn't lose power**

1. Ensure that the node is connected to the same internal network that the rest of the cluster is on\.

1. Run the `snowballEdge describe-device` command to see when the previously unavailable node is added back to the cluster\. For an example, see [Getting Device Status](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#client-status)\.

After you perform the preceding procedures, your nodes should be working normally\. You should also have a read/write quorum\. If that's not the case, then one or more of your nodes might have a more serious issue and might need to be removed from the cluster\.

## Adding or replacing a node in a cluster<a name="replacement"></a>

You can add a new node after you have removed an unhealthy node from a cluster\. You can also add a new node to increase local storage\. 

To add a new node, you first need to order a replacement\. You can order a replacement node from the console, the AWS CLI, or one of the AWS SDKs\. If you're ordering a replacement node from the console, you can order replacements for any job that hasn't been canceled or completed\.

**To order a replacement node from the console**

1. Sign in to the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\.

1. Find and choose a job for a node that belongs to the cluster that you created from the Job dashboard\.

1. For **Actions**, choose **Replace node**\.

   Doing this opens the final step of the job creation wizard, with all settings identical to how the cluster was originally created\.

1. Choose **Create job**\.

Your replacement Snowball Edge is now on its way to you\. When it arrives, use the following procedure to add it to your cluster\.

**To add a replacement node**

1. Position the new node for the cluster such that you have access to the front, back, and top of all nodes\.

1. Ensure that the node has power\.

1. Ensure that the node is connected to the same internal network that the rest of the cluster is on\.

1. Wait for the node to finish powering up \(if it needed to be powered up\)\.

1. Run the `snowballEdge associate-device` command\. For an example, see [Adding a Node to a Cluster](using-client-commands.md#client-cluster-add)\.