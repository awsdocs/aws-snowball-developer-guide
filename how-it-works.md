--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# How AWS Snowball Works with the Snowball Edge<a name="how-it-works"></a>

With AWS Snowball, you can use one of two appliances\. From this guide, you can learn how to use AWS Snowball with an AWS Snowball Edge appliance\. The appliances are owned by AWS, and they reside at your on\-premises location while they're in use\.

There are three job types you can use with an AWS Snowball Edge appliance\.  Although the job types differ in their use cases, every job type has the same workflow for how you order, receive, and return appliances\.

**The shared workflow**

1. **Create the job** – Each job is created in the AWS Snowball Management Console or programmatically through the job management API, and the status for a job can be tracked in the console or through the API\.

1. **An appliance is prepared for your job** – We prepare an AWS Snowball Edge appliance for your job, and the status of your job is now **Preparing Snowball**\.

1. **An appliance is shipped to you by your region's carrier** – The carrier takes over from here, and the status of your job is now **In transit to you**\. You can find your tracking number and a link to the tracking website on the console or with the job management API\. For information on who your region's carrier is, see [Shipping Considerations for AWS Snowball](shipping.md)\.

1. **Receive the appliance** – A few days later, your region's carrier delivers the AWS Snowball Edge appliance to the address that you provided when you created the job, and the status of your job changes to **Delivered to you**\. When it arrives, you’ll notice that it didn’t arrive in a box, because the appliance is its own shipping container\.

1. **Get your credentials and download the Snowball client** – Get ready to start transferring data by getting your credentials, your job manifest, and the manifest's unlock code, and then downloading the Snowball client\.

   + The Snowball client is the tool that you’ll use to manage the flow of data from the appliance to your on\-premises data destination\. You can download the Snowball client from the [AWS Snowball Tools Download](http://aws.amazon.com/snowball/tools) page\.

   + The manifest is used to authenticate your access to the appliance, and it is encrypted so that only the unlock code can decrypt it\. You can get the manifest from the console or with the job management API when the appliance is on\-premises at your location\.

   + The unlock code is a 29\-character code used to decrypt the manifest\. You can get the unlock code from the console or with the job management API\. We recommend that you keep the unlock code saved somewhere separate from the manifest to prevent unauthorized access to the appliance while it’s at your facility\.

1. **Position the hardware** – Move the appliance into your data center and open it following the instructions on the case\. Connect the appliance to power and your local network\.

1. **Power on the appliance** – Next, power on the appliance by pressing the power button above the LCD display\. Wait a few minutes, and the **Ready** screen appears\.

1. **Get the IP address for the appliance** – The LCD display has a **CONNECTION** tab on it\. Tap this tab and get the IP address for the AWS Snowball Edge appliance\.

1. **Use the Snowball client to unlock the appliance** – When you use the Snowball client to unlock the AWS Snowball Edge appliance, type the IP address of the appliance, the path to your manifest, and the unlock code\. The Snowball client decrypts the manifest and uses it to authenticate your access to the appliance\.
**Note**  
For a cluster job, there are additional steps; see [How Clustered Local Compute and Storage Works](#how-cluster)\.

1. **Use the appliance** – The appliance is up and running\. You can use it to transfer data or for local compute and storage\. You can read and write data with the Amazon S3 Adapter for Snowball or the Network File System \(NFS\) mount point\.

1. **Prepare the appliance for its return trip** – After you're done with the appliance in your on\-premises location and the file interface status is **Complete**, press the power button above the LCD display\. It takes about 20 seconds or so for the appliance to power off\. Unplug the appliance and its power cables into the cable nook on top of the appliance, and shut all three of the appliance's doors\. The appliance is now ready to be returned\.

1. **Your region's carrier returns the appliance to AWS** – When the carrier has the AWS Snowball Edge appliance, the status for the job becomes **In transit to AWS**\.
**Note**  
For export and cluster jobs, there are additional steps; see [How Export Works](#how-export) and [How Clustered Local Compute and Storage Works](#how-cluster)\.

## How Import Works<a name="how-import"></a>

Each import job uses a single Snowball appliance\. After you create a job in the AWS Snowball Management Console or the job management API, we ship you a Snowball\. When it arrives in a few days, you’ll connect the Snowball to your network and transfer the data that you want imported into Amazon S3 onto that Snowball\. When you’re done transferring data, ship the Snowball back to AWS, and we’ll import your data into Amazon S3\.

## How Export Works<a name="how-export"></a>

Each export job can use any number of AWS Snowball Edge appliances\. After you create a job in the AWS Snowball Management Console or the job management API, a listing operation starts in Amazon S3\. This listing operation splits your job into parts\. Each job part has exactly one appliance associated with it\. After your job parts are created, your first job part enters the **Preparing Snowball** status\.

**Note**  
The listing operation to split your job into parts is a function of Amazon S3, and you are billed for it as you are for any Amazon S3 operation\.

Soon after that, we start exporting your data onto an appliance\. Typically, exporting data takes one business day; however, this process can take longer\. Once the export is done, AWS gets the appliance ready for pickup by your region's carrier\.

When it arrives in a few days, you’ll connect the AWS Snowball Edge appliance to your network and transfer the data that you want imported into Amazon S3 onto the appliance\. When you’re done transferring data, ship the appliance back to AWS\. Once we receive a returned appliance for your export job part, we erase it completely\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\. This step marks the completion of that particular job part\. If there are more job parts, the next job part now is prepared for shipping\.

## How Local Compute and Storage Works<a name="how-localcompute"></a>

You can use the local compute and storage functionality of an AWS Snowball Edge appliance with all job types in regions that support Lambda\. The compute functionality is AWS Lambda powered by AWS Greengrass, where Python\-language AWS Lambda functions can be triggered by Amazon S3 PUT object actions on buckets specified when you created the job\. For more information, see [Local Compute and Storage Only Jobs](computetype.md)\.

### How Clustered Local Compute and Storage Works<a name="how-cluster"></a>

A special kind of job for local storage and compute only, the cluster job is for those workloads that require increased data durability and storage capacity\. For more information, see [Local Cluster Option](computetype.md#clusteroption)\.

**Note**  
As with standalone local storage and compute jobs, the data stored in a cluster can't be imported into Amazon S3 without ordering additional appliances as a part of separate import jobs\. Then you could transfer the data from the cluster to those appliances and import the data when you return the appliances for the import jobs\.

Clusters have anywhere from 5 to 10 AWS Snowball Edge appliances, called nodes\. When you receive the nodes from your regional carrier, connect all the nodes to power and network to obtain their IP addresses\. With these IP addresses, you unlock all the nodes of the cluster at once with a single unlock command, with the IP address of one of the nodes\. For more information, see [Using the Snowball Client](using-client.md)\.

You can write data to an unlocked cluster by using the Amazon S3 Adapter for Snowball or the NFS mount point through the leader node, and it distributes the data among the other nodes\.

When you’re done with your cluster, ship all the nodes back to AWS\. Once we receive a returned cluster node, we perform a complete erasure of the Snowball\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.