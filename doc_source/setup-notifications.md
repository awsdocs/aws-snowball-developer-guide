# Choose your notification preferences<a name="setup-notifications"></a>

Notifications update you on the latest status of your AWS Snow Family devices jobs\. You create an SNS topic and receive emails from Amazon Simple Notification Service \(Amazon SNS\) as your job status changes\.

**To set up notifications**
+  In the **Set notifications** section, do one of the following:
  + If you want to use an existing SNS topic, choose **Use an existing SNS topic**, and choose the topic Amazon Resource Name \(ARN\) from the list\.
  + If you want to create a new SNS topic, choose **Create a new SNS topic**\. Enter a name for your topic and provide an email address\.

The notification will be about one of the following states of your job:
+ Job created
+ Preparing device
+ Preparing shipment
+ In transit to you
+ Delivered to you
+ In transit to AWS
+ At sorting facility
+ At AWS
+ Importing
+ Completed
+ Canceled