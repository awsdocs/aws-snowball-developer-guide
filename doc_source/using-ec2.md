--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using Amazon EC2 Compute Instances<a name="using-ec2"></a>

The following contains an overview on using compute instances on a Snowball Edge device, including conceptual information, procedures, and examples\.

## Overview<a name="ec2-overview-edge"></a>

Amazon Elastic Compute Cloud \(Amazon EC2\) is a web service that provides resizeable computing capacity—literally, servers in Amazon's data centers—that you use to build and host your software systems\. You can now run Amazon EC2 compute instances hosted on a Snowball Edge with the new `sbe1.xxxx` instance type\. This provides more options to run your compute workloads, adding to the existing support for serverless compute through AWS Lambda powered by AWS Greengrass\.

The compute instance types supported for use on a Snowball Edge \(identified by `sbe1.xxxx`\) are unique to Snowball Edge devices\. Like their cloud\-based counterparts, these instances require Amazon Machine Images \(AMIs\) to launch\. You choose the AMI to be that base image for an `sbe1.xxxx `instance in the cloud, before you create your Snowball Edge job\.

To use a compute instance on a Snowball Edge, create a job and specify your AMIs\. This can be done from the [AWS Snowball Management Console](https://console.aws.amazon.com/importexport/home?region=us-west-2), with the AWS CLI, or with one of the AWS SDKs\. Typically, there are some housekeeping prerequisites that you must resolve before creating your job, in order to use your instances\.

After you've handled the prerequisites, created your job, and waited for your device to arrive, you can start managing your AMIs and instances\. You can manage your compute instances on a Snowball Edge through an Amazon EC2–compatible endpoint\. This type of endpoint supports many of the Amazon EC2 AWS CLI commands and actions for the AWS SDKs\. You can't use the AWS Management Console on the Snowball Edge to manage your AMIs and compute instances\.

When you're done with your device, return it to AWS\. If the device was used in an import job, the data transferred using the Amazon S3 Adapter for Snowball or the file interface is imported into Amazon S3\. Otherwise, we perform a complete erasure of the device when it is returned to AWS\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.

**Important**  
Data in compute instances running on a Snowball Edge is not imported into AWS\.

### Compute Instances on Clusters<a name="ec2-overview-cluster"></a>

You can use compute instances on clusters of Snowball Edge devices, and the procedures and guidance for doing so is the same as it would be for using compute instances on a stand\-alone device\.

When you create a cluster job with AMIs, a copy of each AMI exists on each node in the cluster\. For that reason, there can only be 10 AMIs associated with a cluster of devices, regardless of the number of nodes on the cluster\. When you launch an instance in a cluster, you declare the node to host the instance in your command, and the instance runs on a single node\.

### Pricing for compute instances on Snowball Edge<a name="pricing-for-ec2-edge"></a>

There are additional costs associated with using compute instances\. For more information, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

## Prerequisites<a name="ec2-edge-prereqs"></a>

Before creating your job, keep the following information in mind\.
+ Before you add any AMIs to your job creation request, you'll need to have an AMI created in your AWS account of the supported image type\. Currently, supported AMIs are based on the [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW), [Ubuntu Server 14\.04 LTS \(HVM\)](https://aws.amazon.com/marketplace/pp/B00JV9TBA6), and [Ubuntu 16\.04 LTS \- Xenial \(HVM\)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O) images\. You can get any one of these images from the [AWS Marketplace](https://aws.amazon.com/marketplace?b_k=291)\.
+ All AMIs must be Amazon EBS based, with a single volume\.
+ If you are planning connecting to a compute instance running on a Snowball Edge, you must use SecureShell \(SSH\)\. To do so, you'll first need to *bake\-in* the key pair\. For more information, see [\(Optional\) Configure an AMI so you can SSH into the Compute Instances That the AMIs Launch on the Device](#important-optional-create-ec2-edge-job)\.

## Limits for Compute Instances on a Snowball Edge<a name="ec2-edge-limits"></a>

**Supported AWS Regions**  
You can add compute instances to your devices in the following regions:
+ US East \(Ohio\)
+ US East \(N\. Virginia\)
+ US West \(N\. California\)
+ US West \(Oregon\)
+ Asia Pacific \(Singapore\)
+ Asia Pacific \(Sydney\)
+ Asia Pacific \(Tokyo\)
+ EU \(Frankfurt\)
+ EU \(Ireland\)
+ EU \(London\)
+ EU \(Paris\)
+ South America \(São Paulo\)

**Storage Limits**  
The storage available for compute resources is a separate resource from the dedicated Amazon S3 storage on a Snowball Edge device\. The total available storage for `sbe1.xxxx` instances and AMIs is 1000 GiB\. The total available storage for Amazon S3 on a standalone device is based on the following factors\.
+ **AWS Snowball Edge device without compute instances** – 80 TB
+ **AWS Snowball Edge device with compute instances** – 70 \- 60 TB

When you create a job with compute instances, 10 TB of space are reserved for your AMIs\. This 10 TB is allocated regardless of the number and size of AMIs associated with your job\. When you start the device for the first time, the actual storage required for each of your AMIs is also reserved\. So if you have 5 TB of AMIs, when you turn on your device for the first time, it has 65 TB of available space\. Of this space, 10 TB is allocated for compute instances, and 5 TB is reserved for your actual AMIs\.

There's also a limit to the physical resources available for compute instances on a device\. To find the resource requirements and limitations for this feature, see the following tables\.


****  

| Feature | Limitation | 
| --- | --- | 
| Number of AMIs on a single Snowball Edge | 10 | 
| Number of volumes per instance | 1 | 
| Concurrently running \(or stopped\) instances | Varies depending on available resources | 


****  

| Instance type | vCPU cores | Memory \(GiB\) | 
| --- | --- | --- | 
| sbe1\.small | 1 | 1 | 
| sbe1\.medium | 1 | 2 | 
| sbe1\.large | 2 | 4 | 
| sbe1\.xlarge | 4 | 8 | 
| sbe1\.2xlarge | 8 | 16 | 
| sbe1\.4xlarge | 16 | 32 | 

### Shared Compute Resource Limitations<a name="shared-resource-limitations"></a>

The vCPU cores, memory, and storage available for compute resources is a separate resource from the dedicated Amazon S3 storage on a Snowball Edge\. However, compute resources are spread across the following services on the device:
+ File interface – while `ACTIVE`, this service uses 8 vCPU cores and 16 GiB of memory\.
+ AWS Greengrass and AWS Lambda powered by AWS Greengrass – while `ACTIVE`, these services combined use 4 vCPU cores and 8 GiB of memory\.
+ Compute instances – If no other compute services are `ACTIVE`, you have up to 16 vCPUs and 32 GiB of memory for your compute instances\.

You can determine whether or not a service is `ACTIVE` on a Snowball Edge using the Snowball client command `snowballEdge describe-service`\. For more information, see [Getting Service Status](using-client-commands.md#client-service-status)\.

**Important**  
A Snowball Edge device with any of its available compute resources maxed out is unable to launch new compute resources, and those requests fail\. For example, if you try to start the file interface while also running a `sbe1.4xlarge` compute instance, the file interface doesn't start\.

## Creating a Job with Compute Instances<a name="create-ec2-edge-job"></a>

In this section, you create your first compute instance job\. This process has some optional steps in the beginning, depending on whether or not you plan on using SSH to connect to your instances when they're running on your Snowball Edge device\.

**Important**  
Be aware of the following points before you create your job:  
Make sure the vCPU, memory, and storage values associated with your AMI match the type of instance you want to create\.
If you're going to use SSH to connect to the instance *after* you launch the instance on your Snowball Edge, you must first follow this optional procedure\. You can't update the AMIs on your Snowball Edge after the fact\. You must do this step before creating the job\.

### \(Optional\) Configure an AMI so you can SSH into the Compute Instances That the AMIs Launch on the Device<a name="important-optional-create-ec2-edge-job"></a>

In order to use SSH to connect to your compute instances on Snowball Edge devices, you must perform the following optional procedure to *bake\-in* the SSH key into the AMI before creating your job\. We also recommend that you use this procedure to set up your applications on the instance that you'll use as the AMI for your job\.

**Important**  
If you don't follow this optional procedure, there is no way to SSH into your instances when you receive your Snowball Edge device\.

1. Launch a new instance in the AWS cloud based on the [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW), [Ubuntu Server 14\.04 LTS \(HVM\)](https://aws.amazon.com/marketplace/pp/B00JV9TBA6), or [Ubuntu 16\.04 LTS \- Xenial \(HVM\)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O) images\.

   When you launch your instance, you'll want to make sure that the storage size that you assign to the instance is appropriate for your later use on the Snowball Edge\. In the Amazon EC2 AWS Management Console, this is done in **Step 4: Add Storage**\. For a list of the supported sizes for compute instance storage volumes on a Snowball Edge, see [Limits for Compute Instances on a Snowball Edge](#ec2-edge-limits)\.

1. Install and configure the applications that you want to run on the Snowball Edge, and test that they work as expected\.

1. Make a copy of the PEM/PPK file that you used for the SSH key pair to create this instance\. You'll need to save this file to the server that you'll use to communicate with the Snowball Edge\. This file is required for using SSH to connect to the launched instance on your device, so make a note of the path to this file\.

1. Save the instance as an AMI\. For more information, see [Creating an Amazon EBS\-Backed Linux AMI](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html) in the Amazon EC2 User Guide for Linux Instances\.

1. Repeat this procedure for each of the instances that you want to SSH into, keeping copies of your different SSH key pairs and taking note of the AMIs they're associated with\.

### Creating Your Job in the Console<a name="create-ec2-edge-console"></a>

Your next step is to create a job\. Your job can be of any job type, including a cluster\. Using the [AWS Snowball Management Console](https://console.aws.amazon.com/importexport/home?region=us-west-2), and follow the instructions provided in [Create Your First Job](create-job.md), add these additional steps when you get to the **Step 3: Give job details** page in the job creation wizard\.

1. Choose **Enable compute with EC2**\.

1. Choose **Add an AMI**\.

1. In the dialog box that opens, choose an AMI and choose **Save**\.

1. Add up to 10 total AMIs to your job\.

1. Continue creating your job as normal\.

### Creating Your Job in the AWS CLI<a name="create-ec2-edge-cli"></a>

Alternatively, you can create your job using the AWS CLI\. To do this, open a terminal and run the following command, replacing the red text with your actual values:

```
aws snowball create-job --job-type IMPORT --resources '{"S3Resources":[{"BucketArn":"arn:aws:s3:::bucket-name"}],"Ec2AmiResources":[{"AmiId":"ami-12345678"}]}' --description Example --address-id ADIEXAMPLE60-1234-1234-5678-41fEXAMPLE57  --kms-key-arn arn:aws:kms:us-west-2:012345678901:key/eEXAMPLE-1234-1234-5678-5b4EXAMPLE8e --role-arn arn:aws:iam::012345678901:role/snowball-local-s3-lambda-us-west-2-role --snowball-capacity-preference T100 --shipping-option SECOND_DAY --snowball-type EDGE
```

After it arrives and you've unlocked your device, you'll need to use the Snowball client to get your local credentials\. For more information, see [Getting Credentials](using-client-commands.md#client-credentials)\.

## Network Configuration for Compute Instances<a name="network-config-ec2-edge"></a>

After you’ve launched your compute instances on a Snowball Edge device, you need to set up your network configuration for each instance\. Use the following procedure whenever you launch a new instance to give that instance a virtual network interface and IP address\.

1. Make sure there's power to your device and that one of your physical network interfaces, like the RJ45 port, are connected with an IP address\.

1. Get the IP address associated with the physical network interface that you're using on the Snowball Edge\. For more information, see [Connect to Your Local Network](getting-started-connect.md)\.

1. Configure your Snowball client\. For more information, see [Configuring a Profile for the Snowball Client](using-client-commands.md#client-configuration)\.

1. Unlock the device\. For more information, see [Unlocking AWS Snowball Edge Devices](using-client-commands.md#setting-up-client)\.

1. Run the `snowballEdge describe-device` command to get the list of physical network interface IDs\.

1. Identify the ID for the physical network interface that you want to use, and make a note of it\.

1. Run the `snowballEdge create-virtual-network-interface` command\. The following examples show running this command with the two different IP address assignment methods, either DHCP or STATIC\.

   ```
   snowballEdge create-virtual-network-interface \
   --physical-network-interface-id s.ni-abcd1234 \
   --ip-address-assignment DHCP
            
           //OR//
           
   snowballEdge create-virtual-network-interface \
   --physical-network-interface-id s.ni-abcd1234 \
   --ip-address-assignment STATIC \
   --static-ip-address-configuration IpAddress=192.0.2.0,Netmask=255.255.255.0
   ```

1. The command returns a JSON structure that includes the IP address\. Make a note of that IP address as you'll need it for the `ec2 associate-address` AWS CLI command\.

1. Anytime you need this IP address, you can use the `snowballEdge describe-virtual-network-interfaces` Snowball client command, or the `aws ec2 describe-addresses` AWS CLI command to get it\.

1. Associate your newly created IP address with the instance, using the following AWS CLI command: 

   ```
   aws ec2 associate-address --public-ip 192.0.2.0 --instance-id s.i-01234567890123456 --endpoint <physical IP address for your Snowball Edge>:8008
   ```

## Connecting to Your Compute Instance on a Snowball Edge using SSH<a name="ssh-ec2-edge"></a>

In order to use SSH to connect to your compute instances on Snowball Edge devices, you must have followed the optional procedure to *bake\-in* the SSH key into the AMI before creating your job\. For more information on that procedure, see [\(Optional\) Configure an AMI so you can SSH into the Compute Instances That the AMIs Launch on the Device](#important-optional-create-ec2-edge-job)\. If you haven't followed that procedure, there is no way to SSH into your instances\.

**To connect to your instance with SSH**

1. Make sure your device is powered on, connected to network, and unlocked\. For more information, see [Connect to Your Local Network](getting-started-connect.md)\.

1. Make sure you have your network settings configured for your compute instances\. For more information, see [Network Configuration for Compute Instances](#network-config-ec2-edge)\.

1. Refer to your notes to find the PEM/PPK key pair that you used for this specific instance, and make a copy of those files somewhere on your computer\. Make a note of the path to the PEM file\.

1. Connect to your instance through SSH as in the following example command\. The IP address is the IP address of the virtual network interface \(VNIC\) that you set up in [Network Configuration for Compute Instances](#network-config-ec2-edge)\.

   ```
   ssh -i path/to/PEM/key/file instance-user-name@192.0.2.0
   ```

   For more information, see [Connecting to Your Linux Instance Using SSH](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html) in the Amazon EC2 User Guide for Linux Instances\.

## Transferring Data from Amazon EC2 Compute Instances to Amazon S3 Buckets on the Same Snowball Edge<a name="data-transfer-ec2-s3-edge"></a>

You can transfer data between compute instances and Amazon S3 buckets on the same Snowball Edge device\. This is done by using the supported AWS CLI commands and the appropriate endpoints\. For example, assume that you want to move data from a directory in my `sbe1.xlarge` instance into the Amazon S3 bucket, `myBucket` on the same device, using the Amazon S3 endpoint `192.0.2.1:8080`\. You would use the following procedure\.

**Note**  
This procedure only works if you've followed the instructions in [\(Optional\) Configure an AMI so you can SSH into the Compute Instances That the AMIs Launch on the Device](#important-optional-create-ec2-edge-job)\.

**To transfer data between a compute instance and a bucket on the same Snowball Edge**

1. Use SSH to connect to your compute instance\.

1. Download and install the AWS CLI\. If your instance doesn't already have the AWS CLI, you'll need to download and install it\. For more information, see [Installing the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/installing.html)\. 

1. Configure the AWS CLI on your compute instance to work with the Amazon S3 endpoint on the Snowball Edge\. For more information, see [Getting and Using Local Amazon S3 Credentials](using-adapter.md#adapter-credentials)\.

1. Use the supported Amazon S3 AWS CLI commands to transfer data\. For example:

   ```
   aws s3 cp ~/june2018/results s3://myBucket/june2018/results --recursive --endpoint http://192.0.2.1:8080
   ```