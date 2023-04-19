# Step 2: Choose your compute and storage options<a name="compute-storage"></a>

Choose the hardware specifications for your Snow Family device and which of your Amazon EC2 instances and Amazon S3 buckets to include on it\. You can also order a cluster of Snowball Edge devices to increase durability and redundancy of storage\.

**To choose your device's compute and storage options**

1. In the **Snow devices** section, choose the Snow Family device\. To learn about Snow Family device differences, see [AWS Snowball Edge Device Differences](https://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html) and [AWS Snowcone Device Specifications](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/snowcone-spec-requirements.html)\.
**Note**  
Some device options might not be available in certain AWS Regions\.  
![\[Screenshot of the device options and configurations.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/sbe-devices.png)

1. In the **Compute using EC2 instances \- optional** section, choose Amazon EC2 AMIs from your account to include on the device\. Or, in the search field, enter all or part the name of an AMI to filter the list of available AMIs on your entry, then choose the AMI\.

   For more information, see [Adding an AMI When Ordering Your Device](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-ami.html#add-ami-order) in this guide\.

   This feature incurs additional charges\. For more information, see [AWS Snowball Edge Pricing\.](https://aws.amazon.com/snowball/pricing/)

1. In the **Select the storage type** section, choose either **S3** or **NFS**\.
**Warning**  
The NFS transfer type doesn't support the S3 interface\. If you proceed with the NFS Transfer Type, you must mount the NFS share to transfer objects\. Using the AWS CLI to transfer objects will fail\. See [Using NFS for Offline Data Transfer](https://docs.aws.amazon.com/snowball/latest/developer-guide/shared-using-nfs.html) for more information\.

1. To order a cluster of devices, choose **Order a cluster instead of a single device**, then name the cluster and enter the number of devices in it\. AWS will provide you with this quantity of devices, configured for scalable storage and compute redundancy\.
**Note**  
Only Snowball Edge devices are available for clusters\. If you chose a different type of device in **Snow devices**, the cluster option isn't available\.

1. Depending on the transfer mechanism that you chose, do one of the following:
   + In the **Choose your S3 storage** section, choose to create a new Amazon S3 bucket, or choose the S3 bucket that you want to use in the **Bucket name** list\. You can include additional S3 buckets\. These buckets appear on your device as local S3 buckets\.
   + In the **Choose your NFS storage** section, choose to create a new S3 bucket, or choose the S3 bucket that you want to use in the **Bucket name** list\. You can include additional S3 buckets\. All S3 buckets must belong to the AWS account used to order the device\. These buckets appear on your device as Network File System \(NFS\) mount points\.

1. Choose the **Next** button\.