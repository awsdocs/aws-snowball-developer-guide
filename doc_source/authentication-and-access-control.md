# Access Control for Snow Family Console and Creating Jobs<a name="authentication-and-access-control"></a>

As with all AWS services, access to AWS Snowball requires credentials that AWS can use to authenticate your requests\. Those credentials must have permissions to access AWS resources, such an Amazon S3 bucket or an AWS Lambda function\. AWS Snowball differs in two ways:

1. Jobs in AWS Snowball do not have Amazon Resource Names \(ARNs\)\.

1. Physical and network access control for a device on\-premises is your responsibility\.

See [Identity and Access Management for AWS Snowball](security-iam.md) for details on how you can use [AWS Identity and Access Management \(IAM\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/) and AWS Snowball to help secure your resources by controlling who can access them in the AWS Cloud, and also local access control recommendations\.

## Overview of Managing Access Permissions to Your Resources in the AWS Cloud<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\. 

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

**Topics**
+ [Resources and Operations](#access-control-resources)
+ [Understanding Resource Ownership](#access-control-owner)
+ [Managing Access to Resources in the AWS Cloud](#access-control-manage-access-intro)
+ [Specifying Policy Elements: Actions, Effects, and Principals](#access-control-specify-actions)
+ [Specifying Conditions in a Policy](#specifying-conditions)

### Resources and Operations<a name="access-control-resources"></a>

In AWS Snowball, the primary resource is a *job*\. AWS Snowball also has devices like the Snowball and the AWS Snowball Edge device, however, you can only use those devices in the context of an existing job\. Amazon S3 buckets and Lambda functions are resources of Amazon S3 and Lambda respectively\.

As mentioned previously, jobs don't have Amazon Resource Names \(ARNs\) associated with them\. However, other services' resources, like Amazon S3 buckets, do have unique \(ARNs\) associated with them as shown in the following table\.


| Resource Type | ARN Format | 
| --- | --- | 
| S3 bucket | arn:aws:s3:region:account\-id:BucketName/ObjectName | 

AWS Snowball provides a set of operations to create and manage jobs\. For a list of available operations, see the [AWS Snowball API Reference](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\.

### Understanding Resource Ownership<a name="access-control-owner"></a>

The AWS account owns the resources that are created in the account, regardless of who created the resources\. Specifically, the resource owner is the AWS account of the [principal entity](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html) \(that is, the root account, an IAM user, or an IAM role\) that authenticates the resource creation request\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create a S3 bucket, your AWS account is the owner of the resource \(in AWS Snowball, the resource is the job\)\.
+ If you create an IAM user in your AWS account and grant permissions to create a job to that user, the user can create a job\. However, your AWS account, to which the user belongs, owns the job resource\.
+ If you create an IAM role in your AWS account with permissions to create a job, anyone who can assume the role can create a job\. Your AWS account, to which the role belongs, owns the job resource\. 

### Managing Access to Resources in the AWS Cloud<a name="access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of AWS Snowball\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM polices\) and policies attached to a resource are referred to as *resource\-based* policies\. AWS Snowball supports only identity\-based policies \(IAM policies\)\. 

**Topics**
+ [Resource\-Based Policies](#access-control-manage-access-intro-resource-policies)

#### Resource\-Based Policies<a name="access-control-manage-access-intro-resource-policies"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS Snowball doesn't support resource\-based policies\. 

### Specifying Policy Elements: Actions, Effects, and Principals<a name="access-control-specify-actions"></a>

For each job \(see [Resources and Operations](#access-control-resources)\), the service defines a set of API operations \(see [AWS Snowball API Reference](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\) to create and manage said job\. To grant permissions for these API operations, AWS Snowball defines a set of actions that you can specify in a policy\. For example, for a job, the following actions are defined: `CreateJob`, `CancelJob`, and `DescribeJob`\. Note that, performing an API operation can require permissions for more than one action\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [Resources and Operations](#access-control-resources)\.
**Note**  
This is supported for Amazon S3, Amazon EC2, AWS Lambda, AWS KMS, and many other services\.  
Snowball does not support specifying a resource ARN in the `Resource` element of an IAM policy statement\. To allow access to Snowball, specify `“Resource”: “*”` in your policy\.
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, depending on the specified `Effect`, `snowball:*` either allows or denies the user permissions to perform all operations\.
**Note**  
This is supported for Amazon EC2, Amazon S3, and IAM\.
+ **Effect** – You specify the effect when the user requests the specific action—this can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
**Note**  
This is supported for Amazon EC2, Amazon S3, and IAM\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. AWS Snowball doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the AWS Snowball API actions, see [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](access-policy-examples-for-sdk-cli.md#snowball-api-permissions-ref)\.

### Specifying Conditions in a Policy<a name="specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\. 

To express conditions, you use predefined condition keys\. There are no condition keys specific to AWS Snowball\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

## AWS\-Managed \(Predefined\) Policies for AWS Snowball Edge<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

You can use the following AWS\-managed policies with AWS Snowball\.

### Creating an IAM Role Policy for Snowball Edge<a name="create-iam-role"></a>

An IAM role policy must be created with read and write permissions for your Amazon S3 buckets\. The IAM role must also have a trust relationship with Snowball\. Having a trust relationship means that AWS can write the data in the Snowball and in your Amazon S3 buckets, depending on whether you're importing or exporting data\.

When you create a job in the AWS Snow Family Management Console, creating the necessary IAM role occurs in step 4 in the **Permission** section\. This process is automatic\. The IAM role that you allow Snowball to assume is only used to write your data to your bucket when the Snowball with your transferred data arrives at AWS\. The following procedure outlines that process\.

**To create the IAM role for your import job**

1. Sign in to the AWS Management Console and open the AWS Snowball console at [https://console\.aws\.amazon\.com/importexport/](https://console.aws.amazon.com/importexport/)\. 

1. Choose **Create job**\.

1. In the first step, fill out the details for your import job into Amazon S3, and then choose **Next**\.

1. In the second step, under **Permission**, choose **Create/Select IAM Role**\.

   The IAM Management Console opens, showing the IAM role that AWS uses to copy objects into your specified Amazon S3 buckets\.

1. Review the details on this page, and then choose **Allow**\.

   You return to the AWS Snow Family Management Console, where **Selected IAM role ARN** contains the Amazon Resource Name \(ARN\) for the IAM role that you just created\.

1. Choose **Next** to finish creating your IAM role\.

The preceding procedure creates an IAM role that has write permissions for the Amazon S3 buckets that you plan to import your data into\. The IAM role that is created has one of the following structures, depending on whether it's for an import job or export job\.

**IAM Role for an Import Job**

```
          {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetBucketLocation",
        "s3:ListBucketMultipartUploads"
      ],
      "Resource": "arn:aws:s3:::*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetBucketPolicy",
        "s3:PutObject",
        "s3:AbortMultipartUpload",
        "s3:ListMultipartUploadParts",
        "s3:PutObjectAcl"
      ],
      "Resource": "arn:aws:s3:::*"
    }
  ]
}
```

If you use server\-side encryption with AWS KMS–managed keys \(SSE\-KMS\) to encrypt the Amazon S3 buckets associated with your import job, you also need to add the following statement to your IAM role\.

```
{
     "Effect": "Allow",
     "Action": [
       "kms:GenerateDataKey"
     ],
     "Resource": "arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

If the object sizes are larger, the Amazon S3 client that is used for the import process uses multipart upload\. If you initiate a multipart upload using SSE\-KMS, then all the uploaded parts are encrypted using the specified AWS KMS key\. Because the parts are encrypted, they must be decrypted before they can be assembled to complete the multipart upload\. So you must have permission to decrypt the AWS KMS key \(`kms:Decrypt`\) when you run a multipart upload to Amazon S3 with SSE\-KMS\.

The following is an example of an IAM role needed for an import job that needs `kms:Decrypt` permission\.

```
{
    "Effect": "Allow",
     "Action": [
       "kms:GenerateDataKey","kms:Decrypt"

     ],
     "Resource": "arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

 The following is an example of an IAM role needed for an export job\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetBucketLocation",
        "s3:GetBucketPolicy",
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::*"
    }
  ]
}
```

If you use server\-side encryption with AWS KMS–managed keys to encrypt the Amazon S3 buckets associated with your export job, you also need to add the following statement to your IAM role\.

```
{
     "Effect": "Allow",
     "Action": [
            “kms:Decrypt”
      ],
     "Resource": "arn:aws:kms:us-west-2:123456789012:key/abc123a1-abcd-1234-efgh-111111111111"
}
```

You can create your own custom IAM policies to allow permissions for API operations for AWS Snowball job management\. You can attach these custom policies to the IAM users or groups that require those permissions\. 