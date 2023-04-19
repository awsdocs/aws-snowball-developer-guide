# Returning the Snowball Edge Device<a name="return-device"></a>

For information about returning a Snowball Edge, see [AWS Snowball Pickups in the EU, US, South Africa, Singapore, and Canada](mailing-storage.md#standard-pickup)\.

The prepaid shipping label on the E Ink display contains the correct address to return the AWS Snowball Edge device\. For information about how to return the device, see [Shipping Carriers](mailing-storage.md#carriers)\. 

The device is delivered to an AWS sorting facility and forwarded to the AWS data center\. The carrier automatically reports back a tracking number for your job to the AWS Snow Family Management Console\. You can access that tracking number, and also a link to the tracking website, by viewing the job's status details in the console, or by making calls to the job management API\.

**Important**  
Unless personally instructed otherwise by AWS, never affix a separate shipping label to the device\. Always use the shipping label that is on the E Ink display\.

In addition, you can track the status changes of your job through the AWS Snow Family Management Console\. You can use Amazon SNS notifications if you selected that option during job creation, or you can make calls to the job management API\. For more information about this API, see [AWS Snowball API Reference](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\. 

The final status values include when the AWS Snowball Edge device has been received by AWS, when data import begins, and when the job is completed\.

## Disconnecting the Snowball Edge<a name="disconnectdevice"></a>

Disconnect the AWS Snowball Edge device cables\. Secure the device's power cable into the cable nook beneath the top door on the device\. 

Pull out and close the front and back doors\. When they close completely, you hear an audible click\. When the return shipping label appears on the E Ink display on top of the device, it's ready to be returned\. To see who your region's carrier is, see [Shipping Carriers](mailing-storage.md#carriers)\.

**Job\-Type Specific Consideration** 

**Important**  
If you are importing data, don't delete your local copies of the transferred data until the import to Amazon S3 is successful at the end of the process, and you can verify the results of the data transfer\.