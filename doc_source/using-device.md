--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using an AWS Snowball Edge<a name="using-device"></a>

Following, you can find an overview of the AWS Snowball Edge device, the physically rugged device protected by AWS Key Management Service \(AWS KMS\) that you'll use for local storage and compute, or to transfer data between your on\-premises servers and Amazon Simple Storage Service \(Amazon S3\)\.

For information on unlocking an AWS Snowball Edge device, see [Using the Snowball Client](using-client.md)\.

When the device first arrives, inspect it for damage or obvious tampering\.

**Warning**  
If you notice anything that looks suspicious about the device, don't connect it to your internal network\. Instead, contact [AWS Support](https://aws.amazon.com/premiumsupport/), and a new one will be shipped to you\.

The following image shows what the AWS Snowball Edge device looks like\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/SnowballEdgeAppliance.png)

It has three doors, a front, a back, and a top that all can be opened by latches\. The top door contains the power cable for the device\. The other two doors can be opened and slid inside the device so they're out of the way while you're using it\.

Doing this gives you access to the LCD E Ink display embedded in the front side of the device, and the power and network ports in the back\.

Plug the AWS Snowball Edge device into power, and into your local network using one of your network cables\. Each AWS Snowball Edge device has been engineered to support data transfer over RJ45, SFP\+ , or QSFP\+, and is capable of network speeds of over 10 GB/second\. Power on the AWS Snowball Edge device by pressing the power button above the LCD display\.

You’ll hear the AWS Snowball Edge device internal fans start up, and the display starts up with a small video\. The fans will get quieter after a short time\. Wait a few moments, and a screen appear that indicates that the device is ready\. When that happens, the AWS Snowball Edge device is ready to communicate with the Snowball client, the tool used to unlock your access to it\.

You use the LCD display to get some of the local management information for the services on the device, and also to manage the IP address that the AWS Snowball Edge device uses to communicate across your local network\.

## Changing Your IP Address<a name="change-device-ip"></a>

You can change your IP address to a different static address, which you provide by following this procedure\.

**To change the IP address of a AWS Snowball Edge device**

1. On the LCD display, tap **CONNECTION**\. You'll see a screen that shows you the current network settings for the AWS Snowball Edge device\.

1. The IP address below this drop\-down box is updated to reflect the DHCP address that the AWS Snowball Edge device requested\. You can change it to a static IP address, or leave it as is\.