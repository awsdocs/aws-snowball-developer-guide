--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Authorization with the Amazon S3 API Adapter for AWS Snowball<a name="auth-adapter"></a>

When you use the Amazon S3 Adapter for Snowball, every interaction is signed with the AWS Signature Version 4 algorithm by default\. This authorization is used only to verify the data traveling from its source to the adapter\. All encryption and decryption happens on the appliance\. Unencrypted data is never stored on the appliance\.

When using the adapter, keep the following in mind:

+ To get the local Amazon S3 credentials to sign your requests to the AWS Snowball Edge appliance, run the `snowballEdge credentials` Snowball client command\. For more information, see [Using the Snowball Client](using-client.md)\. These local Amazon S3 credentials include a pair of keys: an access key and a secret key\. These keys are only valid for the appliances associated with your job\. They can't be used in the AWS Cloud as they have no IAM counterpart\.

+ The encryption key is not changed by what AWS credentials you use\. Because signing with the Signature Version 4 algorithm is only used to verify the data traveling from its source to the adapter, it never factors into the encryption keys used to encrypt your data on the Snowball\.