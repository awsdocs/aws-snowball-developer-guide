# Step 3: Choose Your Job Details<a name="import-job-details"></a>

In this step, you provide details for your AWS Snow Family device job, including the job name, AWS Region, device type, Amazon S3 bucket name, and Amazon Machine Image \(AMI\)\.

**To add job details**

1. On the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home), in the **Name your job** section, provide a name for your job in the **Job name** box\.

1. In the **Choose your Snow device** section, choose the Snowball Edge device type that you want to use\.
**Note**  
Some of these options might not be available in certain AWS Regions\.

**AWS Snowball Edge device options**
   + **Snowball Edge Storage Optimized** – 80 TB storage \(HDD\), 32 GB memory, 24 vCPUs 
   + **Snowball Edge Compute Optimized** – 39\.5 TB storage \(HDD\), 7\.68 TB storage \(SSD\), 208 GB memory, 52 vCPUs 
   + **Snowball Edge Compute Optimized with GPU** – 39\.5 TB storage, 7\.68 TB storage \(SSD\), 208 GB memory, 52 vCPUs with GPU   
![\[Screenshot of the device options and configurations.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/sbe-devices.png)
**Note**  
When you're ordering clustered jobs, only the Snowball Edge device type is supported\.
The device capacity is optional\.
The availability of device types differs by AWS Region\. For more information about Region availability, see [AWS Regional Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/?p=ngi&loc=4)\.

1. In the **Choose your data transfer mechanism** section, choose either **S3** or **NFS**\.
**Warning**  
The NFS transfer type does not support the S3 interface\. If you proceed with the NFS Transfer Type, you must mount the NFS share to transfer objects\. Using the AWS CLI to transfer objects will fail\. See [Using NFS for Offline Data Transfer](https://docs.aws.amazon.com/snowball/latest/developer-guide/shared-using-nfs.html) for more information\.

1. Depending on the transfer mechanism that you chose, do one of the following:
   + In the **Choose your S3 storage** section, choose to create a new Amazon S3 bucket, or choose the S3 bucket that you want to use in the **Bucket name** list\. You can include additional S3 buckets\. These buckets appear on your device as local S3 buckets\.
   + In the **Choose your NFS storage** section, choose to create a new S3 bucket, or choose the S3 bucket that you want to use in the **Bucket name** list\. You can include additional S3 buckets\. These buckets appear on your device as Network File System \(NFS\) mount points\.

1. In the **Compute using EC2 instances \- *optional*** section, choose **EC2 AMI name**\. This option enables you to use compute Amazon EC2 instances in a cluster\. It loads your Snowball Edge device with Amazon EC2 AMIs, and enables your device to function as a mobile data center\. 

   For more information, see [Using Amazon EC2 Compute Instances](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-ec2.html)\.

   This feature incurs additional charges\. For more information, see [AWS Snowball Edge Pricing\.](https://aws.amazon.com/snowball/pricing/)

1.  Choose an AMI in the **Source AMI name** list\. Or, search for an AMI in the **Source AMI name** box and choose **Next**\.