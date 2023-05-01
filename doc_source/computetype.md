# Local Compute and Storage Only Jobs<a name="computetype"></a>

Local compute and storage jobs enable you to use Amazon S3 locally, without an internet connection\. While local storage and compute functionality also exists for the import and export job types, this job type is only for local use\. You can't export data from Amazon S3 onto the device or import data into Amazon S3 when the device is returned\. 

**Topics**
+ [Local Storage Jobs](#aboutstorage)
+ [Local Cluster Option](#clusteroption)

## Local Storage Jobs<a name="aboutstorage"></a>

You can read and write objects to an AWS Snowball Edge device using Amazon S3 compatible storage on Snow Family devices or the file interface\. Provision storage space for Amazon S3 compatible storage on Snow Family devices when you order your device\. Amazon S3 compatible storage on Snow Family devices supports Amazon S3 REST API actions\. This Amazon S3 REST API support is limited to a subset of S3 REST API actions\. For more information, see [Amazon S3 compatible storage on Snow Family devices](https://docs.aws.amazon.com/snowball/latest/developer-guide/s3compatible-on-snow.html) in this guide\.

When you've finished using the device, return it to AWS, and the device will be erased\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.

## Local Cluster Option<a name="clusteroption"></a>

A cluster is a logical grouping of Snowball Edge devices, in groups of 3 to 16 devices\. A cluster is created as a single job, which offers increased durability and storage size when compared to other AWS Snowball job offerings\. For more information about cluster jobs, see [Clustinering overview](https://docs.aws.amazon.com/snowball/latest/developer-guide/ClusterOverview.html) in this guide\.