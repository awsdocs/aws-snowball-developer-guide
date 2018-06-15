--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using Identity\-Based Policies \(IAM Policies\) for AWS Snowball<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on AWS Snowball resources in the AWS Cloud\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Snowball resources\. For more information, see [Overview of Managing Access Permissions to Your Resources in the AWS Cloud](access-control-overview.md)\. 

The sections in this topic cover the following:
+  [Permissions Required to Use the AWS Snowball Console](#additional-console-required-permissions) 
+ [AWS Managed \(Predefined\) Policies for AWS Snowball](#access-policy-examples-aws-managed)
+ [Customer Managed Policy Examples](#access-policy-examples-for-sdk-cli)

The following shows an example of a permissions policy\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetBucketLocation",
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::*"
    },
    {
       "Effect": "Allow",
       "Action": [
          "snowball:*",
          "importexport:*"
       ],
       "Resource": "*"
    }
  ]
}
```

The policy has two statements:
+ The first statement grants permissions for three Amazon S3 actions \(`s3:GetBucketLocation`, `s3:GetObject`, and `s3:ListBucket`\) on all Amazon S3 buckets using the *Amazon Resource Name \(ARN\)* of `arn:aws:s3:::*`\. The ARN specifies a wildcard character \(\*\) so the user can choose any or all Amazon S3 buckets to export data from\.
+ The second statement grants permissions for all AWS Snowball actions\. Because these actions don't support resource\-level permissions, the policy specifies the wildcard character \(\*\) and the `Resource` value also specifies a wild card character\.

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permission\. When you attach policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. 

For a table showing all of the AWS Snowball job management API actions and the resources that they apply to, see [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](snowball-api-permissions-ref.md)\. 

## Permissions Required to Use the AWS Snowball Console<a name="additional-console-required-permissions"></a>

The permissions reference table lists the AWS Snowball job management API operations and shows the required permissions for each operation\. For more information about job management API operations, see [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](snowball-api-permissions-ref.md)\. 

 To use the AWS Snowball Management Console, you need to grant permissions for additional actions as shown in the following permissions policy: 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetBucketLocation",
                "s3:GetBucketPolicy",
                "s3:ListBucket",
                "s3:ListBucketMultipartUploads",
                "s3:ListAllMyBuckets"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:CreateBucket",
                "s3:PutObject",
                "s3:AbortMultipartUpload",
                "s3:ListMultipartUploadParts",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:GetFunction",
                "lambda:GetFunctionConfiguration"
            ],
            "Resource": "arn:aws:lambda:::function:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:ListFunctions"
            ],
            "Resource": "arn:aws:lambda:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "kms:CreateGrant",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:RetireGrant",
                "kms:ListKeys",
                "kms:DescribeKey",
                "kms:ListAliases"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:AttachRolePolicy",
                "iam:CreatePolicy",
                "iam:CreateRole",
                "iam:ListRoles",
                "iam:ListRolePolicies",
                "iam:PutRolePolicy",
                "iam:PassRole"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "sns:CreateTopic",
                "sns:ListTopics",
                "sns:GetTopicAttributes",
                "sns:SetTopicAttributes",
                "sns:ListSubscriptionsByTopic",
                "sns:Subscribe"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "greengrass:getServiceRoleForAccount"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "snowball:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

The AWS Snowball console needs these additional permissions for the following reasons:
+ `lambda:` – These allow the user to select Lambda functions for local compute purposes\. For more information, see [Using AWS Lambda with an AWS Snowball Edge](using-lambda.md)\.
+ `kms:` – These allow the user to create or choose the KMS key that will encrypt your data\. For more information, see [AWS Key Management Service in AWS Snowball](kms.md)\.
+ `iam:` – These allow the user to create or choose an IAM role ARN that AWS Snowball will assume to access the AWS resources associated with job creation and processing\.
+ `sns:` – These allow the user to create or choose the Amazon SNS notifications for the jobs they create\. For more information, see [Notifications for the AWS Snowball Edge](notifications.md)\.

## AWS Managed \(Predefined\) Policies for AWS Snowball<a name="access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. There are no AWS managed policies for AWS Snowball\.

You can create your own custom IAM policies to allow permissions for AWS Snowball job management API actions\. You can attach these custom policies to the IAM users or groups that require those permissions\. 

## Customer Managed Policy Examples<a name="access-policy-examples-for-sdk-cli"></a>

In this section, you can find example user policies that grant permissions for various AWS Snowball job management actions\. These policies work when you are using AWS SDKs or the AWS CLI\. When you are using the console, you need to grant additional permissions specific to the console, which is discussed in [Permissions Required to Use the AWS Snowball Console](#additional-console-required-permissions)\.

**Note**  
All examples use the us\-west\-2 region and contain fictitious account IDs\.

**Topics**
+ [Example 1: Role Policy That Allows a User to Create a Job with the API](#access-policy-example-create-api)
+ [Example 2: Role Policy for Creating Import Jobs](#role-policy-example-import)
+ [Example 3: Role Policy for Creating Export Jobs](#role-policy-example-export)

### Example 1: Role Policy That Allows a User to Create a Job with the API<a name="access-policy-example-create-api"></a>

The following permissions policy is a necessary component of any policy that is used to grant job or cluster creation permission using the job management API\. The user also needs some or all of the permissions specified in [Permissions Required to Use the AWS Snowball Console](#additional-console-required-permissions), depending on the type of job created\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "Service": "importexport.amazonaws.com"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "sts:ExternalId": "AWSIE"
        }
      }
    }
  ]
}
```

