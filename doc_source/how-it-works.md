# How AWS Snowball Edge Works<a name="how-it-works"></a>

AWS Snowball Edge devices are owned by AWS, and they reside at your on\-premises location while they're in use\.

There are three job types you can use with an AWS Snowball Edge device\.  Although the job types differ in their use cases, every job type has the same workflow for how you order, receive, and return devices\. Regardless of the job type, every job follows a data erasure of the National Institute of Standards and Technology \(NIST\) 800\-88 standard after the job completes\.

**The shared workflow**

1. **Create the job** – Each job is created in the AWS Snow Family Management Console or programmatically through the job management API\. The status for a job can be tracked in the console or through the API\.

1. **A device is prepared for your job** – We prepare an AWS Snowball Edge device for your job, and the status of your job is now **Preparing Snowball**\.

1. **A device is shipped to you by your region's carrier** – The carrier takes over from here, and the status of your job is now **In transit to you**\. You can find your tracking number and a link to the tracking website on the console or with the job management API\. For information about who your region's carrier is, see [Shipping Considerations for AWS Snowball](shipping.md)\.

1. **Receive the device** – A few days later, your region's carrier delivers the AWS Snowball Edge device to the address that you provided when you created the job, and the status of your job changes to **Delivered to you**\. When it arrives, you’ll notice that it didn’t arrive in a box, because the device is its own shipping container\.

