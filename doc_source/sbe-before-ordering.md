# Before You Order a Snowball Edge device<a name="sbe-before-ordering"></a>

AWS Snowball Edge is a region\-specific service\. So before you plan your job, be sure that the service is available in your AWS Region\. Ensure that your location and Amazon S3 bucket are within the same AWS Region or the same country because it will impact your ability to order the device\. 

To use Amazon S3 compatible storage on Snow Family devices with compute optimized devices for local edge compute and storage jobs, you need to provision S3 capacity on the device or devices when you order\. Amazon S3 compatible storage on Snow Family devices supports local bucket management, so you can create S3 buckets on the device or cluster after you receive the device or devices\.

As part of the order process, you create an AWS Identity and Access Management \(IAM\) role and an AWS Key Management Service \(AWS KMS\) key\. The KMS key is used to encrypt the unlock code for your job\. For more information about creating IAM roles and KMS keys, see [Creating an AWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html)\.

**Topics**
+ [Questions about the Local Environment](#sbe-before-questions)
+ [Working with Files That Contain Special Characters](#sbe-before-data-format)
+ [Using Amazon EC2 on Snowball](#before-ec2)
+ [Using Amazon S3 on Snowball Edge](#before-s3)
+ [Snowball Edge Clusters](#sbe-ordering-cluster)

## Questions about the Local Environment<a name="sbe-before-questions"></a>

Understanding your dataset and how the local environment is set up will help you complete your data transfer\. Consider the following before placing your order\.

**What data are you transferring?**  
Transferring a large number of small files does not work well with AWS Snowball Edge\. This is because Snowball Edge encrypts each individual object\. Small files include files under 1 MB in size\. We recommend that you zip them up before transferring them onto the AWS Snowball Edge device\. We also recommend that you have no more than 500,000 files or directories within each directory\.

**Will the data be accessed during the transfer?**  
It is important to have a static dataset, \(that is, no users or systems are accessing the data during transfer\)\. If not, the file transfer can fail due to a checksum mismatch\. The files won't be transferred and the files will be marked as `Failed`\.   
We recommend that if you are using the file interface, you only use one method of transferring data to the AWS Snowball Edge\. Copying data with both the file interface and the Amazon S3 adapter can result in read/write conflicts\.   
To prevent corrupting your data, don't disconnect an AWS Snowball Edge device or change its network settings while transferring data\. Files should be in a static state while being written to the device\. Files that are modified while they are being written to the device can result in read/write conflicts\.

**Will the network support AWS Snowball data transfer?**  
Snowball Edge supports the *RJ45*, *SFP\+*, or *QSFP\+* networking adapters\. Verify that your switch is a gigabit switch\. Depending on the brand of switch, it might say **gigabit** or **10/100/1000**\. Snowball Edge devices do not support a megabit switch, or 10/100 switch\.

## Working with Files That Contain Special Characters<a name="sbe-before-data-format"></a>

It's important to note that if your objects contain special characters, you might encounter errors\. Although Amazon S3 allows special characters, we highly recommend that you avoid the following characters:
+ Backslash \("\\"\)
+ Left curly brace \("\{"\)
+ Right curly brace \("\}"\)
+ Left square bracket \("\["\)
+ Right square bracket \("\]"\)
+ 'Less Than' symbol \("<"\)
+ 'Greater Than' symbol \(">"\)
+ Non\-printable ASCII characters \(128–255 decimal characters\)
+ Caret \("^"\)
+ Percent character \("%"\)
+ Grave accent / back tick \("`"\)
+ Quotation marks
+ Tilde \("\~"\)
+ 'Pound' character \("\#"\)
+ Vertical bar / pipe \("\|"\)

If your files have one or more of these characters, rename them before you copy them to the AWS Snowball Edge device\. Windows users who have spaces in their file names should be careful when copying individual objects or running a recursive command\. Surround individual objects that have spacing in the name with quotation marks\. The following are examples of such files\. 


| Operating system | File name: test file\.txt | 
| --- | --- | 
|  Windows  |  `“C:\Users\<username>\desktop\test file.txt”`  | 
|  iOS  |  `/Users/<username>/test\ file.txt`  | 
|  Linux  |  `/home/<username>/test\ file.txt`  | 

**Note**  
The only object metadata that is transferred is the object name and size\. If you want additional metadata to be copied, you can use the file interface or other tools to copy the data to Amazon S3\.

## Using Amazon EC2 on Snowball<a name="before-ec2"></a>

This section provides an overview of using Amazon EC2 compute instances on an AWS Snowball Edge device\. It includes conceptual information, procedures, and examples\.

**Note**  
These Amazon EC2 features on AWS Snowball are not supported in the Asia Pacific \(Mumbai\) and Europe \(Paris\) AWS Regions\.

You can run Amazon EC2 compute instances hosted on an AWS Snowball Edge with the `sbe1`, `sbe-c`, and `sbe-g` instance types:
+ The `sbe1` instance type works on devices with the Snowball Edge Storage Optimized option\.
+ The `sbe-c` instance type works on devices with the Snowball Edge Compute Optimized option\.
+ Both the `sbe-c` and `sbe-g` instance types work on devices with the Snowball Edge Compute Optimized with GPU option\.

All the compute instance types supported on Snowball Edge device options are unique to AWS Snowball Edge devices\. Like their cloud\-based counterparts, these instances require Amazon Machine Images \(AMIs\) to launch\. You choose the AMI for an instance before you create your Snowball Edge job\.

To use a compute instance on a Snowball Edge, create a job and specify your AMIs\. You can do this using the AWS Snowball Management Console, the AWS Command Line Interface \(AWS CLI\), or one of the AWS SDKs\. Typically, to use your instances, there are some housekeeping prerequisites that you must perform before creating your job\.

After your device arrives, you can start managing your AMIs and instances\. You can manage your compute instances on a Snowball Edge through an Amazon EC2\-compatible endpoint\. This type of endpoint supports many of the Amazon EC2 CLI commands and actions for the AWS SDKs\. You can't use the AWS Management Console on the Snowball Edge to manage your AMIs and compute instances\.

When you're done with your device, return it to AWS\. If the device was used in an import job, the data transferred using the Amazon S3 adapter or the file interface is imported into Amazon S3\. Otherwise, we perform a complete erasure of the device when it is returned to AWS\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.

**Important**  
Data in compute instances running on a Snowball Edge isn't imported into AWS\.

### Pricing for Compute Instances on Snowball Edge<a name="pricing-for-ec2-edge"></a>

There are additional costs associated with using compute instances\. For more information, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

### Prerequisites<a name="ec2-edge-prereqs"></a>

Before creating your job, keep the following information in mind:
+ Before you add any AMIs to your job request, make sure that you have created an AMI that is supported in your AWS account\. Currently, supported AMIs are based on the [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW) and [Ubuntu 16\.04 LTS \- Xenial \(HVM\)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O) images\. You can get these images from the [AWS Marketplace](https://aws.amazon.com/marketplace) website\.
+ All AMIs must be based on Amazon Elastic Block Store \(Amazon EBS\), with a single volume\.
+ If you are connecting to a compute instance running on a Snowball Edge, you must use Secure Shell \(SSH\)\. To do so, you first add the key pair\. For more information, see [Configuring an AMI to Use SSH to Connect to Compute Instances Launched on the Device](create-ec2-edge-job.md#important-create-ec2-edge-job)\.

### Creating a Linux AMI from an Instance<a name="ec2-ami-export"></a>

You can create an AMI using the AWS Management Console or the command line\. Start with an existing AMI, launch an instance, customize it, create a new AMI from it, and finally, launch an instance of your new AMI\.

**To create an AMI from an instance using the console**

1. Select an appropriate EBS\-backed AMI as a starting point for your new AMI, and configure it as needed before launch\. For more information, see [Launching an instance using the Launch Instance Wizard](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html) in the *Amazon EC2 User Guide for Linux Instances*\.

1. Choose **Launch** to launch an instance of the EBS\-backed AMI that you selected\. Accept the default values as you step through the wizard\. For more information, see [Launching an instance using the Launch Instance Wizard](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html)\.

1. While the instance is running, connect to it\. You can perform the following actions on your instance to customize it for your needs:
   + Install software and applications\.
   + Copy data\.
   + Reduce start time by deleting temporary files, defragmenting your hard drive, and zeroing out free space\.
   + Attach additional Amazon EBS volumes\.

1. \(Optional\) Create snapshots of all the volumes attached to your instance\. For more information about creating snapshots, see [Creating Amazon EBS snapshots](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-snapshot.html) in the *Amazon EC2 User Guide for Linux Instances*\.

1. In the navigation pane, choose **Instances**, and choose your instance\. Choose **Actions**, choose **Image**, and then choose **Create image**\.
**Tip**  
If this option isn't available, your instance isn't an Amazon EBS\-backed instance\.

1. In the **Create Image** dialog box, specify the following information, and then choose **Create image**\.
   + **Image name** \- A unique name for the image\.
   + **Image description** \- An optional description of the image, up to 255 characters\.
   + **No reboot** \- This option is not selected by default\. Amazon EC2 shuts down the instance, takes snapshots of any attached volumes, creates and registers the AMI, and then reboots the instance\. Select **No reboot** to avoid having your instance shut down\.
**Warning**  
If you select **No reboot**, we can't guarantee the file system integrity of the created image\.
   + **Instance Volumes** \- The fields in this section enable you to modify the root volume, and add more Amazon EBS and instance store volumes\. For information about each field, pause on the **i** icon next to each field to display field tooltips\. Some important points are listed following:
     + To change the size of the root volume, locate **Root** in the **Volume Type** column\. For **Size \(GiB\)**, enter the required value\.
     + If you select **Delete on Termination**, when you terminate the instance created from this AMI, the Amazon EBS volume is deleted\. If you clear **Delete on Termination**, when you terminate the instance, the Amazon EBS volume is not deleted\. For more information, see [Preserving Amazon EBS volumes on instance termination](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html#preserving-volumes-on-termination) in the *Amazon EC2 User Guide for Linux Instances*\.
     + To add an Amazon EBS volume, choose **Add New Volume** \(which adds a new row\)\. For **Volume Type**, choose **EBS**, and fill in the fields in the row\. When you launch an instance from your new AMI, additional volumes are automatically attached to the instance\. Empty volumes must be formatted and mounted\. Volumes based on a snapshot must be mounted\.
     + To add an instance store volume, see [Adding instance store volumes to an AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/add-instance-store-volumes.html#adding-instance-storage-ami) in the *Amazon EC2 User Guide for Linux Instances*\. When you launch an instance from your new AMI, additional volumes are automatically initialized and mounted\. These volumes don't contain data from the instance store volumes of the running instance on which you based your AMI\.

1. To view the status of your AMI while it is being created, in the navigation pane, choose **AMIs**\. Initially, the status is pending but should change to available after a few minutes\.

   \(Optional\) To view the snapshot that was created for the new AMI, choose **Snapshots**\. When you launch an instance from this AMI, we use this snapshot to create its root device volume\.

1. Launch an instance from your new AMI\. For more information, see [Launching an instance using the Launch Instance Wizard](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html) in the *Amazon EC2 User Guide for Linux Instances*\.

1. The new running instance contains all of the customizations that you applied in previous steps\.

#### To Create an AMI from an Instance Using the Command Line<a name="ec2-ami-export-cli"></a>

You can use one of the following commands\. For more information about these command line interfaces, see [Accessing Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html#access-ec2) in the *Amazon EC2 User Guide for Linux Instances*\.
+ [create\-image](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-image.html) \(AWS CLI\)
+ [New\-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/New-EC2Image.html) \(AWS Tools for Windows PowerShell\)

### Creating a Linux AMI from a Snapshot<a name="ec2-ami-export"></a>

If you have a snapshot of the root device volume of an instance, you can create an AMI from this snapshot using the AWS Management Console or the command line\.

**To create an AMI from a snapshot using the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Elastic Block Store**, choose **Snapshots**\.

1. Choose the snapshot, choose **Actions**, and then choose **Create image**\.

1. In the **Create image from EBS snapshot** dialog box, complete the fields to create your AMI\. Then choose **Create**\. If you're re\-creating a parent instance, choose the same options as the parent instance\.
   + **Architecture** – Choose **i386** for 32\-bit or **x86\_64** for 64\-bit\.
   + **Root device name** – Enter the appropriate name for the root volume\. For more information, see [Device naming on Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/device_naming.html) in the *Amazon EC2 User Guide for Linux Instances*\.
   + **Virtualization type** – Choose whether instances launched from this AMI use paravirtual \(PV\) or hardware virtual machine \(HVM\) virtualization\. For more information, see [Linux AMI virtualization types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/virtualization_types.html)\.
   + \(PV virtualization type only\) **Kernel ID** and **RAM disk ID** – Choose the AKI and ARI from the lists\. If you choose the default AKI, or you don't choose an AKI, you must specify an AKI every time you launch an instance using this AMI\. In addition, your instance might fail the health checks if the default AKI is incompatible with the instance\.
   + \(Optional\) **Block Device Mappings** – Add volumes or expand the default size of the root volume for the AMI\. For more information about resizing the file system on your instance for a larger volume, see [Extending a Linux File system after resizing a volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html) in the *Amazon EC2 User Guide for Linux Instances*\.

#### To Create an AMI from a Snapshot Using the Command Line<a name="ec2-snapshot-export-cli"></a>

To create an AMI from a snapshot, you can use one of the following commands\. For more information about these command line interfaces, see [Accessing Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html#access-ec2) in the *Amazon EC2 User Guide for Linux Instances*\.
+ [register\-image](https://docs.aws.amazon.com/cli/latest/reference/ec2/register-image.html) \(AWS CLI\)
+ [Register\-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/Register-EC2Image.html) \(AWS Tools for Windows PowerShell\)

## Using Amazon S3 on Snowball Edge<a name="before-s3"></a>

As part of the order process, you are asked to create an AWS Identity and Access Management \(IAM\) role and AWS Key Management Service \(AWS KMS\) key\. The KMS key is used for encrypting the data at rest on the Snowball Edge device\. For more information about creating IAM roles and KMS keys, see [Creating an AWSAWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html)\.

**Important**  
If the imported data must be encrypted in the S3 bucket using Server\-Side Encryption with keys stored in AWS KMS \(SSE\-KMS\), see [Amazon S3 encryption with AWS KMS](#s3-kms-encryption)\.  
If the imported data must be encrypted in the S3 bucket using Server\-Side Encryption with Amazon S3 managed keys \(SSE\-S3\), see [Amazon S3 encryption with server\-side encryption](#s3-sse-encryption)\.

### How import works<a name="s3-import"></a>

Each import job uses a single Snowball Edge device\. After you create a job, we ship a Snowball Edge device to you\. When it arrives, you connect the Snowball Edge device to your network and transfer the data that you want to import to Amazon S3 onto that Snowball Edge\. When you’re done transferring data, ship the Snowball Edge back to AWS\. We then import your data into Amazon S3\.

**Important**  
Snowball Edge cannot write to buckets if you have turned on S3 Object Lock\. We also cannot write to your bucket if IAM policies on the bucket prevent writing to the bucket\.

### How export works<a name="s3-export"></a>

Each export job can use any number of AWS Snowball Edge devices\. After you create a job, a listing operation starts in Amazon S3\. This listing operation splits your job into parts\. Each job part has exactly one device associated with it\. After your job parts are created, your first job part enters the **Preparing** Snowball status\.

**Note**  
The listing operation to split your job into parts is a function of Amazon S3, and you are billed the same as Amazon S3 operation\.

 We then start exporting your data onto a device\. Typically, exporting data takes one business day\. However, this process can take longer\. When the export is done, AWS gets the device ready for your regional carrier to pick up\.

When the device arrives at your site, you connect it to your network and transfer the data that you want to import into Amazon S3 onto the device\. When you’re done transferring the data, ship the device back to AWS\. When we receive the returned device, we erase it completely\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\. 

This step marks the completion of that particular job part\. If there are more job parts, the next job part now is prepared for shipping\.

**Important**  
Snowball Edge is unable to export files that are in S3 Glacier storage class\. These objects must be restored before we can export the files\. If we encounter files in S3 Glacier storage class, we contact you to let you know, but this might add delays to your export job\.

### Using Amazon S3 compatible storage on Snow Family devices for edge compute and storage jobs<a name="s3-on-snow-before"></a>

Amazon S3 compatible storage on Snow Family devices delivers secure object storage with increased resiliency, scale, and expanded Amazon S3 API feature\-set to the rugged, mobile edge, and disconnected environments\. Amazon S3 compatible storage on Snow Family devices enables customers to store data and run highly available applications on Snow Family devices for edge compute use case\.

Amazon S3 compatible storage on Snow Family devices can be deployed in standalone configuration or cluster configuration\. In standalone configuration you can provision usable S3 capacity on device and the balance will be available as block storage\. In cluster setup all data disk capacity will be utilzied for S3 storage\. Depending on the size of cluster, S3 service is designed to sustain device fault tolerance of 1 or 2 devices\. For more information about cluster fault tolerance, see [Clustering overview](ClusterOverview.md)\. 

To set up and use Amazon S3 compatible storage on Snow Family devices see [Amazon S3 compatible storage on Snow Family devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/s3compatible-on-snow.html) in this guide\.

### Amazon S3 encryption with AWS KMS<a name="s3-kms-encryption"></a>

You can use the default AWS managed or customer managed encryption keys to protect your data when importing or exporting data\.

#### Using Amazon S3 default bucket encryption with AWS KMS managed keys<a name="kms-aws-managed-keys"></a>

**To enable AWS managed encryption with AWS KMS**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the Amazon S3 bucket that you want to encrypt\.

1. In the wizard that appears on the right side, choose **Properties**\.

1. In the **Default encryption** box, choose ** Disabled** \(this option is grayed out\) to enable default encryption\.

1. Choose **AWS\-KMS** as the encryption method, and then choose the KMS key that you want to use\. This key is used to encrypt objects that are PUT into the bucket\.

1. Choose **Save**\.

After the Snowball Edge job is created, and before the data is imported, add a statement to the existing IAM role policy\. This is the role you created during the ordering process\. Depending on the job type, the default role name looks similar to `Snowball-import-s3-only-role` or `Snowball-export-s3-only-role`\.

The following are examples of such a statement\.

**For importing data**

If you use server\-side encryption with AWS KMS managed keys \(SSE\-KMS\) to encrypt the Amazon S3 buckets associated with your import job, you also need to add the following statement to your IAM role\.

**Example Snowball import IAM role**  

```
{
    "Effect": "Allow",
    "Action": [
        "kms: GenerateDataKey",
	"kms: Decrypt"
    ],
    "Resource":"arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

**For exporting data**

If you use server\-side encryption with AWS KMS managed keys to encrypt the Amazon S3 buckets associated with your export job, you also must add the following statement to your IAM role\.

**Example Snowball export IAM role**  

```
{
    "Effect": "Allow",
    "Action": [
        "kms:Decrypt"
    ],
    "Resource":"arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

#### Using S3 default bucket encryption with AWS KMS customer keys<a name="kms-customer-keys"></a>

You can use the default Amazon S3 bucket encryption with your own KMS keys to protect data you are importing and exporting\.

**For importing data**

**To enable customer managed encryption with AWS KMS**

1. Sign in to the AWS Management Console and open the AWS Key Management Service \(AWS KMS\) console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. In the left navigation pane, choose **Customer managed keys**, and then choose the KMS key associated with the buckets that you want to use\.

1. Expand **Key Policy** if it is not already expanded\. 

1. In the **Key Users** section, choose **Add** and search for the IAM role\. Choose the IAM role, and then choose **Add**\.

1. Alternatively, you can choose **Switch to Policy view** to display the key policy document and add a statement to the key policy\. The following is an example of the policy\.

**Example of a policy for the AWS KMS customer managed key**  

```
{
  "Sid": "Allow use of the key",
  "Effect": "Allow",
  "Principal": {
    "AWS": [
      "arn:aws:iam::111122223333:role/snowball-import-s3-only-role"
    ]
  },
  "Action": [
    "kms:Decrypt",
    "kms:GenerateDataKey"
  ],
  "Resource": "*"
}
```
After this policy has been added to the AWS KMS customer managed key, it is also needed to update the IAM role associated with the Snowball job\. By default, the role is `snowball-import-s3-only-role`\.

**Example of the Snowball import IAM role**  

```
{
  "Effect": "Allow",
  "Action": [
    "kms: GenerateDataKey",
    "kms: Decrypt"
  ],
  "Resource": "arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

For more information, see [Using Identity\-Based Policies \(IAM Policies\) for AWS Snowball](access-control-managing-permissions.md)\.

The KMS key that is being used looks like the following: 

`“Resource”:“arn:aws:kms:region:AccoundID:key/*”`

**For exporting data**

**Example of a policy for the AWS KMS customer managed key**  

```
{
  "Sid": "Allow use of the key",
  "Effect": "Allow",
  "Principal": {
    "AWS": [
      "arn:aws:iam::111122223333:role/snowball-import-s3-only-role"
    ]
  },
  "Action": [
    "kms:Decrypt",
    "kms:GenerateDataKey"
  ],
  "Resource": "*"
}
```

After this policy has been added to the AWS KMS customer managed key, it is also needed to update the IAM role associated with the Snowball job\. By default, the role looks like the following:

 `snowball-export-s3-only-role`

**Example of the Snowball export IAM role**  

```
{
  "Effect": "Allow",
  "Action": [
    "kms: GenerateDataKey",
    "kms: Decrypt"
  ],
  "Resource": "arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

After this policy has been added to the AWS KMS customer managed key, it is also needed to update the IAM role associated with the Snowball job\. By default, the role is `snowball-export-s3-only-role`\.

### Amazon S3 encryption with server\-side encryption<a name="s3-sse-encryption"></a>

AWS Snowball supports server\-side encryption with Amazon S3 managed encryption keys \(SSE\-S3\)\. Server\-side encryption is about protecting data at rest, and SSE\-S3 has strong, multifactor encryption to protect your data at rest in Amazon S3\. For more information about SSE\-S3, see [Protecting Data Using Server\-Side Encryption with Amazon S3\-Managed Encryption Keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the * Amazon Simple Storage Service User Guide*\.

**Note**  
Currently, AWS Snowball doesn't support server\-side encryption with customer\-provided keys \(SSE\-C\)\. However, you might want to use that SSE type to protect data that has been imported, or you might already use it on data you want to export\. In these cases, keep the following in mind:  
**Import** – If you want to use SSE\-C to encrypt the objects that you've imported into S3, copy those objects into another bucket that has SSE\-KMS or SSE\-S3 encryption established as a part of that bucket's bucket policy\.
**Export** – If you want to export objects that are encrypted with SSE\-C, first copy those objects to another bucket that either has no server\-side encryption, or has SSE\-KMS or SSE\-S3 specified in that bucket's bucket policy\.

## Snowball Edge Clusters<a name="sbe-ordering-cluster"></a>

A *cluster* is a logical grouping of AWS Snowball Edge devices, in groups of 3 to 16 devices\. A cluster is created with a single job\. A cluster offers increased durability and storage capacity\. This section provides information about Snowball Edge clusters with Amazon S3 compatible storage on Snow Family devices\.

For the AWS Snowball service, a cluster is a collective of Snowball Edge devices, used as a single logical unit, for local storage and compute purposes\.

A cluster offers these primary benefits over a standalone Snowball Edge used for local storage and compute purposes:
+ **Increased durability** – The data stored in a cluster of Snowball Edge devices has increased data durability\. In addition, the data on the cluster remains as safe and viable even during possible Snowball Edge outages in the cluster\. Clusters of 3 or 4 nodes can withstand the loss of 1 node and clusters of 5 to 16 nodes can withstand loss of up to 2 nodes before the data in the cluster becomes a concern\. You can also add or replace nodes\.
+ **Increased storage** – For compute\-optimized Snowball Edge devices with Amazon S3 compatible storage on Snow Family devices, the total available storage is up to 31 terabytes of data per node in a cluster, depending on the device used\. Thus, in a sixteen\-node cluster, there are up to 501 terabytes of available storage space\. In contrast, there are about 39\.5 terabytes of available storage space in a standalone Snowball Edge compute\-optimized device\. For more information about cluster capacity, see [Clustering overview](ClusterOverview.md)\.

A cluster of Snowball Edge devices is made of leaderless nodes\. Any node can write data to and read data from the entire cluster, and all nodes can perform the behind\-the\-scenes management of the cluster\.

### Snowball Edge cluster quorums<a name="sbe-clusterquorums"></a>

A *quorum* represents the minimum number of Snowball Edge devices in a cluster that must be communicating with each other to maintain some level of operation\. For more information about cluster fault tolerance, see [Clustering overview](ClusterOverview.md)\.

Suppose that you upload your data to a cluster of Snowball Edge devices\. With all devices healthy, you have a *read/write quorum* for your cluster\. If one or two nodes goes offline, you reduce the operational capacity of the cluster, but you can still read and write to the cluster\.

Finally, if a third node goes offline and quorum is breached, the cluster is offline and the data in the cluster becomes unavailable\. In this case, you might be able fix it, but the data could be permanently lost depending on the severity of the event\. If it is a temporary external power event, and you can bring the three Snowball Edge devices back online and unlock all the nodes in the cluster, your data becomes available again\.

**Important**  
As soon as one cluster node is unhealthy or unrecoverable, contact AWS Support for a replacement device\.

You can determine the quorum state of your cluster by determining your node's lock state and network reachability\. The `snowballEdge describe-cluster` command reports back the lock and network reachability state for every node in an unlocked cluster\. Ensuring that the devices in your cluster are healthy and connected is an administrative responsibility that you take on when you create the cluster job\. For more information about the different client commands, see [Commands for the Snowball Edge Client](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html)\.

### Considerations for Cluster Jobs for AWS Snowball Edge<a name="sbe-clusterconsiderations"></a>

Keep the following considerations in mind when planning to use a cluster of Snowball Edge devices:
+ We recommend that you have a redundant power supply to reduce potential performance and stability issues for your cluster\.
+ Like standalone local storage and compute jobs, the data stored in a cluster can't be imported into Amazon S3 without ordering additional devices as a part of separate import jobs\. If you order these devices, you can transfer the data from the cluster to the devices and import the data when you return the devices for the import jobs\.
+ To get data onto a cluster from Amazon S3, create a separate export job and copy the data from the devices of the export job onto the cluster\.
+ You can use the console, the AWS CLI, or AWS SDK to create a cluster job\.
+ Cluster nodes have node IDs\. A *node ID* is the same as the job ID for a device that you can get from the console, the AWS CLI, the AWS SDKs, or the Snowball Edge client\. You can use node IDs to remove old nodes from clusters\. You can get a list of node IDs by using the `snowballEdge describe-device` command on an unlocked device or the `describe-cluster` on an unlocked cluster\.
+ The lifespan of a cluster is limited by the security certificate granted to the cluster devices when the cluster is provisioned\.
+ When AWS receives a returned device that was part of a cluster, we perform a complete erasure of the device\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.