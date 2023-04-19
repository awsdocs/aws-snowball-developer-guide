# Choose security preferences<a name="set-security"></a>

Setting security adds the permissions and encryption settings for your AWS Snow Family devices job to help protect your data while in transit\.

**Topics**
+ [Restricting access to the Snow role policy](restricting-access.md)

**To set security for your job**

1. In the **Encryption** section, choose the **KMS key** that you want to use\.
   + If you want to use the default AWS Key Management Service \(AWS KMS\) key, choose **AWS/importexport \(default\)**\. This is the default key that protects your import and export jobs when no other key is defined\.
   + If you want to provide your own AWS KMS key, choose **Enter a key ARN**, provide the Amazon Resource Name \(ARN\) in the **key ARN** box, and choose **Use this KMS key**\. The key ARN will be added to the list\.

1.  In the **Service access** section, do one of the following:
   + Choose **Snow console will create and use a service\-linked role to access AWS resources on your behalf\.** to grant AWS Snow Family permissions to use Amazon S3 and Amazon Simple Notification Service \(Amazon SNS\) on your behalf\. The role grants AWS Security Token Service \(AWS STS\) AssumeRole trust to the Snow service
   + Choose **Add an existing service role to use**, to specify the **Role ARN** that you want, or you can use the default role\.

     For **Policy name**, choose the import policy that you want to use\.

     Add the `Condition` object and `aws:SourceAccount` or `aws:SourceARN` elements to the access policy to restrict the Snow service so that it acts as only one AWS account numbers\. Or add both to be most restrictive\.

     To restrict the Snow service so that it acts as only one or more account numbers, add one `aws:SourceAccount` element to the access policy and the account ID as the value\.

     To restrict the Snow service so that it acts as only one or more ARNs, add one `aws:SourceArn` element to the access policy and the ARN as the value\.  
**Example of `Condition` object to restrict Snow service actions**  

   Example of restricting Snow service actions by ARN and account IDs\.

   ```
       "Condition": {
           "StringEquals": {
               "aws:SourceAccount": "AWS_ACCOUNT_ID"
           }
           "ArnLike": {
               "aws:SourceArn": "arn:aws:snowball:REGION:AWS_ACCOUNT_ID:RESOURCE_ID"
           }
       }
   ```

   The following shows these conditions included in a policy\.

   ```
       {
       "Version": "2012-10-17",
       "Id": "__default_policy_ID",
       "Statement": [
           {
         "Sid": "__default_statement_ID",
         "Effect": "Allow",
         "Principal": {
         "AWS": "*"
         },
         "Action": [
           "SNS:GetTopicAttributes",
           "SNS:SetTopicAttributes",
           "SNS:AddPermission",
           "SNS:RemovePermission",
           "SNS:DeleteTopic",
           "SNS:Subscribe",
           "SNS:ListSubscriptionsByTopic",
           "SNS:Publish"
         ],
        "Resource": "arn:aws:sns:us-east-1:123456789012:my-sns-topic",
        "Condition": {
               "StringEquals": {
                   "aws:SourceAccount": "111122223333"
               },
               "ArnLike": {
                   "aws:SourceArn": "arn:aws:sns:us-east-1:555555555555:my-sns-topic"
               }
           }
       }
       ]
       }
   ```  
**Example policies for Snowball Edge devices**  

   The following is an example of an Amazon S3 import\-only role policy\.

   ```
   {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "s3:GetBucketPolicy",
                       "s3:GetBucketLocation",
                       "s3:ListBucketMultipartUploads",
                       "s3:ListBucket",
                       "s3:PutObject",
                       "s3:AbortMultipartUpload",
                       "s3:ListMultipartUploadParts",
                       "s3:PutObjectAcl",
                       "s3:GetObject"
                   ],
                   "Resource": [
                       "arn:aws:s3:::DOC-EXAMPLE-BUCKET1",
                       "arn:aws:s3:::DOC-EXAMPLE-BUCKET2/*"
                    ]
               }
           ]
       }
   ```

   ```
       {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "importexport.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

   The following is an example of an Amazon S3 export role policy\.

   ```
   {
           "Version": "2012-10-17",
           "Statement": [
               {
                   "Effect": "Allow",
                   "Action": [
                       "s3:GetBucketLocation",
                       "s3:GetObject",
                       "s3:ListBucket",
                       "s3:GetBucketPolicy"
                   ],
                   "Resource": [
                       "arn:aws:s3:::DOC-EXAMPLE-BUCKET3",
                       "arn:aws:s3:::DOC-EXAMPLE-BUCKET1/*"
                   ]
               }
           ]
       }
   ```

   ```
      
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "importexport.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```
**Note**  
 You can modify the trust relationship and restrict access to this role based on the customer account number and source arn\. See **[Restricting Access to the Snow Role Policy](restricting-access.md)** on how to modify the trust relationship to restrict access\.

1. Choose **Next\.** If the selected **IAM role ** has defined a restricted access, the **Create Job ** procedure will fail if the access criteria is not met\.

1. Choose **Allow**\.

1. Choose **Next**\.