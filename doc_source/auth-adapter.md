--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Authorization with the Amazon S3 API Adapter for AWS Snowball<a name="auth-adapter"></a>

When you use the Amazon S3 Adapter for Snowball, every interaction is signed with the AWS Signature Version 4 algorithm by default\. This authorization is used only to verify the data traveling from its source to the adapter\. All encryption and decryption happens on the device\. Unencrypted data is never stored on the device\.

When using the adapter, keep the following in mind:
+ To get the local Amazon S3 credentials to sign your requests to the AWS Snowball Edge device, run the `snowballEdge list-access-keys` and `snowballEdge get-secret-access-keys` Snowball client commands\. For more information, see [Using the Snowball Client](using-client.md)\. These local Amazon S3 credentials include a pair of keys: an access key and a secret key\. These keys are only valid for the devices associated with your job\. They can't be used in the AWS Cloud because they have no IAM counterpart\.
+ The encryption key is not changed by what AWS credentials you use\. Signing with the Signature Version 4 algorithm is only used to verify the data traveling from its source to the adapter\. Thus, this signing never factors into the encryption keys used to encrypt your data on the Snowball\.