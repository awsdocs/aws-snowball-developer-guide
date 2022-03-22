# Restricting Access to the Snow Role Policy<a name="restricting-access"></a>

You can restrict access to the selected role based on the customer account number and source arn\.

1. In the navigation pane of the IAM console, choose **Roles**\. The console displays the roles for your account\.

1. Choose the name of the role that you want to modify, and select the **Trust relationships** tab on the details page\.

1. Choose **Edit trust relationships**\. Update the trust policy to one of the following:

   To restrict access by **customer account number**:

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "importexport.amazonaws.com"
         },
         "Action": "sts:AssumeRole",
         "Condition":{
             "StringEquals":{
             "aws:SourceAccount":"<AWS_ACCOUNT_ID>"
             }
         }
       }
     ]
   }
   ```

   To restrict access by **source arn**:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [{
           "Effect": "Allow",
           "Principal": {
               "Service": "importexport.amazonaws.com"
           },
           "Action": "sts:AssumeRole",
           "Condition": {
               "ArnLike": {
                   "aws:SourceArn": "arn:aws:snowball:<REGION>:<AWS_ACCOUNT_ID>:<RESOURCE_ID>"
               }
           }
       }]
   }
   ```

   To restrict access by both **customer account number** and **source arn**:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [{
           "Effect": "Allow",
           "Principal": {
               "Service": "importexport.amazonaws.com"
           },
           "Action": "sts:AssumeRole",
           "Condition": {
               "StringEquals": {
                   "aws:SourceAccount": "<AWS_ACCOUNT_ID>"
               },
               "ArnLike": {
                   "aws:SourceArn": "arn:aws:snowball:<REGION>:<AWS_ACCOUNT_ID>:<RESOURCE_ID>"
               }
           }
       }]
   }
   ```