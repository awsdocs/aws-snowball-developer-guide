--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using the Snowball Client<a name="using-client"></a>

Following, you can find information about how to get and use the Snowball client with your AWS Snowball Edge appliance\. The Snowball client is a standalone terminal application that you run on your local server to unlock the appliance and get credentials, logs, and status information\. You can also use the client for administrative tasks for a cluster\. When you read and write data to the AWS Snowball Edge appliance, you use the Amazon S3 Adapter for Snowball or the file interface\.

## Download and Install the Snowball Client<a name="download-client"></a>

You can download and install the Snowball client from the [AWS Snowball Tools Download](http://aws.amazon.com/snowball/tools) page\. When you've reached that page, find the installation package for your operating system and follow the instructions to install the Snowball client\. Running the Snowball client from a terminal in your workstation might require using a specific path, depending on your operating system:

+ **Microsoft Windows** – When the client has been installed, you can run it from any directory without any additional preparation\.

+ **Linux** – The Snowball client must be run from the \~/snowball\-client\-linux\-*build\_number*/bin/ directory\.

+ **Mac** – The **install\.sh** script creates symbolic links \(symlinks\) in addition to copying folders from the Snowball client \.tar file to the /usr/local/bin/snowball directory\. If you run this script, you can then run the Snowball client from any directory, as long as the /usr/local/bin is a path in your bash\_profile\. You can verify your path with the `echo $PATH` command\.

## Commands for the Snowball Client<a name="using-client-commands"></a>

Following, you can find information on the Snowball client commands, including examples of use and sample outputs\.

### Unlocking<a name="client-unlock"></a>

The `unlock` command unlocks access to the AWS Snowball Edge appliance with the AWS Snowball Edge appliance's IP address and your credentials\.

If you're unlocking a cluster, you use the `-i` option for your primary node and the `-s` option for each secondary node, as in the following example\. All nodes are identical until you assign one to be the primary node\. The primary node is the leader of the cluster and performs most of the behind\-the\-scenes management of the cluster\. For more information on clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\.

**Usage**

```
snowballEdge unlock -i IP Address -m Path/to/manifest/file -u
 29 character unlock code
```

**Example Single Device Unlock Input**  

```
snowballEdge unlock -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234
```

**Example Single Device Unlock Output**  

```
The Snowball Edge unlock status is: UnlockSnowballResult(status=UNLOCKING)
```

**Example Cluster Unlock Input**  

```
snowballEdge unlock -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234 -s 192.0.2.1 -s 192.0.2.2 -s 192.0.2.3 -s 192.0.2.4
```

**Example Cluster Unlock Output**  

```
Snowball Unlock Status: SUCCESS
Node Ip:  [Node Id, State]
192.0.2.0 : [JID850f06EXAMPLE-4EXA-MPLE-2EXAMPLEab00, AVAILABLE]
192.0.2.1 : [JID850f06EXAMPLE-4EXA-MPLE-2EXAMPLEab01, AVAILABLE]
192.0.2.2 : [JID850f06EXAMPLE-4EXA-MPLE-2EXAMPLEab02, AVAILABLE]
192.0.2.3 : [JID850f06EXAMPLE-4EXA-MPLE-2EXAMPLEab03, AVAILABLE]
192.0.2.4 : [JID850f06EXAMPLE-4EXA-MPLE-2EXAMPLEab04, AVAILABLE]
Total Size: 225 TB
Free Space: 121 TB
Primary Node: 192.0.2.0
S3 Endpoint running at: http://192.0.2.0:8080
Durability Status: HEALTHY - The Snowball Edge cluster is highly durable.
```

### Getting Credentials<a name="client-credentials"></a>

The `credentials` command returns the set of local credentials \(an access key and a secret key\) that you use to sign your requests when using the AWS CLI or your own application with the Amazon S3 Adapter for Snowball to read and write data to the AWS Snowball Edge appliance\. These credentials are only associated with an individual job for AWS Snowball, and they can only be used on the appliance or cluster of appliances\. The appliance or appliances don't have any AWS Identity and Access Management \(IAM\) permissions in the AWS Cloud\.

**Note**  
If you're using the AWS CLI with the Snowball Edge, you must use these credentials when you configure the CLI\. For information on configuring credentials for the CLI, see [Quick Configuration](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-quick-configuration) in the *AWS Command Line Interface User Guide\. *

**Usage**

```
snowballEdge credentials -i IP Address -m Path/to/manifest/file -u 29 character unlock code
```

**Example Input**  

```
snowballEdge credentials -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234
```

**Example Output**  

```
[snowballEdge]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

### Getting Status<a name="client-status"></a>

The `status` command returns the status of an AWS Snowball Edge appliance\. When you run this command to check the status of a cluster, the IP address you should use is the IP address of the primary node\. For more information on clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\. 

**Usage**

```
snowballEdge status -i IP Address -m Path/to/manifest/file -u 29 character unlock code
```

**Example Input**  

```
snowballEdge status -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234
```

**Example Output**  

```
Snowball Status: SUCCESS
S3 Endpoint running at: http://192.0.2.0:8080
Total Size: 82 TB
Free Space: 74 TB
```

### Getting AWS Lambda Powered by AWS Greengrass And File Interface Logs<a name="client-logs"></a>

The `logs` command saves a copy of the Lambda and file interface logs to the specified path on your server in an archive format\. You can specify the path with the `-o` option\.

**Usage**

```
snowballEdge logs -i IP Address -m Path/to/manifest/file -u 29 character unlock code -o Path/to/logs
```

**Example Input**  

```
snowballEdge logs -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234 -o ~/
```

**Example Output**  

```
Snowball logs written to: /home/dan/snowballLogs-14EXAMPLE8009.zip
```

### Getting Device Logs<a name="client-servicelogs"></a>

The `servicelogs` saves a encrypted blob of support logs from a Snowball Edge or cluster to the specified output path on your server\. Give these logs to AWS Support when debugging issues\.

**Usage**

```
snowballEdge servicelogs -o Path/to/service/logs/output/directory -i IP Address -m Path/to/manifest/file -u 29 character unlock code
```

**Example Input**  

```
snowballEdge servicelogs -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234 -o ~/
```

**Example Output**  

```
Snowball servicelogs written to: /home/dan/snowballLogs-14EXAMPLE8010.bin
```

### Removing a Node from a Cluster<a name="client-cluster-remove"></a>

The `removenode` command removes a node from a cluster of Snowball Edge devices\. Use this command if a node has become unavailable\. For more information on clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\.

**Important**  
Use the `removenode` command only when you are removing a unresponsive node\. Don't use this command to remove a healthy node\.

If a node was accidentally powered off or disconnected from the network and was therefore temporarily unavailable to the rest of the cluster, you don't have to use this command\. In this case, simply plug the previously unavailable node back into power and the network\. The node should then rejoin the cluster automatically\.

**Usage**

```
snowballEdge removenode -i IP Address -m Path/to/manifest/file -u 29 character unlock code -n node id of unavailable node
```

**Example Input**  

```
snowballEdge removenode -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234 -n JIDfEXAMPLE-1234-abcd-1234-4EXAMPLE8ae9
```

**Example Output**  

```
The node: JIDfEXAMPLE-1234-abcd-1234-4EXAMPLE8ae9 was successfully removed from the cluster.
```

### Adding a Node to a Cluster<a name="client-cluster-add"></a>

The `addnode` command adds a node to a cluster of Snowball Edge devices\. You can use this command to replace an unavailable node with a new node that you ordered as a replacement\. You can also use this command to re\-add a node that was disconnected and removed with the `removenode` command\. For more information on clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\.

**Important**  
Don't attempt to re\-add any node that you previously removed from the cluster with the `snowballEdge removenode` command\.

**Usage**

```
snowballEdge addnode -i IP Address -m Path/to/manifest/file -u 29 character unlock code -a IP address of the node to be added
```

**Example Input**  

```
snowballEdge addnode -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234 -a 192.0.2.5
```

**Example Output**  

```
The node: 192.0.2.5 was successfully added to the cluster.
```

## Unlocking the AWS Snowball Edge Appliance<a name="setting-up-client"></a>

To unlock the AWS Snowball Edge appliance, run the `snowballEdge unlock` command\. This command authenticates your access to the AWS Snowball Edge appliance\. To run this command, the AWS Snowball Edge appliance you use for your job must be onsite, plugged into power and network, and turned on\. In addition, the LCD display on the AWS Snowball Edge appliance's front must indicate that the appliance is ready for use\.

**To authenticate the Snowball client's access to an AWS Snowball Edge appliance**

1. Obtain your manifest and unlock code\.

   1. Get the manifest from the AWS Snowball Management Console or the job management API\. Your manifest is encrypted so that only the unlock code can decrypt it\. The Snowball client compares the decrypted manifest against the information that was put in the AWS Snowball Edge appliance when it was being prepared\. This comparison verifies that you have the right AWS Snowball Edge appliance for the data transfer job you’re about to begin\. 

   1. Get the unlock code, a 29\-character code that also appears when you download your manifest\. We recommend that you write it down and keep it in a separate location from the manifest that you downloaded, to prevent unauthorized access to the AWS Snowball Edge appliance while it’s at your facility\.

1. Locate the IP address for the AWS Snowball Edge appliance on the AWS Snowball Edge appliance's LCD display\. When the AWS Snowball Edge appliance is connected to your network for the first time, it automatically creates a DHCP IP address\. If you want to use a different IP address, you can change it from the E Ink display\. For more information, see [Using an AWS Snowball Edge](using-appliance.md)\.

1. Execute the `snowballEdge unlock` command to authenticate your access to the AWS Snowball Edge appliance with the AWS Snowball Edge appliance's IP address and your credentials, as follows:

   ```
   snowballEdge unlock -i [IP Address] -m [Path/to/manifest/file] -u [29
                       character unlock code]
   ```  
**Example**  

   ```
   snowballEdge unlock -i 192.0.2.0 -m /user/tmp/manifest -u 01234-abcde-01234-ABCDE-01234
   ```

## AWS Snowball Edge Appliance Logs<a name="logs"></a>

When you transfer data between your on\-premises data center and an AWS Snowball Edge appliance, logs are automatically generated\. If you encounter unexpected errors during data transfer to the AWS Snowball Edge appliance, you can use the `snowballEdge logs` command to save a copy of the logs to your local server\.

The logs are downloaded in a compressed folder, saved with the file name snowballLogs\_*time stamp*\.zip\. The time stamp is based on your system time\. All logs are encrypted, except for any AWS Lambda application logs that are a part of the functions you created\. These encrypted logs can be used to help AWS Support engineers resolve issues if you reach out to us\.

**Important**  
Lambda logs are saved in plaintext format and might contain sensitive information, if you programmed the logs to do so\. To protect this potentially sensitive information, we strongly suggest that you delete these logs once you're done with them\.