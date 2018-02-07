--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Troubleshooting for an AWS Snowball Edge<a name="troubleshooting"></a>

Following, you can find information to help you troubleshoot problems with an AWS Snowball Edge appliance\. If you have trouble establishing a connection to a Snowball, see [Why can’t my AWS Snowball appliance establish a connection with the network?](https://aws.amazon.com/premiumsupport/knowledge-center/troubleshoot-connect-snowball/) in the *AWS Knowledge Center*\. In addition, be aware of the following:

+ Objects in Amazon S3 have a maximum file size of 5 TB\.

+ Objects transferred onto AWS Snowball Edge appliances have a maximum key length of 933 bytes\. Key names that include characters that take up more than 1 byte each still have a maximum key length of 933 bytes\. When determining key length, you include the file or object name and also its path or prefixes\. Thus, files with short file names within a heavily nested path can have keys longer than 933 bytes\. The bucket name is not factored into the path when determining the key length\. Some examples follow\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/troubleshooting.html)

+ For security purposes, import and export jobs using an AWS Snowball Edge appliance must be completed within 120 days of the being prepared\. If you need to keep one or more devices for longer than 120 days, contact AWS Support\. Otherwise, after 120 days, the appliance becomes locked to additional on\-premises data transfers\. If the appliance becomes locked during a data transfer, return it and create a new job to transfer the rest of your data\. If the AWS Snowball Edge appliance becomes locked during an import job, we can still transfer the existing data on the appliance into Amazon S3\.

+ If you encounter unexpected errors using an AWS Snowball Edge appliance, we want to hear about it\. Make a copy of the relevant logs and include them along with a brief description of the issues that you encountered in a message to AWS Support\. For more information about logs, see [Commands for the Snowball Client](using-client-commands.md)\.

## Troubleshooting Connection Problems<a name="connection-troubleshooting"></a>

The following can help you troubleshoot issues you might have with connecting to your AWS Snowball Edge appliance: 

+ Routers and switches that work at a rate of 100 megabytes per second won't work with an AWS Snowball Edge appliance\. We recommend that you use a switch that works at a rate of 1 GB per second \(or faster\)\. 

## Troubleshooting Data Transfer Problems<a name="transfer-troubleshooting"></a>

If you encounter performance issues while transferring data to or from a Snowball Edge, see [Performance](BestPractices.md#performance) for recommendations and guidance on improving transfer performance\. The following can help you troubleshoot issues you might have with your data transfer to or from a Snowball Edge:

+ If you're using Linux and you can't upload files with UTF\-8 characters to an AWS Snowball Edge appliance, it might be because your Linux server doesn't recognize UTF\-8 character encoding\. You can correct this issue by installing the `locales` package on your Linux server and configuring it to use one of the UTF\-8 locales like `en_US.UTF-8`\. You can configure the `locales` package by exporting the environment variable `LC_ALL`, for example: `export LC_ALL=en_US.UTF-8`

+ If you're communicating with the AWS Snowball Edge appliance through the Amazon S3 Adapter for Snowball using the AWS CLI, and you encounter an error that says `Unable to locate credentials. You can configure credentials by running "aws configure".` you \\need to configure your AWS credentials used by the CLI to run commands\. For more information, see [Configuring the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) in the *AWS Command Line Interface User Guide*\.

+ When you use the Amazon S3 Adapter for Snowball with the AWS CLI, you can work with files or folders with spaces in their names, such as `my photo.jpg` or `My Documents.` However, make sure that you handle the spaces properly\. For more information, see [Specifying Parameter Values for the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-using-param.html) in the *AWS Command Line Interface User Guide*\.

## Troubleshooting Import Job Problems<a name="import-troubleshooting"></a>

Sometimes files fail to import into Amazon S3\. If the following issue occurs, try the actions specified to resolve your issue\. If a file fails import, you might need to try importing it again\. Importing it again might require a new job for Snowball Edge\.

**Files failed import into Amazon S3 due to invalid characters in object names**  
This problem occurs if a file or folder name has characters that aren't supported by Amazon S3\. Amazon S3 has rules about what characters can be in object names\. For more information, see [Object Key Naming Guidelines](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-key-guidelines)\.

**Action to take**  
If you encounter this issue, you see the list of files and folders that failed import in your job completion report\.

In some cases, the list is prohibitively large, or the files in the list are too large to transfer over the internet\. In these cases, you should create a new Snowball import job, change the file and folder names to comply with Amazon S3 rules, and transfer the files again\.

If the files are small and there isn't a large number of them, you can copy them to Amazon S3 through the AWS CLI or the AWS Management Console\. For more information, see [How Do I Upload Files and Folders to an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/upload-objects.html) in the *Amazon Simple Storage Service Console User Guide\.*

## Troubleshooting Export Job Problems<a name="export-troubleshooting"></a>

Sometimes files fail to export into your workstation\. If the following issue occurs, try the actions specified to resolve your issue\. If a file fails export, you might need to try exporting it again\. Exporting it again might require a new job for Snowball Edge\.

**Files failed export to a Microsoft Windows Server**  
A file can fail export to a Microsoft Windows Server if it or a related folder is named in a format not supported by Windows\. For example, if your file or folder name has a colon \(`:`\) in it, the export fails because Windows doesn't allow that character in file or folder names\.

**Action to take**

1. Make a list of the names that are causing the error\. You can find the names of the files and folders that failed export in your logs\. For more information, see [AWS Snowball Edge Logs](using-client-commands.md#logs)\.

1. Change the names of the objects in Amazon S3 that are causing the issue to remove or replace the unsupported characters\.

1. If the list of names is prohibitively large, or if the files in the list are too large to transfer over the internet, create a new export job specifically for those objects\.

   If the files are small and there isn't a large number of them, copy the renamed objects from Amazon S3 through the AWS CLI or the AWS Management Console\. For more information, see [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) in the* Amazon Simple Storage Service Console User Guide\.*