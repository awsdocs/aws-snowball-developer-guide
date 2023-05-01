# Using Your Snowball Edge<a name="transfer-data"></a>

Now you can use the AWS Snowball Edge device\. Regardless of your job type, keep the following information in mind while using the device:
+ You can use the AWS OpsHub for Snow Family application to read or write data to the device or cluster of devices\. You can also use it to manage your device\. For more information about AWS OpsHub, see [Using AWS OpsHub for Snow Family to Manage Devices](aws-opshub.md)\.
+ You can use the built\-in Amazon S3 adapter to read or write data to a device or cluster of devices\. The interface can work through the AWS Command Line Interface \(AWS CLI using version 1\.16\.14 or earlier\), one of the AWS SDKs, or your own RESTful application\. For more information about the Amazon S3 adapter, see [Transferring files using the Amazon S3 adapter for data migration](using-adapter.md)\.
+ You can use the file interface to read or write data to a device or a cluster of devices\. For more information, see [Transferring Files to Snowball Edge devices using the File Interface](using-fileinterface.md)\.
+ You can use Amazon S3 compatible storage on Snow Family devices to create Amazon S3 buckets on your Snowball Edge device and store and retrieve objects on\-premises for applications that require local data access, local data processing, and data residency\. You can use AWS CLI, the AWS SDK, or AWS OpsHub with Amazon S3 compatible storage on Snow Family devices\. For more information, see [Amazon S3 compatible storage on Snow Family devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/s3compatible-on-snow.html) in this guide\.
+ There is at least one directory at the root level of the device\. This directory and any others at the root level have the same names as the buckets that were chosen when this job was created\. Data cannot be transferred directly into the root directory\. It must instead go into one of these bucket directories or into their subdirectories\.

When you're done using the AWS Snowball Edge device, it's time to prepare the device for its return trip to AWS\.

**Next:** [Powering Off the Snowball Edge](turnitoff.md) 