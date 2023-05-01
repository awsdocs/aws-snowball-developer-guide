# Security<a name="best-practice-security"></a>

The following are recommendations and best practices for maintaining security while working with an AWS Snowball Edge device\.

**General Security**
+ If you notice anything that looks suspicious about the AWS Snowball Edge device, don't connect it to your internal network\. Instead, contact [AWS Support](https://aws.amazon.com/premiumsupport/), and a new AWS Snowball Edge device will be shipped to you\.
+ We recommend that you don't save a copy of the unlock code in the same location on the workstation as the manifest for that job\. Saving these in different locations helps prevent unauthorized parties from gaining access to the AWS Snowball Edge device\. For example, you can save a copy of the manifest to your local server, and email the code to a user that unlocks the device\. This approach limits access to the AWS Snowball Edge device to individuals who have access to files saved on the server and the user's email address\.
+ The credentials displayed, when you run the Snowball Edge client commands list\-access\-keys and get\-secret\-access\-key, are a pair of access keys used to access your device\.

  These keys are only associated with the job and the local resources on the device\. They don't map to your AWS account or any other AWS account\. If you try to use these keys to access services and resources in the AWS Cloud, they will fail because they only work for the local resources associated with your job\.
+ If you feel your credentials are lost or have been compromised, request a new manifest file and unlock code by following the process to update the device's SSL certificate\. See [Update the SSL certificate](updating-device.md#update-ssl-cert)\.

For information about how to use AWS Identity and Access Management \(IAM\) policies to control access, see [AWS\-Managed \(Predefined\) Policies for AWS Snowball Edge](authentication-and-access-control.md#access-policy-examples-aws-managed)\.

**Network Security**
+ We recommend that you only use one method at a time for reading and writing data to a local bucket on an AWS Snowball Edge device\. Using both the file interface and the Amazon S3 adapter on the same Amazon S3 bucket at the same time can result in read/write conflicts\.
+ To prevent corrupting your data, don't disconnect the AWS Snowball Edge device or change its network settings while transferring data\.
+ Files that are being written to on the device should be in a static state\. Files that are modified while they are being written to can result in read/write conflicts\.
+ For more information about improving performance of your AWS Snowball Edge device, see [Performance](performance.md)\.