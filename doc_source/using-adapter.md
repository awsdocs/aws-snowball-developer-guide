--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using the Amazon S3 Adapter<a name="using-adapter"></a>

Following, you can find an overview of the Amazon S3 Adapter for Snowball, which allows you to programmatically transfer data to and from the AWS Snowball Edge appliance using Amazon S3 REST API actions\. This Amazon S3 REST API support is limited to a subset of actions\. You can use this subset of actions with one of the AWS SDKs to transfer data programmatically\. You can also use the subset of supported AWS Command Line Interface \(AWS CLI\) commands for Amazon S3 to transfer data programmatically\.

If your solution uses the AWS SDK for Java version 1\.11\.0 or newer, you must use the following `S3ClientOptions`:

+ `disableChunkedEncoding()` – Indicates that chunked encoding is not supported with the adapter\.

+ `setPathStyleAccess(true)` – Configures the adapter to use path\-style access for all requests\.

For more information, see [Class S3ClientOptions\.Builder](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/s3/S3ClientOptions.Builder.html) in the Amazon AppStream SDK for Java\.

**Important**  
We recommend that you only use one method of reading and writing data to a local bucket on an AWS Snowball Edge appliance at a time\. Using both the file interface and the Amazon S3 Adapter for Snowball on the same bucket at the same time can result in read/write conflicts\.

## Getting and Using Local Amazon S3 Credentials<a name="adapter-credentials"></a>

Every interaction with the AWS Snowball Edge appliance is signed with the AWS Signature Version 4 algorithm\. For more information on the algorithm, see [Signature Version 4 Signing Process](http://docs.aws.amazon.com/general/latest/gr/signature-version-4.html)\. When you start the Amazon S3 Adapter for Snowball, you specify the local Amazon S3 credentials that you want to use to sign this communication\.

You can get the local Amazon S3 credentials to sign your requests to the AWS Snowball Edge appliance by running the `snowballEdge credentials` Snowball client command\. For more information, see [Using the Snowball Client](using-client.md)\. These local Amazon S3 credentials include a pair of keys: an access key and a secret key\. These keys are only valid for the appliances associated with your job\. They can't be used in the AWS Cloud because they have no AWS Identity and Access Management \(IAM\) counterpart\.

You can add these permissions to the AWS credentials file on your server\. The default credential profiles file is typically located at `~/.aws/credentials`, but the location can vary per platform\. This file is shared by many of the AWS SDKs and by the AWS CLI\. You can save local credentials with a profile name as in the following example\.

```
[snowballEdge]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

The following example lets you execute support CLI commands with these local credentials\.

```
aws s3 ls --profile snowballEdge --endpoint http://192.0.2.0:8080
```