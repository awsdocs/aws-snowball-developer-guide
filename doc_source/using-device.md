# Using an AWS Snowball Edge Device<a name="using-device"></a>

Following, you can find an overview of the AWS Snowball Edge device\. Snowball Edge is a physically rugged device protected by AWS Key Management Service \(AWS KMS\) that you use for local storage and compute, or to transfer data between your on\-premises servers and Amazon Simple Storage Service \(Amazon S3\)\.

For information about unlocking an AWS Snowball Edge device, see [Using the Snowball Edge Client](using-client.md)\.

When the device first arrives, inspect it for damage or obvious tampering\.

**Warning**  
If you notice anything that looks suspicious about the device, don't connect it to your internal network\. Instead, contact [AWS Support](https://aws.amazon.com/premiumsupport/), and a new one will be shipped to you\.

The following image shows what the AWS Snowball Edge device looks like\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/Snowball-Edge-Image.png)

The device has three doors—a front, a back, and a top—that all can be opened by latches\. The top door contains the power cable for the device\. The other two doors can be opened and slid inside the device so that they're out of the way while you're using it\. By opening the doors, you get access to the LCD E Ink display embedded in the front side of the device, and the power and network ports in the back\.

After your device arrives and is powered on, you're ready to use it\.

**Topics**
+ [Using the Snowball Edge Client](using-client.md)
+ [Transferring files using the Amazon S3 adapter for data migration](using-adapter.md)
+ [Transferring Files to Snowball Edge devices using the File Interface](using-fileinterface.md)
+ [Using NFS for Offline Data Transfer](shared-using-nfs.md)
+ [Using an AWS Snowball Edge device with a Tape Gateway](using-snowball-tape-gateway.md)
+ [Using AWS IoT Greengrass to run pre\-installed software on Amazon EC2 instances](using-green-grass.md)
+ [Using Amazon EC2 Compute Instances](using-ec2.md)
+ [Using Amazon S3 compatible storage on Snow Family devices](s3compatible-on-snow.md)
+ [Using Amazon EKS Anywhere on AWS Snow](using-eksa.md)
+ [Using IAM Locally](using-local-iam.md)
+ [Using AWS Security Token Service](using-sts.md)
+ [Ports Required to Use AWS Services on an AWS Snowball Edge Device](port-requirements.md)