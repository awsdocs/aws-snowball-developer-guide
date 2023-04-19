# AWS Snowball Edge Device Differences<a name="device-differences"></a>

This guide contains documentation for the Snowball Edge devices\. You can use these devices to move huge amounts of data into and out of Amazon S3\. You can order them using the [job management API](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html) or the [AWS Snow Family console](https://console.aws.amazon.com/importexport)\. For frequently asked questions and pricing information, see [AWS Snowball](https://aws.amazon.com/snowball-edge)\.

**Topics**
+ [Snowball Edge Device Options](#device-options)
+ [AWS Snow Family Use Case Differences](#usecase-differences)
+ [AWS Snow Family Tool Differences](#tool-differences)

## Snowball Edge Device Options<a name="device-options"></a>

Snowball Edge devices have the following options for device configurations:
+ **Snowball Edge Storage Optimized \(for data transfer\)** – This Snowball Edge device option has a 100 TB \(80 TB usable\) storage capacity\. 
+ **Snowball Edge Storage Optimized \(with EC2 compute functionality\)** – This Snowball Edge device option has up to 80 TB of usable storage space, 24 vCPUs, and 32 GiB of memory for compute functionality\. It also comes with 1 TB of additional SSD storage space for block volumes attached to Amazon EC2 AMIs\.
+ **Snowball Edge Compute Optimized** – This Snowball Edge device option has the most compute functionality, with 52 vCPUs, 208 GiB of memory, and 42 TB \(39\.5 usable\) plus 7\.68 TB of dedicated NVMe SSD for compute instances for block storage volumes for EC2 compute instances, and 42 TB of HDD capacity for either object storage or block storage volumes\.
+ **Snowball Edge Compute Optimized with GPU** – This Snowball Edge device option is identical to the Compute Optimized option, except for an installed GPU, equivalent to the one available in the P3 Amazon EC2 instance type\. It has a storage capacity of 42 TB \(39\.5 TB of HDD storage that can be used for a combination of Amazon S3 compatible object storage and Amazon EBS compatible block storage volumes\) plus 7\.68 TB of dedicated NVMe SSD for compute instances\.

For more information about the compute functionality of these three options, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.

**Note**  
When this guide refers to *Snowball Edge devices*, it's referring to all optional variants of the device\. Whenever specific information applies only to one or more optional configurations \(such as how the Snowball Edge Compute Optimized with GPU option has an on\-board GPU peripheral\), it is mentioned explicitly\.

The following table summarizes the differences between the various device options\. For hardware specification information, see [AWS Snowball Edge Specifications](specifications.md)\.


|  | Snowball Edge Storage Optimized \(for data transfer\) | Snowball Edge Storage Optimized \(with EC2 compute functionality\) | Snowball Edge Compute Optimized | 
| --- | --- | --- | --- | 
| CPU | AMD Naples, 32 cores, 3\.4Ghz | Intel Xeon D processor, 16 cores, 1\.8Ghz | AMD Naples, 32 cores, 3\.4Ghz | 
| vCPUs |  | 24 | 52 | 
| Usable memory |  | 32 GB | 208 GB | 
| Security card | Yes | Yes | Yes | 
| GPU \(optional\) | None | None | None \(NVidia V100\) | 
| SSD |  | 1 TB SATA | 7\.68 TB NVMe | 
| Usable HDD | 80 TB plus 1 TB of dedicated SATA SSD for compute instances\. | 80 TB | 39\.5 TB  | 
| Network interfaces |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  | 
| Physical security features |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/device-differences.html)  | 

## AWS Snow Family Use Case Differences<a name="usecase-differences"></a>

The following table shows the different use cases for the different AWS Snow Family devices\.


| Use case | Snowball Edge | AWS Snowcone | 
| --- | --- | --- | 
| Import data into Amazon S3 | ✓ | ✓ | 
| Export from Amazon S3 | ✓ |  | 
| Durable local storage | ✓ |  | 
| Local compute with AWS Lambda | ✓ |  | 
| Local compute instances | ✓ | ✓ | 
| Durable Amazon S3 storage in a cluster of devices | ✓ |  | 
| Use with AWS IoT Greengrass \(IoT\) | ✓ |  | 
| Transfer files through NFS with a GUI | ✓ | ✓ | 
| GPU workloads | ✓ |  | 

**Note**  
Workloads that need GPU support require the Snowball Edge Compute Optimized with GPU option\.

## AWS Snow Family Tool Differences<a name="tool-differences"></a>

The following outlines the different tools used with the Snow Family devices, and how they are used\.

### Snowball Edge Tools<a name="tool-differences-edge"></a>

**AWS OpsHub for Snow Family**
+ The Snow Family devices now offer a user\-friendly tool, AWS OpsHub for Snow Family, that you can use to manage your devices and local AWS services\. You use AWS OpsHub on a client computer to perform tasks such as unlocking and configuring single or clustered devices, transferring files, and launching and managing instances running on Snow Family devices\. For more information, see [Using AWS OpsHub for Snow Family to Manage Snowball Devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/aws-opshub.html)\.

**Snowball Edge client with Snowball Edge**
+ Download the Snowball Edge client from the [AWS Snowball Edge Resources](http://aws.amazon.com/snowball-edge/resources/) page and install it on your own computer\.
+ Use the Snowball Edge client to unlock the Snowball Edge or the cluster of Snowball Edge devices\. For more information, see [Using the Snowball Edge Client](using-client.md)\.
+ The Snowball Edge client doesn't transfer data\.

**Amazon S3 interface with Snowball Edge**
+ Is already installed on the Snowball Edge by default\. It does not need to be downloaded or installed\.
+ Can transfer data to or from the Snowball Edge\. For more information, see [Transferring Files Using the Amazon S3 Interface](using-adapter.md)\.
+ Encrypts data on the Snowball Edge while the data is transferred to the device\.

**File interface with Snowball Edge**
+ Is already installed on the Snowball Edge by default\. It does not need to be downloaded or installed\.
+ Can transfer data by dragging and dropping files up to 150 GB in size from your computer to the buckets on the Snowball Edge through an easy\-to\-configure NFS mount point\. For more information, see [Transferring Files to AWS Snowball Edge Using the File Interface](using-fileinterface.md)\.
+ Encrypts data on the Snowball Edge while the data is transferred to the device\.

**AWS IoT Greengrass console with Snowball Edge**
+ With a Snowball Edge, you can use the AWS IoT Greengrass console to update your AWS IoT Greengrass group and the core running on the Snowball Edge\.

### Items Provided for Snowball Edge<a name="network-differences"></a>

The following outlines the network adapters, cables used, and cables provided for the Snowball Edge device\.


| Network interface | Snowball Edge support | Cables provided with device | 
| --- | --- | --- | 
| RJ45 | ✓ | Not provided\. | 
| SFP28 | ✓ | Not provided\. | 
| SFP28 \(with optic connector\) | ✓ | No cables provided\. No optic connector provided for Snowball Edge devices\.  | 
| QSFP | ✓ | No cables or optics provided\. | 

For more information about the network interfaces, cables, and connectors, see [Supported Network Hardware](specifications.md#network-hardware)\.