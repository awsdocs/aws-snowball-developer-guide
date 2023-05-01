# Set up Amazon S3 compatible storage on Snow Family devices using AWS OpsHub<a name="s3-edge-snow-opshub"></a>

If you don't want to use the AWS CLI, you can set up your device or cluster using the AWS OpsHub for Snow Family, user interface\.

The Amazon S3 compatible storage on Snow Family devices service is not active by default\. To start the service on a device or cluster, you must create two virtual network interfaces \(VNICs\) on each device to attach to the `s3control` and `s3api` endpoints\.

**Topics**
+ [Prerequisites](#s3-edge-snow-opshub-prereqs)
+ [Using the simple setup option](#s3-edge-snow-opshub-simple-setup)
+ [Using the advanced setup option](#s3-edge-snow-opshub-advanced-setup)

## Prerequisites<a name="s3-edge-snow-opshub-prereqs"></a>

Before you can set up your device or cluster using AWS OpsHub for Snow Family, do the following:
+ Power on your Snowball Edge device and connect it to your network\.
+ On your local machine, download and install the latest version of [AWS OpsHub](https://docs.aws.amazon.com/snowball/latest/developer-guide/download-opshub.html)\. Connect to the device or cluster to unlock it with a manifest file\. For more information, see [unlocking a device](https://docs.aws.amazon.com/snowball/latest/developer-guide/connect-unlock-device.html)\.

## Using the simple setup option<a name="s3-edge-snow-opshub-simple-setup"></a>

Use the simple setup option if your network uses DHCP\. With this option, the VNICs are created automatically on each device when you start the service\.

1. Log in to AWS OpsHub, then choose **Manage Storage**\.

   This takes you to the Amazon S3 compatible storage on Snow Family devices landing page\.

1. For **Start service setup type**, choose **Simple**\.

1. Choose **Start service**\.
**Note**  
This takes a few minutes to complete and depends on the number of devices you're using\.

   After the service starts, the Service state is active, and there are endpoints\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/s3-snow/s3-snow-active-service.png)

   The Amazon S3 compatible storage on Snow Family devices resources screen, showing a service state of Active and its active endpoints\.

## Using the advanced setup option<a name="s3-edge-snow-opshub-advanced-setup"></a>

Use the advanced setup option if your network uses static IP addresses or if you want to reuse existing VNIs\. With this option, you create VNICs for each device manually\.

1. Log in to AWS OpsHub, then choose **Manage Storage**\.

   This takes you to the Amazon S3 compatible storage on Snow Family devices landing page\.

1. For **Start service setup type**, choose **Advanced**\.

1. Select the devices that you need to create VNICs for\.

   For clusters, you need a minimum quorum of devices to start the Amazon S3 compatible storage on Snow Family devices service\. The quorum is two for a three\-node cluster\.
**Note**  
For the initial start of the service in a cluster setup, you must have all devices in the cluster configured and available for the service to start\. For subsequent starts, you can use a subset of the devices if you meet quorum, but the service will start in a degraded state\.

1. For each device, choose an existing VNIC or select **Create VNI**\. 

   Each device needs a VNIC for the **S3 endpoint** for object operations and another for the **S3Control endpoint** for bucket operations\.

1. If you're creating a VNIC, choose a physical network interface and enter the status IP address and subnet mask, then choose **Create virtual network interface**\.

1. After you create your VNICS, choose **Start service**\.
**Note**  
This takes a few minutes to complete and depends on the number of devices you're using\.

   After the service starts, the Service state is active, and there are endpoints\.