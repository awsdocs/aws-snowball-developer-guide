# What is AWS Snowball Edge?<a name="whatisedge"></a>

AWS Snowball Edge is a type of Snowball device with on\-board storage and compute power for select AWS capabilities\. Snowball Edge can do local processing and edge\-computing workloads in addition to transferring data between your local environment and the AWS Cloud\.

Each Snowball Edge device can transport data at speeds faster than the internet\. This transport is done by shipping the data in the appliances through a regional carrier\. The appliances are rugged, complete with E Ink shipping labels\. 

Snowball Edge devices have four options for device configurations—*Storage Optimized*, *Compute Optimized*, *Compute Optimized with GPU*, and *Import virtual tapes into AWS Storage Gateway*\. When this guide refers to Snowball Edge devices, it's referring to all options of the device\. When specific information applies only to one or more optional configurations of devices \(such as how the Snowball Edge with GPU has an on\-board GPU\), it is called out specifically\. For more information, see [Snowball Edge Device Options](device-differences.md#device-options)\.

**Topics**
+ [AWS Snowball Edge features](#edge-feature-overview)
+ [Prerequisites for using Snow Family devices](#snowball-prereqs)
+ [Services related to AWS Snowball Edge](#edge-related)
+ [Accessing the service](#accessing-service)
+ [Pricing for the AWS Snowball Edge](#pricing-for-edge)
+ [Are you a first\-time AWS Snowball user?](#first-time-user)
+ [AWS Snowball Edge Device Differences](device-differences.md)

## AWS Snowball Edge features<a name="edge-feature-overview"></a>

Snowball Edge devices have the following features:
+ Large amounts of storage capacity or compute functionality for devices\. This depends on the options you choose when you create your job\.
+ Network adapters with transfer speeds of up to 100 Gbit/second\.
+ Encryption is enforced, protecting your data at rest and in physical transit\.
+ You can import or export data between your local environments and Amazon S3, and physically transport the data with one or more devices without using the internet\.
+ Snowball Edge devices are their own rugged box\. The built\-in E Ink display changes to show your shipping label when the device is ready to ship\.
+ Snowball Edge devices come with an on\-board LCD display that can be used to manage network connections and get service status information\.
+ You can cluster Snowball Edge devices for local storage and compute jobs to achieve data durability across 3 to 16 devices and locally grow or shrink storage on demand\.
+ You can use the file interface to read and write data to an AWS Snowball Edge device through a file share or Network File System \(NFS\) mount point\.
+ You can use Amazon EKS Anywhere on Snowball Edge devices for Kubernetes workloads\.
+ Snowball Edge devices have Amazon S3 and Amazon EC2 compatible endpoints available, enabling programmatic use cases\.
+ Snowball Edge devices support the new `sbe1`, `sbe-c`, and `sbe-g` instance types, which you can use to run compute instances on the device using Amazon Machine Images \(AMIs\)\.
+ Snowball Edge supports these data transfer protocols for data migration:
  + NFSv3
  + NFSv4
  + NFSv4\.1
  + Amazon S3 over HTTP or HTTPS \(via API compatible with AWS CLI version 1\.16\.14 and earlier\)

## Prerequisites for using Snow Family devices<a name="snowball-prereqs"></a>

### Sign up for an AWS account<a name="sign-up-for-aws"></a>

If you do not have an AWS account, complete the following steps to create one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

AWS sends you a confirmation email after the sign\-up process is complete\. At any time, you can view your current account activity and manage your account by going to [https://aws\.amazon\.com/](https://aws.amazon.com/) and choosing **My Account**\.

### Create an administrative user<a name="create-an-admin"></a>

After you sign up for an AWS account, create an administrative user so that you don't use the root user for everyday tasks\.

**Secure your AWS account root user**

1.  Sign in to the [AWS Management Console](https://console.aws.amazon.com/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.

   For help signing in by using root user, see [Signing in as the root user](https://docs.aws.amazon.com/signin/latest/userguide/console-sign-in-tutorials.html#introduction-to-root-user-sign-in-tutorial) in the *AWS Sign\-In User Guide*\.

1. Turn on multi\-factor authentication \(MFA\) for your root user\.

   For instructions, see [Enable a virtual MFA device for your AWS account root user \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html#enable-virt-mfa-for-root) in the *IAM User Guide*\.

**Create an administrative user**
+ For your daily administrative tasks, grant administrative access to an administrative user in AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\.

  For instructions, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide*\.

**Sign in as the administrative user**
+ To sign in with your IAM Identity Center user, use the sign\-in URL that was sent to your email address when you created the IAM Identity Center user\.

  For help signing in using an IAM Identity Center user, see [Signing in to the AWS access portal](https://docs.aws.amazon.com/signin/latest/userguide/iam-id-center-sign-in-tutorial.html) in the *AWS Sign\-In User Guide*\.

### Prerequisites for using Amazon S3 adapter on Snow Family devices for import and export jobs<a name="s3-prereqs"></a>

You will use S3 adapter on Snow Family devices when you are using the devices to move data from on\-premises data sources to the cloud or from the cloud to on\-premises data storage\.

**Note**  
You must select S3 adapter on Snow when you order devices\. See [Step 2: Choose your compute and storage options](https://docs.aws.amazon.com/snowball/latest/developer-guide/compute-storage.html) in this guide\.

The Amazon S3 bucket associated with the job must use the Amazon S3 standard storage class\. Before creating your first job, keep the following in mind\.

For jobs that import data into Amazon S3, follow these steps:
+ Confirm that the files and folders to transfer are named according to the [object key naming guidelines](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-key-guidelines) for Amazon S3\. Any files or folders with names that don't meet these guidelines aren't imported into Amazon S3\.
+ Plan what data you want to import into Amazon S3\. For more information, see [Planning Your Large Transfer](copy-general-planning.md)\.

Before exporting data from Amazon S3, follow these steps:
+ Understand what data is exported when you create your job\. For more information, see [Using Export Ranges](exporttype.md#ranges)\.
+ For any files with a colon \(`:`\) in the file name, change the file names in Amazon S3 before you create the export job to get these files\. Files with a colon in the file name fail export to Microsoft Windows Server\. 

### Prerequisites for using Amazon S3 compatible storage on Snow Family devices<a name="s3-on-snowprereqs"></a>

You will use Amazon S3 compatible storage on Snow Family devices when you are storing data on the device at your edge location and using the data for local compute operations\. To migrate data to or from AWS, set up an export or import job and use the Amazon S3 adapter\. 

When ordering a Snow device for local compute and storage with Amazon S3 compatible storage, keep the following in mind\.
+ You will provision Amazon S3 storage capacity when you order the device\. So consider your storage need before ordering a device\.
+ You can create Amazon S3 buckets on the device after you receive it rather than while ordering a Snow Family device\.
+ You will need to download the latest version of the AWS CLI, Snowball Edge client, or AWS OpsHub and install it on your computer to use Amazon S3 compatible storage on Snow Family devices\.

### Prerequisites for using compute instances on Snow Family devices<a name="compute-prereqes"></a>

For jobs using compute instances, before you can add any AMIs to your job, you must have an AMI in your AWS account and it must be a supported image type\. Currently, supported AMIs are based on these operating systems:
+ [Amazon Linux 2](https://aws.amazon.com/marketplace/pp/B08Q76DLTM)
+ [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW)
+ Ubuntu 16\.04 LTS \- Xenial \(HVM\)
+ [Ubuntu 20\.04 LTS \- Focal](https://aws.amazon.com/marketplace/pp/prodview-iftkyuwv2sjxi)
+ [Ubuntu 22\.04 LTS \- Jammy](https://aws.amazon.com/marketplace/pp/prodview-f2if34z3a4e3i)
+ [Microsoft Windows Server 2012 R2](https://aws.amazon.com/marketplace/pp/prodview-g3y27m7b55tag)
+ [Microsoft Windows Server 2016](https://aws.amazon.com/marketplace/pp/prodview-fsarquezghuic)
+ [Microsoft Windows Server 2019](https://aws.amazon.com/marketplace/pp/prodview-bd6o47htpbnoe)

**Note**  
Ubuntu 16\.04 LTS \- Xenial \(HVM\) images are no longer supported in the AWS Marketplace, but still supported for use on Snowball Edge devices through Amazon EC2 VM Import/Export and running locally in AMIs\.

You can get these images from [AWS Marketplace](https://aws.amazon.com/marketplace)\.

If you're using SSH to connect to the instances running on a Snowball Edge, you must already have the key pair for connecting to the instance\. For more information, see [Amazon EC2 key pairs and Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) in the Amazon EC2 User Guide for Linux Instances\.

For information specific to using compute instances on a device, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.

## Services related to AWS Snowball Edge<a name="edge-related"></a>

You can use an AWS Snowball Edge device with the following related AWS services:
+ **Amazon S3 adapter** — Use for programmatic data transfer in to and out of AWS using the Amazon S3 API for Snowball Edge, which supports a subset of Amazon S3 API operations\. In this role, data is transferred to the Snow device by AWS on your behalf and the device is shipped to you \(for an export job\), or AWS ships an empty Snow device to you and you transfer data from your on\-premises sources to the device and ship it back to AWS \(for an import job\)" 
+ **Amazon S3 compatible storage on Snow Family devices** — Use to support the data needs of compute services such as Amazon EC2, Amazon EKS Anywhere on Snow, and others\. This feature is available on Snowball Edge compute\-optimized devices and provides an expanded Amazon S3 API set and features such as increased resiliency with flexible cluster setup for 3 to 16 nodes, local bucket management, and local notifications\.
+ **Amazon EC2** – Run compute instances on a Snowball Edge device using the Amazon EC2 compatible endpoint, which supports a subset of the Amazon EC2 API operations\. For more information about using Amazon EC2 in AWS, see [Getting started with Amazon EC2 Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/GettingStartedGuide/)\.
+ **Amazon EKS Anywhere on Snow** – Create and operate Kubernetes clusters on Snow Family devices\. See [Using Amazon EKS Anywhere on AWS Snow](using-eksa.md)\.
+ **AWS Lambda powered by AWS IoT Greengrass** – Invoke Lambda functions based on Amazon S3 storage actions made on an AWS Snowball Edge device\. These Lambda functions are associated with an AWS Snowball Edge device during job creation\. For more information about using Lambda, see the [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/)\.
+ **Amazon Elastic Block Store \(Amazon EBS\)** – Provide block\-level storage volumes for use with EC2 instances\. For more information, see [Amazon Elastic Block Store \(Amazon EBS\)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)\.
+ **AWS Identity and Access Management \(IAM\)** – Use this service to securely control access to AWS resources\. For more information, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
+ **AWS Security Token Service \(AWS STS\)** – Request temporary, limited\-privilege credentials for IAM users or for users that you authenticate \(federated users\)\. For more information, see [Temporary security credentials in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html)\.
+ **Amazon EC2 Systems Manager** – Use this service to view and control your infrastructure on AWS\. For more information, see [What is AWS Systems Manager?](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html)

## Accessing the service<a name="accessing-service"></a>

You can either use the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home) or the job management API to create and manage jobs\. For information about the job management API, see [Job Management API Reference for AWS Snowball](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\.

### Accessing an AWS Snowball Edge device<a name="accessing-edge"></a>

After your Snowball Edge device is onsite, you can configure it with an IP address using the LCD screen then you can unlock the device using the Snowball Edge client or AWS OpsHub for Snow Family\. Then, you run can perform data transfer or edge compute tasks\. For more information, see [Using an AWS Snowball Edge Device](using-device.md)\.

## Pricing for the AWS Snowball Edge<a name="pricing-for-edge"></a>

For information about the pricing and fees associated with the service and its devices, see [AWS Snowball Edge Pricing\.](https://aws.amazon.com/snowball/pricing/)

## Are you a first\-time AWS Snowball user?<a name="first-time-user"></a>

If you are a first\-time user of the AWS Snow Family service, we recommend that you read the following sections in order:

1. For information about device types and options, see [AWS Snowball Edge Device Differences](device-differences.md)\.

1. To learn more about the types of jobs, see [Understanding AWS Snowball Edge Jobs](jobs.md)\.

1. For an end\-to\-end overview of how to use an AWS Snowball Edge device, see [How AWS Snowball Edge works](how-it-works.md)\.

1. When you're ready to get started, see [Getting Started](getting-started.md)\.

1. For information about using compute instances on a device, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.