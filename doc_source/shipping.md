# Shipping Considerations for AWS Snowball<a name="shipping"></a>

The following sections provide information about how shipping is handled for an AWS Snowball Edge device and a list that shows each AWS Region that is supported\. The shipping rate you choose for a job applies to both sending and receiving the AWS Snowball Edge device or devices used for that job\. For information about shipping charges, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

**Topics**
+ [Preparing an AWS Snowball Edge for Shipping](#device-shipping)
+ [Region\-Based Shipping Restrictions](#shipwithinregion)
+ [Shipping an AWS Snowball Edge](mailing-storage.md)

When you create a job, you specify a shipping address and shipping speed\. This shipping speed doesn’t indicate how soon you can expect to receive the AWS Snowball Edge device from the day you created the job\. It only shows the time that the device is in transit between AWS and your shipping address\. That time doesn’t include any time for processing\. That depends on factors that include job type \(exports take longer than imports, typically\) and job size \(cluster jobs take longer than individual jobs, typically\)\. Also, carriers generally only pick up outgoing Snowball Edge devices once a day\. Thus, processing before shipping can take a day or more\.

**Note**  
Snowball Edge devices can only be used to import or export data within the AWS Region where the devices were ordered\.

## Preparing an AWS Snowball Edge for Shipping<a name="device-shipping"></a>

The following explains how to prepare an AWS Snowball Edge device and ship it back to AWS\.

**To prepare an AWS Snowball Edge device for shipping**

1. Make sure that you've finished transferring all the data for this job to or from the AWS Snowball Edge device\. [Unlock the device\.](https://docs.aws.amazon.com/snowball/latest/developer-guide/connect-unlock-device-sbe.html)

1. Press the power button above the LCD display\. It takes about 20 seconds for the device to power off\.
**Note**  
If you've powered off and unplugged the AWS Snowball Edge device, and your shipping label doesn't appear after about a minute on the E Ink display on top of the device, contact [AWS Support](https://aws.amazon.com/premiumsupport/)\.

1. Disconnect and stow the power cable the AWS Snowball Edge device was sent with in the cable nook on top of the device\.

1. Close the three doors on the back, the top, and the front of the AWS Snowball Edge device\. Press in on each one at a time until you hear and feel them click\.

You don't need to pack the AWS Snowball Edge device in a container, because it is its own physically rugged shipping container\. The E Ink display on the top of the AWS Snowball Edge device changes to your return shipping label when the device is turned off\.

## Region\-Based Shipping Restrictions<a name="shipwithinregion"></a>

Before you create a job, you should sign in to the console from the AWS Region that your Amazon S3 data is housed in\. A few shipping restrictions apply:
+ AWS Snowball Edge devices are not shipped between international countries—for example, from Asia Pacific \(India\) to Asia Pacific \(Australia\)\. 

The sole exception to crossing international countries is among EU Member Countries\. For data transfers in the EU Regions, we only ship AWS Snowball Edge devices to the EU member countries listed: 
+ Austria, Belgium, Bulgaria, Croatia, Republic of Cyprus, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Italy, Ireland, Latvia, Lithuania, Luxembourg, Malta, Netherlands, Poland, Portugal, Romania, Slovakia, Slovenia, Spain and Sweden\.

Shipments domestically within the same country is permitted\. Examples:
+ For data transfers in the United Kingdom Region, we ship devices domestically within the UK\.
+ For data transfers in Asia Pacific \(Mumbai\), we ship devices within India\. 

**Note**  
AWS doesn't ship AWS Snowball Edge devices to post office boxes\.