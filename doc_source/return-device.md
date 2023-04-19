# Returning the Snowball Edge Device<a name="return-device"></a>

The prepaid shipping information on the E Ink display contains the address to return the AWS Snowball Edge device\. For information about with which carrier to return the device, see [Shipping carriers](mailing-storage.md#carriers)\. 

The device is delivered to an AWS sorting facility and forwarded to the AWS data center\. The carrier automatically provides a tracking number for your job to the AWS Snow Family Management Console\. You can access the tracking number and a link to the carrier's tracking website by viewing the job's status details in the console or by making calls to the job management API\.

If you've powered off and unplugged your Snowball Edge device and the shipping information doesn't appear on the E Ink screen after about a minute, see [Troubleshooting problems returning Snow Family devices](troubleshooting.md#return-shipping-troubleshooting)\.

You can track the status changes of your job through the AWS Snow Family Management Console as AWS processes the device\. You can use Amazon SNS notifications if you selected that option during job creation, or you can make calls to the job management API\. For more information about this API, see [AWS Snowball API Reference](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\. 

The final status values include when the AWS Snowball Edge device has been received by AWS, when data import begins, and when the job is completed\.

## Preparing an AWS Snowball Edge device for shipping<a name="device-shipping"></a>

The following explains how to prepare an AWS Snowball Edge device and ship it back to AWS\.

**To prepare an AWS Snowball Edge device for shipping**

1. Disconnect and stow the power cable in the cable nook on top of the AWS Snowball Edge device\.

1. Close the doors on the back, top, and front of the AWS Snowball Edge device\. Press in until you hear and feel them click\.

You don't need to pack the AWS Snowball Edge device in a container, because the device itself is its own physically rugged shipping container\. The E Ink display on the top of the AWS Snowball Edge device displays the return shipping information when the device is turned off\.

**Job\-Type Specific Consideration** 

**Important**  
If you are importing data, don't delete your local copies of the transferred data until the import to Amazon S3 is successful at the end of the process, and you can verify the results of the data transfer\.