1. **Get your credentials and download the Snowball Edge client** – Get ready to start transferring data by getting your credentials, your job manifest, and the manifest's unlock code, and then downloading the Snowball Edge client\.
   + The 8 client is the tool that you use to manage the flow of data from the device to your on\-premises data destination\.

     You can download and install the Snowball Edge client from the [AWS Snowball resources](http://aws.amazon.com/snowball/resources/) page\.

     You must download the Snowball Edge client from the [AWS Snowball Edge Resources](http://aws.amazon.com/snowball-edge/resources/) page and install on a powerful workstation that you own\.
   + The manifest is used to authenticate your access to the device, and it is encrypted so that only the unlock code can decrypt it\. You can get the manifest from the console or with the job management API when the device is on\-premises at your location\.
   + The unlock code is a 29\-character code used to decrypt the manifest\. You can get the unlock code from the console or with the job management API\. We recommend that you keep the unlock code saved somewhere separate from the manifest to prevent unauthorized access to the device while it’s at your facility\.

1. **Position the hardware** – Move the device into your data center and open it following the instructions on the case\. Connect the device to power and your local network\.

1. **Power on the device** – Next, power on the device by pressing the power button above the LCD display\. Wait a few minutes, and the **Ready** screen appears\.

1. **Get the IP address for the device** – The LCD display has a **CONNECTION** tab on it\. Tap this tab and get the IP address for the AWS Snowball Edge device\.

1. **Use the Snowball Edge client to unlock the device** – When you use the Snowball Edge client to unlock the AWS Snowball Edge device, enter the IP address of the device, the path to your manifest, and the unlock code\. The Snowball Edge client decrypts the manifest and uses it to authenticate your access to the device\.

1. **Use the device** – The device is up and running\. You can use it to transfer data or for local compute and storage\. You can read and write data with the Amazon S3 interface or the Network File System \(NFS\) mount point\.

1. **Prepare the device for its return trip** – After you're done with the device in your on\-premises location and the file interface status is **Complete**, press the power button above the LCD display\. It takes about 20 seconds or so for the device to power off\. Unplug the device and its power cables into the cable nook on top of the device, and shut all three of the device's doors\. The device is now ready to be returned\.

1. **Your region's carrier returns the device to AWS** – When the carrier has the AWS Snowball Edge device, the status for the job becomes **In transit to AWS**\.
**Note**  
There are additional steps for export and cluster jobs\. For more information, see [How Export Jobs Work](#how-export) and [How a Clustered Local Compute and Storage Job Works](#how-cluster)\.

**Topics**
+ [How Import Jobs Work](#how-import)
+ [How Export Jobs Work](#how-export)
+ [How Local Compute and Storage Jobs Work](#how-localcompute)
+ [Snowball Edge Videos and Blogs](#blog-videos)

## How Import Jobs Work<a name="how-import"></a>

Each import job uses a single Snowball appliance\. After you create a job in the AWS Snow Family Management Console or the job management API, we ship a Snowball to you\. When it arrives in a few days, you connect the Snowball Edge device to your network and transfer the data that you want imported into Amazon S3 onto the device\. When you’re done transferring data, ship the Snowball back to AWS, and we import your data into Amazon S3\.

## How Export Jobs Work<a name="how-export"></a>

Each export job can use any number of AWS Snowball Edge devices\.  If the listing contains more data than can fit on a single device, multiple devices are provided to you\. Each job part has exactly one device associated with it\. After your job parts are created, your ﬁrst job part enters the **Preparing Snowball** status\.

**Note**  
The listing operation used to split your job into parts is a function of Amazon S3, and you are billed for it the same way as any Amazon S3 operation\.

Soon after that, we start exporting your data onto a device\. Typically, exporting data takes one business day\. However, this process can take longer depending on the amount and type of data\. When the export is done, AWS gets the device ready for pickup by your region's carrier\. When it arrives, you connect the AWS AWS Snowball Edge device to your network and transfer the data that you want to import from Amazon S3 onto the device\. 

When you’re done transferring data, ship the device back to AWS\. When we receive the device for your export job part, we erase it completely\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\. This step marks the completion of that particular job part\.
+ For keylisting 

  Before we export the objects in the S3 bucket, we scan the bucket\. If the bucket is altered after the scan, the job could encounter delays because we scan for missing or altered objects\.
+ For S3 Glacier Flexible Retrieval

   It is important to note that AWS Snowball cannot export objects in the S3 Glacier Flexible Retrieval storage class\. These objects must be restored before AWS Snowball can successfully export the objects in the bucket\.

## How Local Compute and Storage Jobs Work<a name="how-localcompute"></a>

You can use the local compute and storage functionality of an AWS Snowball Edge device with all job types in AWS Regions that support Lambda\. The compute functionality is named AWS Lambda powered by AWS IoT Greengrass, where Python\-language AWS Lambda functions can be triggered by Amazon S3 `PUT` object actions on buckets specified when you created the job\. For more information, see [Local Compute and Storage Only Jobs](computetype.md)\.

### How a Clustered Local Compute and Storage Job Works<a name="how-cluster"></a>

A cluster job is a special kind of job for local storage and compute only\. It is for those workloads that require increased data durability and storage capacity\. For more information, see [Local Cluster Option](computetype.md#clusteroption)\.

**Note**  
Like standalone local storage and compute jobs, the data stored in a cluster can't be imported into Amazon S3 without ordering additional devices as a part of separate import jobs\. If you order these devices, you can transfer the data from the cluster to the devices and import the data when you return the devices for the import jobs\.

Clusters have 5–10 AWS Snowball Edge devices, called *nodes*\. When you receive the nodes from your regional carrier, connect all the nodes to power and your network to obtain their IP addresses\. You use these IP addresses to unlock all the nodes of the cluster at once with a single unlock command, using the IP address of one of the nodes\. For more information, see [Using the Snowball Edge Client](using-client.md)\.

You can write data to an unlocked cluster by using the Amazon S3 interface or the NFS mount point through the leader node and the data distributed among the other nodes\.

When you’re done with your cluster, ship all the nodes back to AWS\. When we receive the cluster node, we perform a complete erasure of the Snowball\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.

## Snowball Edge Videos and Blogs<a name="blog-videos"></a>
+ [AWS Snowball Edge Data Migration](https://d1.awsstatic.com/whitepapers/snowball-edge-data-migration-guide.pdf)
+ [AWS OpsHub for Snow Family](https://www.youtube.com/watch?v=_A3A47Vuu0I)
+ [Novetta delivers IoT and Machine Learning to the edge for disaster response](https://aws.amazon.com/blogs/storage/novetta-delivers-iot-and-machine-learning-to-the-edge-for-disaster-response/)
+ [Enable large\-scale database migrations with DMS and AWS Snowball](https://aws.amazon.com/blogs/storage/enable-large-scale-database-migrations-with-aws-dms-and-aws-snowball/)
+ [Data Migration Best Practices with AWS Snowball Edge](https://aws.amazon.com/blogs/storage/data-migration-best-practices-with-snowball-edge/)
+ [AWS Snowball resources](https://aws.amazon.com/snowball/resources/)