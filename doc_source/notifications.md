# Notifications for the AWS Snowball Edge<a name="notifications"></a>

The AWS Snowball Edge device is designed to take advantage of the robust notifications delivered by Amazon Simple Notification Service \(Amazon SNS\)\. While creating a job, you can provide a list of comma\-separated email addresses to receive email notifications for your job\.

You configure Amazon SNS to send text messages for these status notifications from the Amazon SNS console\. For more information, see [Mobile text messaging \(SMS\)](https://docs.aws.amazon.com/sns/latest/dg/SMSMessages.html) in the *Amazon Simple Notification Service Developer Guide*\.

After you create your job, every email address that you specified to get Amazon SNS notifications receives an email from AWS notifications asking for confirmation to the topic subscription\. For each email address to receive additional notifications, a user of the account must confirm the subscription by choosing **Confirm subscription**\.

The Amazon SNS notification emails are tailored for each triggering state, and include a link to the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\.