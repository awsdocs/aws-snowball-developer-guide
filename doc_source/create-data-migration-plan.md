# Creating a Large Data Migration Plan<a name="create-data-migration-plan"></a>

The AWS Snow Family large data migration plan feature enables you to plan, track, monitor, and manage large data migrations from 500 TB to multiple petabytes when using multiple Snow Family service products\.

Use the large data migration plan feature to collect information about data migration goals, such as the size of the data to move to AWS and the number of Snow Family devices needed to migrate the data simultaneously\. Use the plan to create a projected schedule for your data migration project and the recommended job ordering schedule to meet your goals\.

**To create a large data migration plan**
**Note**  
The data migration plan is supported for import job use cases only\.

1. Sign in to the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. If this is your first time using Snow Family in this AWS Region, you will see the AWS Snow Family page\. Otherwise, you will see the list of pre\-existing jobs\. 

1. If this is your first data migration plan, choose **Create your large data migration plan** for migrations larger than 500 TB from the main page\. Otherwise, choose **Large data migration plan** from the left navigation bar\. Choose **Create data migration plan** to open the plan creation wizard\. 

1. In the **Name your data migration plan** section, provide a name for the plan in the **Data migration plan name** box\. The plan name can have up to 64 characters\. Valid characters are A\-Z, a\-z, 0\-9, and \. \- \(hyphen\)\. A plan name must not start with aws:\.

1. In the **Shipping Address** section, choose an existing address or create a new one\.
   + If you choose **Use recent address**, the addresses on file are displayed\. Choose the address you want from the list\.
   + If you choose **Add a new address**, provide the requested address information\. The AWS Snow Family Management Console saves your new shipping information\.
**Note**  
The country in the address must match the destination country for the device, and must be valid for that country\.

1. In **Concurrent devices**, enter the number of Snow Family devices that you can simultaneously copy data on your premises

1. In **Total data to be migrated to AWS**, enter the size of the data that you want to migrate to AWS\. A large data migration plan is only allowed for data migrations larger than 500 TB\. Place Snow Family job orders individually for your data transfer project\.

1. In **Service Access**, do one of the following:
   + Allow Snow to create a new service\-linked role for you with all of the necessary permissions to publish CloudWatch metrics and Amazon SNS notifications for your Snow Family jobs\.
   + Or, add an existing service role that has the necessary permissions \. You can see an example of how to set up this role in [Example 4: Expected Role Permissions and Trust Policy](access-policy-examples-for-sdk-cli.md#expected-role-permissions-and-trust-policy)\.

1. In **Send notifications**, choose whether to send notifications\. Note that if you choose **Do not send notification about data migration plans**, you will not receive any notifications from the plan you are creating but you will still receive job notifications\.

1. In **Set notifications** section, do one of the following:
   + To use an existing topic, choose **Use an existing SNS topic**, and then choose the topic Amazon Resource Name \(ARN\) from the list\.
   + To create a new topic, choose **Create a new SNS topic**\. Enter a name for your topic and provide an email address\.

1.  Choose **Create data migration plan** to create the plan\.