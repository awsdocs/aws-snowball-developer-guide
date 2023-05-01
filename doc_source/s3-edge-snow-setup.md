# Setting up your Snowball Edge device<a name="s3-edge-snow-setup"></a>

AWS Snowball Edge is a rugged device protected by AWS Key Management Service \(AWS KMS\) that you can use for local storage and compute or transferring data between your on\-premises servers and Amazon S3\.

When the device first arrives, visually inspect it for damage or obvious tampering\.

**Warning**  
If you notice anything that looks suspicious about the device, such as a damaged enclosure or signs of tampering, don't connect it to your internal network\. Instead, contact your AWS representative to have a new one shipped to you\.

The device has three doors—a front, a back, and a top—that all can be opened by latches\. The top door contains the power cable for the device\. The other two doors can be opened and slid inside the device so that they're out of the way while you're using it\. By opening the doors, you can access the display that's embedded in the front side of the device and the power and network ports in the back\.

After your device is powered on, you're ready to use it\. For more information on using the device, see the [https://docs.aws.amazon.com/snowball/latest/developer-guide/using-device.html](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-device.html)\.

You can use Amazon S3 compatible storage on Snow Family devices in a *cluster* as a single unit, which is a logical grouping of Snowball Edge devices\. After your system is set up and running, you can make API calls to any of the devices in the cluster\.