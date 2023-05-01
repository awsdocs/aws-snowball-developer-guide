# Step 2: Choose your compute and storage options<a name="compute-storage"></a>

Choose the hardware specifications for your Snow Family device, which of your Amazon EC2 instances to include on it, how data will be stored, and pricing\.

**To choose your device's compute and storage options**

1. In the **Snow devices** section, choose the Snow Family device to order\.
**Note**  
Some Snow Family devices might not be available depending on the AWS Region you are ordering from and the job type you chose\.  
![\[List of Snow device options showing compute, memory, and storage of each.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/sbe-devices.png)

1. In the **Choose your pricing option** section, from the **Pricing Option** menu, choose the type of pricing to apply to this job\. See [AWS Snowball Edge Pricing\.](https://aws.amazon.com/snowball/pricing/)\.

1. In the **Select the storage type** section, make a choice according to your need:
   + **S3 Adapter**: Use the S3 adapter to transfer data programmatically to and from Snow Family devices using Amazon S3 REST API actions\.
   + **Amazon S3 compatible storage**: Use Amazon S3 compatible storage to deploy S3 compatible durable, scalable object storage on single Snowball Edge device or in a multi\-device cluster\.
   + **NFS based data transfer**: Use Network File System \(NFS\) based data transfer to drag and drop files from your computer into Amazon S3 buckets on Snow Family devices\.
**Warning**  
NFS based data transfer doesn't support the S3 adapter\. If you proceed with NFS based data transfer, you must mount the NFS share to transfer objects\. Using the AWS CLI to transfer objects will fail\.  
See [Using NFS for Offline Data Transfer](https://docs.aws.amazon.com/snowball/latest/developer-guide/shared-using-nfs.html) in the AWS Snowball Edge Developer Guide for more information\.
**Note**  
Storage type options available depend on the job type and Snow device you chose\.

1. If you selected *S3 Adapter* as the storage type, do the following to select one or more S3 buckets to include on the device:

   1. In the **Select your S3 buckets** section, do one or more of the following to select one or more S3 buckets:

     1. Choose the S3 bucket that you want to use in the **S3 bucket name** list\.

     1. In the **Search for an item** field, enter all or part a bucket name to filter the list of available buckets on your entry, then choose the bucket\.

     1. Choose the **Create a new S3 bucket** to create a new S3 bucket\. The new bucket name appears in the **Bucket name** list\. Choose it\.

     You can include one or more S3 buckets\. These buckets appear on your device as local S3 buckets\.  
![\[Select your S3 buckets panel showing Create a new S3 bucket button, search filed, and S3 bucket names.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/select-s3-buckets-console.png)

1. If you selected *Amazon S3 compatible storage* as the storage type, in the **S3 storage capacity** section, do the following:

   1. Select to use Amazon S3 compatible storage on Snow Family devices on a single device or a cluster of devices\. See [Using an AWS Snowball Edge cluster](https://docs.aws.amazon.com/snowball/latest/developer-guide/UsingCluster.html) in this guide\.

   1. Select the amount of device storage to use for Amazon S3 compatible storage on Snow Family devices\.
**Note**  
When using Amazon S3 compatible storage on Snow Family devices, you can manage and create Amazon S3 buckets after you receive the device, so you don't need to choose them while ordering\. See [Amazon S3 compatible storage on Snow Family devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/s3compatible-on-snow.html) in this guide\.  
![\[S3 storage capacity panel showing single device selected as the device type and storage amount.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/S3-storage-capacity-console.png)

1. If you selected *NFS based data transfer* as the storage type, in the **Select your S3 buckets** section, do one or more of the following to select one or more S3 buckets:

   1. Choose the S3 bucket that you want to use in the **S3 bucket name** list\.

   1. In the **Search for an item** field, enter all or part a bucket name to filter the list of available buckets on your entry, then choose the bucket\.

   1. Choose the **Create a new S3 bucket** to create a new S3 bucket\. The new bucket name appears in the **Bucket name** list\. Choose it\.

   You can include one or more S3 buckets\. These buckets appear on your device as local S3 buckets\.  
![\[Select your S3 buckets panel showing Create a new S3 bucket button, search filed, and S3 bucket names.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/select-s3-buckets-console.png)

1. In the **Compute using EC2 instances \- *optional*** section, choose Amazon EC2 AMIs from your account to include on the device\. Or, in the search field, enter all or part the name of an AMI to filter the list of available AMIs on your entry, then choose the AMI\.

   For more information, see [Adding an AMI When Ordering Your Device](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-ami.html#add-ami-order) in this guide\.

   This feature incurs additional charges\. For more information, see [AWS Snowball Edge Pricing\.](https://aws.amazon.com/snowball/pricing/)

1. Choose the **Next** button\.