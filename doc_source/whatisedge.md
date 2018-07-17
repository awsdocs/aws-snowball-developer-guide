--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# What Is an AWS Snowball Edge?<a name="whatisedge"></a>

AWS Snowball is a service that accelerates transferring large amounts of data into and out of AWS by using physical storage devices, bypassing the internet\. AWS Snowball Edge is a 100\-TB data transfer device with on\-board storage and compute power for select AWS capabilities\. In addition to transferring data to AWS, Snowball Edge can undertake local processing and edge\-computing workloads\.

Each AWS Snowball device can transport data at speeds faster than the internet\. This transport is done by shipping the data in the appliances through a regional carrier\. The appliances are rugged shipping containers, complete with E Ink shipping labels\. The AWS Snowball Edge device differs from the standard Snowball because it can bring the power of the AWS Cloud to your local environment, with local storage and compute functionality\.

The storage and compute functionality is built\-in\. With an AWS Snowball Edge device, there's no need for a powerful workstation to handle encryption, because all encryption happens on the device itself\.

**Note**  
There are many options for transferring your data into AWS\. The AWS Snowball service is intended for transferring large amounts of data\. If you want to transfer less than 30 terabytes of data, or if you don’t have a local computing or clustering need, using an AWS Snowball Edge device might not be your most economical choice\.

## AWS Snowball Edge Features<a name="edge-feature-overview"></a>

AWS Snowball Edge devices have the following features:
+ Each AWS Snowball Edge device has 100 TB of storage capacity, twice the storage space of the original Snowball device\. 
+ Any one of three network adapters on the AWS Snowball Edge device supports network speeds of over 10 GB/second\.
+ Encryption is enforced, protecting your data at rest and in physical transit\.
+ You can import or export data between your local environments and Amazon S3, physically transporting the data with one or more AWS Snowball Edge devices, completely bypassing the internet\.
+ AWS Snowball Edge devices are their own rugged shipping containers, and the built\-in E Ink display changes to show your shipping label when the device is ready to ship\.
+ Snowball Edge devices come with an on\-board LCD display that can be used to manage network connections, get status, and watch helpful how\-to videos to help you get the most out of your job\.
+ You can cluster Snowball Edge devices for local storage and compute jobs to achieve 99\.999 percent data durability across 5–10 devices, and to locally grow and shrink storage on demand\.
+ You can use the file interface to read and write data to an AWS Snowball Edge device through a file share or Network File System \(NFS\) mount point\.
+ You can write Python\-language Lambda functions and associate them with Amazon S3 buckets when you create an AWS Snowball Edge device job\. Each function triggers whenever there's a local Amazon S3 PUT object action executed on the associated bucket on the appliance\.
+ Amazon S3 and Amazon EC2 compatible endpoints available on each Snowball Edge device\.
+ Snowball Edge devices support the SBE1 instance type, which you can use to run compute instances on the device using Amazon Machine Images \(AMIs\)\.

## Prerequisites for Using Snowball Edge<a name="snowball-prereqs"></a>

Before creating your first job, keep the following in mind\.

For jobs where you import data into Amazon S3, take these steps:
+ Create an AWS account with AWS Identity and Access Management \(IAM\) administrator\-level permissions\. For more information, see [Setting Up Your AWS Access for AWS Snowball Edge](setting-up.md)\.
+ Confirm that the files and folders to transfer are named according to the [object key naming guidelines](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-key-guidelines) for Amazon S3\. Any files or folders with names that don't meet these guidelines aren't imported into Amazon S3\.
+ Plan what data you want to import into Amazon S3\. For more information, see [How to Transfer Petabytes of Data Efficiently](transfer-petabytes.md)\.

Before exporting data from Amazon S3, take these steps:
+ Understand what data is exported when you create your job\. For more information, see [Using Export Ranges](exporttype.md#ranges)\.
+ For any files with a colon \(`:`\) in the file name, change the file names in Amazon S3 before you create the export job to get these files\. Files with a colon in the file name fail export to Microsoft Windows Server\. 

For jobs using compute instances:
+ Before you can add any SBE1 AMIs to your job, you must have an AMI created in your AWS account of the supported image type\. Currently, supported AMIs are based on the [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW), [Ubuntu Server 14\.04 LTS \(HVM\)](https://aws.amazon.com/marketplace/pp/B00JV9TBA6), and [Ubuntu 16\.04 LTS \- Xenial \(HVM\)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O) images\. You can get any one of these images from the [AWS Marketplace](https://aws.amazon.com/marketplace?b_k=291)\.
+ If you're going to SSH into the instances running on a Snowball Edge, you must already have the key pair for connecting to the instance
+ For information specific to using compute instances on a device, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.

## Services Related to the AWS Snowball Edge<a name="edge-related"></a>

You can use AWS Snowball with an AWS Snowball Edge device with the following related AWS services:
+ **Amazon S3** – You can use the Amazon S3 Adapter for Snowball, which supports a subset of the Amazon S3 API actions, to transfer data onto an AWS Snowball Edge device\. You can do this in a single AWS Snowball Edge device or in a cluster of devices for increased data durability\. In addition, you can import data hosted on an AWS Snowball Edge device into Amazon S3 and your local environment through a shipped AWS Snowball Edge device\. For more information on using Amazon S3, see the [Amazon Simple Storage Service Getting Started Guide](http://docs.aws.amazon.com/AmazonS3/latest/gsg/)\.
+ **Amazon EC2** – You can use the Amazon EC2 compatible endpoint, which supports a subset of the Amazon EC2 API actions, to run compute instances on a Snowball Edge device\. For more information on using Amazon EC2 in AWS, see [Amazon EC2 Getting Started Guide](http://docs.aws.amazon.com/AWSEC2/latest/GettingStartedGuide/)\.
+ **AWS Lambda powered by AWS Greengrass** – You can trigger Lambda functions based on Amazon S3 storage actions made on an AWS Snowball Edge device\. These Lambda functions are associated with an AWS Snowball Edge device during job creation\. For more information on using Lambda, see the [AWS Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/)\.

## Accessing the AWS Snowball Service<a name="accessing-service"></a>

There are two ways to access both the AWS Snowball service\. You can either use the [AWS Snowball Management Console](https://console.aws.amazon.com/importexport/home?region=us-west-2) or the job management API to create and manage jobs for AWS Snowball\. For more information on the job management API, see [Job Management API Reference for AWS Snowball](http://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\.

### Accessing an AWS Snowball Edge Device<a name="accessing-edge"></a>

After your Snowball Edge device or devices are onsite, you can access them through either the LCD display built into each device, the Amazon S3 and Amazon EC2 compatible endpoints, or through the available file interface\. You can also use the endpoints or the file interface to transfer data\. For more information, see [Using an AWS Snowball Edge](using-device.md)\.

## Pricing for the AWS Snowball Edge<a name="pricing-for-edge"></a>

For information about the pricing and fees associated with the service and its appliances, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

## Are You a First\-Time AWS Snowball User?<a name="first-time-user"></a>

If you are a first\-time user of the AWS Snowball service with the AWS Snowball Edge device, we recommend that you read the following sections in order:

1. To learn more about the different types of jobs, see [Jobs for AWS Snowball Edge devices](jobs.md)\.

1. For an end\-to\-end overview of how to use an AWS Snowball Edge device, see [How AWS Snowball Works with the Snowball Edge](how-it-works.md)\.

1. When you're ready to get started, see [Getting Started with an AWS Snowball Edge Device](getting-started.md)\.

1. For information about using compute instances on a device, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.