### Example 2: Role Policy for Creating Import Jobs<a name="role-policy-example-import"></a>

You use the following role trust policy for creating import jobs for Snowball Edge that use AWS Lambda powered by AWS Greengrass functions\.

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
        },
        {
            "Effect": "Allow",
            "Action": [
                "snowball:*"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iot:AttachPrincipalPolicy",
                "iot:AttachThingPrincipal",
                "iot:CreateKeysAndCertificate",
                "iot:CreatePolicy",
                "iot:CreateThing",
                "iot:DescribeEndpoint",
                "iot:GetPolicy"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:GetFunction"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "greengrass:CreateCoreDefinition",
                "greengrass:CreateDeployment",
                "greengrass:CreateDeviceDefinition",
                "greengrass:CreateFunctionDefinition",
                "greengrass:CreateGroup",
                "greengrass:CreateGroupVersion",
                "greengrass:CreateLoggerDefinition",
                "greengrass:CreateSubscriptionDefinition",
                "greengrass:GetDeploymentStatus",
                "greengrass:UpdateGroupCertificateConfiguration",
                "greengrass:CreateGroupCertificateAuthority",
                "greengrass:GetGroupCertificateAuthority",
                "greengrass:ListGroupCertificateAuthorities",
                "greengrass:ListDeployments", 
                "greengrass:GetGroup", 
                "greengrass:GetGroupVersion", 
                "greengrass:GetCoreDefinitionVersion"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Example 3: Role Policy for Creating Export Jobs<a name="role-policy-example-export"></a>

You use the following role trust policy for creating export jobs for Snowball Edge that use AWS Lambda powered by AWS Greengrass functions\.

```
                    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetBucketLocation",
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::*"
        },
        {
           "Effect": "Allow",
           "Action": [
                "snowball:*"
           ],
           "Resource": [
                "*"
           ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iot:AttachPrincipalPolicy",
                "iot:AttachThingPrincipal",
                "iot:CreateKeysAndCertificate",
                "iot:CreatePolicy",
                "iot:CreateThing",
                "iot:DescribeEndpoint",
                "iot:GetPolicy"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:GetFunction"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "greengrass:CreateCoreDefinition",
                "greengrass:CreateDeployment",
                "greengrass:CreateDeviceDefinition",
                "greengrass:CreateFunctionDefinition",
                "greengrass:CreateGroup",
                "greengrass:CreateGroupVersion",
                "greengrass:CreateLoggerDefinition",
                "greengrass:CreateSubscriptionDefinition",
                "greengrass:GetDeploymentStatus",
                "greengrass:UpdateGroupCertificateConfiguration",
                "greengrass:CreateGroupCertificateAuthority",
                "greengrass:GetGroupCertificateAuthority",
                "greengrass:ListGroupCertificateAuthorities",
                "greengrass:ListDeployments", 
                "greengrass:GetGroup", 
                "greengrass:GetGroupVersion", 
                "greengrass:GetCoreDefinitionVersion"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```