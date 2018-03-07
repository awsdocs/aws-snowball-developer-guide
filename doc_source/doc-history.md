--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Document History<a name="doc-history"></a>

The following table describes documentation releases for the AWS Snowball Edge appliance\.

+ **API version: 1\.0** 

+ **Latest documentation update: **February 5, 2018


****  

| Change | Description | Date | 
| --- | --- | --- | 
| Major feature revision to the Snowball client, and cluster update | The new major feature revision for the Snowball client includes performance improvements, profiles, and support for the cluster update\. For more information, see [Using the Snowball Client](using-client.md)\. Clusters are now leaderless\. All nodes can read and write data to the cluster\. For more information, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\. | February 5, 2018 | 
| New AWS Region supported | AWS Snowball is now supported in the EU \(Paris\) region\. For more information on shipping in this AWS Region, see [Shipping Considerations for AWS Snowball](shipping.md)\. | December 18, 2017 | 
| Improved AWS CLI support for the Amazon S3 Adapter for Snowball | You can now use the `s3 sync` command with the Amazon S3 Adapter for Snowball to sync data between a Snowball Edge and your local computer\. For more information, see [Supported AWS CLI Commands for Amazon S3](using-adapter-cli.md#using-adapter-cli-commands)\. | November 10, 2017 | 
| Updated file interface file size support | The file interface can now support files up to 150 GB in size\. For more information, see [Using the File Interface for the AWS Snowball Edge](using-fileinterface.md)\. | October 4, 2017 | 
| New AWS Region supported | AWS Snowball Edge is now supported in the Asia Pacific \(Tokyo\) region, with region\-specific shipping options\. For more information, see [Shipping Considerations for AWS Snowball](shipping.md)\. | September 19, 2017 | 
| New AWS Region supported | AWS Snowball Edge is now supported in the South America \(São Paulo\) region, with region\-specific shipping options\. For more information, see [Shipping Considerations for AWS Snowball](shipping.md)\. | August 8, 2017 | 
| Updated AWS Greengrass and Lambda functionality | Lambda functions running on AWS Snowball Edge devices can now be added, updated, removed, or replaced, once the devices are on\-premises\. In addition, AWS Snowball Edge devices can now be used as AWS Greengrass core devices\. For more information, see [Using AWS Lambda with an AWS Snowball Edge](using-lambda.md)\. | July 25, 2017 | 
| New AWS Region supported | AWS Snowball Edge is now supported in the Canada \(Central\) region, with region\-specific shipping options\. For more information, see [Shipping Considerations for AWS Snowball](shipping.md)\. | June 29, 2017 | 
| Updated file interface functionality | With the file interface, you can now choose the Network File System \(NFS\) clients that are allowed to access the file share on the Snowball Edge, in addition to accessing other support and troubleshooting features\. For more information, see [Using the File Interface for the AWS Snowball Edge](using-fileinterface.md)\. | June 21, 2017 | 
| Updated cluster functionality | Clusters can now be created in groups of 5–10 AWS Snowball Edge appliances\. For more information, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\. | June 5, 2017 | 
| Documentation update | Documentation navigation has been updated for clarity and consistency, and a regional limitations section has been added\. For more information, see [Regional Limitations for AWS Snowball](limits.md#region-limits)\. | May 8, 2017 | 
| Updated compute information | The following updates have been made for AWS Lambda powered by AWS Greengrass functions: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/doc-history.html) | December 6, 2016 | 
| Introducing AWS Snowball Edge | The AWS Snowball service now has two appliances, the standard Snowball and the AWS Snowball Edge appliance\. With the new Snowball Edge, you can now create local storage and compute jobs, harnessing the power of the AWS Cloud locally, without an internet connection\. | November 30, 2016 | 