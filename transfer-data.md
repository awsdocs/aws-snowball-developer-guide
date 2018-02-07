--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Use the Snowball Edge<a name="transfer-data"></a>

Now you can use the AWS Snowball Edge appliance\. Regardless of your job type, keep the following information in mind while using the appliance:

+ You can use the built\-in Amazon S3 Adapter for Snowball to read or write data to an appliance or cluster of appliances\. The adapter can work through the AWS Command Line Interface \(AWS CLI\), one of the AWS SDKs, or your own RESTful application\. For more information on the adapter, see [Using the Amazon S3 Adapter](using-adapter.md)\.

+ You can use the file interface to read or write data to an appliance or a cluster of appliances\. For more information, see [Using the File Interface for the AWS Snowball Edge](using-fileinterface.md)\.

+ There is at least one directory at the root level of the appliance\. This directory and any others at the root level have the same names as the buckets that were chosen when this job was created\. Data cannot be transferred directly into the root directory; it must instead go into one of these bucket directories or into their subdirectories\.

When you're done using the AWS Snowball Edge appliance, it's time to prepare the appliance for its return trip to AWS\.

**Next:** [Stop the Snowball Client, and Power Off the Snowball Edge](turnitoff.md) 