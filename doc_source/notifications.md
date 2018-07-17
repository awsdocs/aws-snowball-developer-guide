--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Notifications for the AWS Snowball Edge<a name="notifications"></a>

Like the standard Snowball, the AWS Snowball Edge device is designed to take advantage of the robust notifications delivered by Amazon Simple Notification Service \(Amazon SNS\)\. While creating a job, you can provide a list of comma\-separated email addresses to receive email notifications for your job\.

You can also choose from the status list which job status values trigger these notifications\. For more information about the different job status values, see [Job Statuses](jobstatuses.md)\.

You can configure Amazon SNS to send text messages for these status notifications from the Amazon SNS console\. For more information, see [Sending and Receiving SMS Notifications Using Amazon SNS](http://docs.aws.amazon.com/sns/latest/dg/SMSMessages.html)\.

**Note**  
These notifications are optional, and are free if you're within your first million Amazon SNS requests for the month\. For more information about Amazon SNS pricing, see [https://aws.amazon.com/sns/pricing](https://aws.amazon.com/sns/pricing)\.

After you create your job, every email address that you specified to get Amazon SNS notifications receives an email from AWS Notifications asking for confirmation to the topic subscription\. For each email address to receive additional notifications, a user of the account must confirm the subscription by choosing **Confirm subscription**\.

The Amazon SNS notification emails are tailored for each triggering state, and include a link to the [AWS Snowball Management Console](https://console.aws.amazon.com/importexport/home?region=us-west-2)\.