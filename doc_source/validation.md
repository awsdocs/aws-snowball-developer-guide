# Data Validation with Snowball Edge Jobs<a name="validation"></a>

Following, you'll find information about how AWS Snowball Edge validates data transfers, and the manual steps you can take to help ensure data integrity during and after a job\.

**Topics**
+ [Checksum Validation of Transferred Data](#snowball-edge-checksums)
+ [Local Inventory Creation During Snowball Transfer](#local-inventory-creation-during-snowball-transfer)
+ [Common Validation Errors](#validation-error-causes)
+ [Manual Data Validation for Snowball Edge After Import into Amazon S3](#manual-validation-s3)

## Checksum Validation of Transferred Data<a name="snowball-edge-checksums"></a>

When you copy a file from a local data source using the Amazon S3 interface to the Snowball Edge, a number of checksums are created\. These checksums are used to automatically validate data as it's transferred\.

At a high level, these checksums are created for each file \(or for parts of large files\)\. For the Snowball Edge, these checksums are visible when you run the following AWS CLI command against a bucket on the device\. The checksums are used to validate the integrity of your data throughout the transfers and help ensure that your data is copied correctly\.

```
aws s3api list-objects --bucket bucket-name --endpoint http://ip:8080 --profile edge-profile
```

When these checksums don't match, the associated data is not imported into Amazon S3\.

## Local Inventory Creation During Snowball Transfer<a name="local-inventory-creation-during-snowball-transfer"></a>

Create a local inventory of files copied to the Snowball when using the Amazon S3 adapter or CLI\. The content of the local inventory can be used to compare with what is on the local storage or server\. 

For example,

```
aws s3 cp folder/ s3://bucket --recursive > inventory.txt
```

## Common Validation Errors<a name="validation-error-causes"></a>

 When a validation error occurs, the corresponding data \(a file or a part of a large file\) is not written to the destination\. The following are common causes for validation errors:
+ Trying to copy symbolic links\.
+ Trying to copy files that are actively being modified\. The attempt fails checksum validation and is marked as a failed transfer\.
+ Trying to copy files that are larger than 5 TB in size\.
+ Trying to copy part sizes that are larger than 512 MB in size\.
+ Trying to copy files to a Snowball Edge device that is already at full data storage capacity\.
+ Trying to copy files to a Snowball Edge device that doesn't follow the [object key naming guidelines](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-key-guidelines) for Amazon S3\.

When any one of these validation errors occurs, it is logged\. You can take steps to manually identify what files failed validation and why\. For information, see [Manual Data Validation for Snowball Edge After Import into Amazon S3](#manual-validation-s3)\. 

## Manual Data Validation for Snowball Edge After Import into Amazon S3<a name="manual-validation-s3"></a>

After an import job has completed, you have several options to manually validate the data in Amazon S3, as described following\.

**Check job completion report and associated logs**  
Whenever data is imported into or exported out of Amazon S3, you get a downloadable PDF job report\. For import jobs, this report becomes available at the end of the import process\. For more information, see [Getting your job completion report and logs on the console](report.md)\.

**S3 inventory**  
If you transferred a huge amount of data into Amazon S3 in multiple jobs, going through each job completion report might not be an efficient use of time\. Instead, you can get an inventory of all the objects in one or more Amazon S3 buckets\. Amazon S3 inventory provides a comma\-separated values \(CSV\) file showing your objects and their corresponding metadata on a daily or weekly basis\. This file covers objects for an Amazon S3 bucket or a shared prefix \(that is, objects that have names that begin with a common string\)\.

When you have the inventory of the Amazon S3 buckets that you've imported data into, you can easily compare it against the files that you transferred on your source data location\. In this way, you can quickly identify what files where not transferred\.

**Use the Amazon S3 sync command**  
If your workstation can connect to the internet, you can do a final validation of all your transferred files by running the AWS CLI command `aws s3 sync`\. This command syncs directories and S3 prefixes\. This command recursively copies new and updated files from the source directory to the destination\. For more information, see [sync](https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html) in the *AWS CLI Command Reference*\.

**Important**  
If you specify your local storage as the destination for this command, make sure that you have a backup of the files that you sync against\. These files are overwritten by the contents in the specified Amazon S3 source\.