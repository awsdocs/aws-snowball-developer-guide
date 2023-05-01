# Using Identity\-Based Policies \(IAM Policies\) for AWS Snowball<a name="access-control-managing-permissions"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. These policies thereby grant permissions to perform operations on AWS Snowball resources in the AWS Cloud\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Snowball resources\. For more information, see [Overview of Managing Access Permissions to Your Resources in the AWS Cloud](authentication-and-access-control.md#access-control-overview)\. 

The sections in this topic cover the following:
+  [Permissions Required to Use the AWS Snowball Console](#additional-console-required-permissions) 
+ [AWS\-Managed \(Predefined\) Policies for AWS Snowball Edge](authentication-and-access-control.md#access-policy-examples-aws-managed)
+ [Customer Managed Policy Examples](access-policy-examples-for-sdk-cli.md)

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

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permission\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\. 

For a table showing all of the AWS Snowball job management API actions and the resources that they apply to, see [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](access-policy-examples-for-sdk-cli.md#snowball-api-permissions-ref)\. 

## Permissions Required to Use the AWS Snowball Console<a name="additional-console-required-permissions"></a>

The permissions reference table lists the AWS Snowball job management API operations and shows the required permissions for each operation\. For more information about job management API operations, see [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](access-policy-examples-for-sdk-cli.md#snowball-api-permissions-ref)\. 

 To use the AWS Snow Family Management Console, you need to grant permissions for additional actions as shown in the following permissions policy: 

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
            "Resource": "arn:aws:lambda:*::function:*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "lambda:ListFunctions"
            ],
            "Resource": "*"
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
                "iam:PutRolePolicy"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "iam:PassedToService": "importexport.amazonaws.com"
                }
            }
        },
        {
           "Effect": "Allow",
           "Action": [
                "ec2:DescribeImages",
                "ec2:ModifyImageAttribute"
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
+ `ec2:` – These allow the user to describe Amazon EC2 instances and modify their attributes for local compute purposes\. For more information, see [Using Amazon EC2 Compute Instances](using-ec2.md)\.
+ `kms:` – These allow the user to create or choose the KMS key that will encrypt your data\. For more information, see [AWS Key Management Service in AWS Snowball Edge](kms.md)\.
+ `iam:` – These allow the user to create or choose an IAM role ARN that AWS Snowball will assume to access the AWS resources associated with job creation and processing\.
+ `sns:` – These allow the user to create or choose the Amazon SNS notifications for the jobs they create\. For more information, see [Notifications for the AWS Snowball Edge](notifications.md)\.