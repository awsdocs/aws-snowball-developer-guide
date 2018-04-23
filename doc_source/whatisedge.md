--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# What Is an AWS Snowball Edge?<a name="whatisedge"></a>

AWS Snowball is a service that accelerates transferring large amounts of data into and out of AWS using physical storage appliances, bypassing the internet\. AWS Snowball Edge is a 100 TB data transfer device with on\-board storage and compute power for select AWS capabilities\. In addition to transferring data to AWS, Snowball Edge can undertake local processing and edge\-computing workloads\.

Features include:
+ An Amazon S3\-compatible endpoint on the device\.
+ A file interface with Network File System \(NFS\) support\.
+ A cluster mode where multiple Snowball Edge devices can act as a single, scalable storage pool with increased durability\.
+ The ability to run AWS Lambda powered by AWS Greengrass functions as data is copied to the device\.

Each AWS Snowball appliance type can transport data at speeds faster than the internet\. This transport is done by shipping the data in the appliances through a regional carrier\. The appliances are rugged shipping containers, complete with E Ink shipping labels\. The AWS Snowball Edge appliance differs from the standard Snowball because it can bring the power of the AWS Cloud to your local environment, with local storage and compute functionality\.

The storage and compute functionality is built in\. With an AWS Snowball Edge appliance, there’s no need for a powerful workstation to handle encryption, because all encryption happens on the appliance itself\. There are two primary use cases supported for the AWS Snowball Edge appliance:
+ **Local storage and compute** – You can use one AWS Snowball Edge appliance, or a cluster of appliances, to harness AWS storage and compute services—like AWS Lambda powered by AWS Greengrass and an Amazon S3 compatible interface—in an environment that might or might not have an internet connection\.
+ **Transfer large amounts of data into and out of Amazon S3** – As with the original AWS Snowball appliance, the Snowball, the AWS Snowball Edge appliance can be used to transfer many terabytes or petabytes of data between Amazon S3 and your local environment, bypassing the internet\.

**Note**  
There are many options for transferring your data into AWS\. The AWS Snowball service is intended for transferring large amounts of data\. If you want to transfer less than 30 terabytes of data, or if you don’t have a local computing or clustering need, using an AWS Snowball Edge appliance might not be your most economical choice\.

## AWS Snowball Edge Features<a name="edge-feature-overview"></a>

AWS Snowball Edge appliances have the following features:
+ Each AWS Snowball Edge appliance has 100 TB of storage capacity, giving it twice the storage space of the original Snowball appliance\. 
+ Any one of three network adapters on the AWS Snowball Edge appliance supports network speeds of over 10 GB/second\.
+ Encryption is enforced, protecting your data at rest and in physical transit\.
+ You can import or export data between your local environments and Amazon S3, physically transporting the data with one or more AWS Snowball Edge appliances, completely bypassing the internet\.
+ AWS Snowball Edge appliances are their own rugged shipping containers, and the built\-in E Ink display changes to show your shipping label when the appliance is ready to ship\.
+ AWS Snowball Edge appliances come with an on\-board LCD display that can be used to manage network connections, get status, and watch helpful how\-to videos to help you get the most out of your job\.
+ AWS Snowball Edge appliances can be clustered for local storage and compute jobs to achieve 99\.999% data durability across 5 to 10 devices, and to locally grow and shrink storage on demand\.
+ You can use the file interface to read and write data to an AWS Snowball Edge appliance through a file share or Network File System \(NFS\) mount point\.
+ You can write Python\-language Lambda functions and associate them with buckets when you create an AWS Snowball Edge appliance job\. Each function triggers whenever there's a local Amazon S3 PUT object action executed on the associated bucket on the appliance\.

## Prerequisites for Using Snowball Edge<a name="snowball-prereqs"></a>

Before transferring data into Amazon S3 using Snowball Edge, you should do the following:
+ Create an AWS account and an administrator user in AWS Identity and Access Management \(IAM\)\. For more information, see [Sign Up for AWS](getting-started.md#signing-up)\.
+ If you are importing data, do the following:
  + Confirm that the files and folders to transfer are named according to the [Object Key Naming Guidelines](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-key-guidelines) for Amazon S3\. Any files or folders with names that don't meet these guidelines won't be imported into Amazon S3\.
  + Plan what data you want to import into Amazon S3\. For more information, see [How to Transfer Petabytes of Data Efficiently](transfer-petabytes.md)\.
+ If you are exporting data, do the following:
  + Understand what data will be exported when you create your job\. For more information, see [Using Export Ranges](exporttype.md#ranges)\.
  + For any files with a colon \(`:`\) in the file name, change the file names in Amazon S3 before you create the export job to get these files\. Files with a colon in the file name fail export to Microsoft Windows Server\. 

## Services Related to the AWS Snowball Edge<a name="edge-related"></a>

You can use AWS Snowball with an AWS Snowball Edge appliance with the following related AWS services:
+ **Amazon S3** – You can use the Amazon S3 Adapter for Snowball, which supports a subset of the Amazon S3 API actions, to transfer data onto an AWS Snowball Edge appliance\. You can do this in a single AWS Snowball Edge appliance or in a cluster of appliances for increased data durability\. In addition, you can import data hosted on an AWS Snowball Edge appliance into Amazon S3 and your local environment through a shipped AWS Snowball Edge appliance\. For more information on using Amazon S3, see the [Amazon Simple Storage Service Getting Started Guide](http://docs.aws.amazon.com/AmazonS3/latest/gsg/)\.
+ **AWS Lambda powered by AWS Greengrass** – You can trigger Lambda functions based on Amazon S3 storage actions made on an AWS Snowball Edge appliance\. These Lambda functions are associated with an AWS Snowball Edge appliance during job creation\. For more information on using Lambda, see the [AWS Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/)\.

## Accessing the AWS Snowball Service<a name="accessing-service"></a>

There are two ways to access both the AWS Snowball service and the appliances\. You can either use the [AWS Snowball Management Console](https://console.aws.amazon.com/importexport/home?region=us-west-2) or the job management API to create and manage jobs for AWS Snowball\. For more information on the job management API, see [Job Management API Reference for AWS Snowball](http://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\.

### Accessing the AWS Snowball Edge Appliance<a name="accessing-edge"></a>

Once your AWS Snowball Edge appliance or appliances are onsite, you can access them through either the LCD display built into each appliance, the Amazon S3 Adapter for Snowball, or through the available file interface\. You can also use the adapter or the file interface to transfer data\. For more information, see [Using an AWS Snowball Edge](using-appliance.md)\.

## Pricing for the AWS Snowball Edge<a name="pricing-for-edge"></a>

For information about the pricing and fees associated with the service and its appliances, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

## Are You a First\-Time AWS Snowball User?<a name="first-time-user"></a>

If you are a first\-time user of the AWS Snowball service with the AWS Snowball Edge appliance, we recommend that you read the following sections in order:

1. To learn more about the different types of jobs, see [Jobs for AWS Snowball Edge Appliances](jobs.md)\.

1. For an end\-to\-end overview of how to use an AWS Snowball Edge appliance, see [How AWS Snowball Works with the Snowball Edge](how-it-works.md)\.

1. When you're ready to get started, see [Getting Started with an AWS Snowball Edge Appliance](getting-started.md)\.