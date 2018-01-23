--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Getting Started with Lambda Powered by AWS Greengrass<a name="function-getting-started"></a>

To get started with AWS Lambda powered by AWS Greengrass functions on a Snowball Edge, take the following steps:

1. [Associating an AWS Greengrass Service Role with Your Account](#gg-associate-role)

1. [Configuring AWS Greengrass with a Snowball Edge](#gg-config)

1. [Creating Your Job](#function-create-job)

1. [Using Lambda Powered by AWS Greengrass Functions on a Snowball Edge](#use-functions)

## Associating an AWS Greengrass Service Role with Your Account<a name="gg-associate-role"></a>

Before you can use AWS Greengrass with a Snowball Edge as a core device, you must associate an AWS Greengrass service role with your account\. This association allows AWS Greengrass to access your Lambda functions and AWS IoT resources\. If you try to create a job for a Snowball Edge before you associate the service role, the job creation request fails\.

The following procedures show how to configure and store your AWS Greengrass settings in the cloud\. This configuration means that you can push Lambda function changes to the Snowball Edge and changes to other devices in your AWS Greengrass group\. The first procedure uses the AWS Identity and Access Management \(IAM\) console, and the second procedure uses the AWS Command Line Interface \(AWS CLI\)\. 

**To create an AWS Greengrass service role in the IAM console**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. For **Role Type**, choose **AWS Greengrass Role**\.

1. Select **AWSGreengrassResourceAccessPolicy**, and then choose **Next Step**\.

1. Type a name for your role, and then choose **Create Role**\.

After creating the role, make a note of the role Amazon Resource Name \(ARN\), and use it in the next procedure\.

**To associate the AWS Greengrass service role with your account**

1. Install the AWS CLI on your computer, if you haven't already\. For more information, see [Installing the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the *AWS Command Line Interface User Guide*\.

1. Configure the AWS CLI on your computer, if you haven't already\. For more information, see [Configuring the AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) in the *AWS Command Line Interface User Guide*\.

1. Open a terminal on your computer and run the following AWS CLI command, with the AWS Greengrass role ARN you created in the first procedure\.

   ```
   aws greengrass associate-service-role-to-account --role-arn arn:aws:iam::123EXAMPLE12:role/GreengrassRole
   ```

Now you can create a job for a Snowball Edge and use AWS Lambda powered by AWS Greengrass\.

## Configuring AWS Greengrass with a Snowball Edge<a name="gg-config"></a>

When you create a compute job for a Snowball Edge, the service automatically configures the following AWS Greengrass elements:

+ **AWS Greengrass Core Software** – The AWS Greengrass distributable has been pre\-installed on the Snowball Edge\.

+ **AWS Greengrass Group** – When you create a compute job, an AWS Greengrass group named `JobID_group` is created and provisioned\. The core of this group is named `JobID_core`, and it has a device in it named `JobID_s3adapter`\. The Amazon S3 Adapter for Snowball is registered as an IoT device in your AWS Greengrass group\. This registration is because the adapter sends MQTT messages for every Amazon S3 PUT object action for the buckets on the Snowball Edge\.

If you have other configuration changes that you want to make for the AWS Greengrass group associated with a Snowball Edge, you can make them after you unlock the device and connect it to the internet\.

## Creating Your Job<a name="function-create-job"></a>

Create a job in the AWS Snowball Management Console and associate the Amazon Resource Name \(ARN\) for at least one published Lambda function with a bucket\. For a walkthrough on creating your first job, see [Getting Started with AWS Snowball Edge: Your First Job](common-get-start.md)\. 

All the Lambda functions that you choose during job creation are triggered by MQTT messages sent by the IoT device associated with the Amazon S3 Adapter for Snowball\. These MQTT messages are triggered whenever an [Amazon S3 PUT object](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUT.html) action is made against the bucket on the AWS Snowball Edge appliance\.

## Connecting to the Internet to Update AWS Greengrass Group Certificates<a name="function-update-certs"></a>

When the Snowball Edge arrives, unlock the device, and then connect it to the internet for at least one minute\. Connecting the device to the internet allows the AWS Greengrass service in the cloud to send the AWS Greengrass certificates that are needed to operate the Snowball Edge\. After that, you can disconnect the device from the internet\. The associated AWS Greengrass group then functions in offline mode\.

**Important**  
When the IP address for any device in the local AWS Greengrass group changes, reconnect the Snowball Edge to the internet so it can get new certificates\.

## Using Lambda Powered by AWS Greengrass Functions on a Snowball Edge<a name="use-functions"></a>

Unless programmed otherwise, Lambda functions are triggered by MQTT messages sent by the IoT device associated with the Amazon S3 Adapter for Snowball\. These MQTT messages are in turn triggered by Amazon S3 PUT object actions\. Amazon S3 PUT object actions occur through the file interface \(with a write operation\), the AWS CLI \(using the Amazon S3 Adapter for Snowball\), or programmatically through one of the SDKs or a REST application of your own design\.

You can use your AWS Lambda powered by AWS Greengrass functions to execute Python code against public endpoints among AWS services in the cloud\. For this Python code execution to work, your AWS Snowball Edge appliance needs to be connected to the internet\. For more information, see the [AWS Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/)\.

### Updating Existing Functions<a name="update-functions"></a>

You can update existing Lambda functions in the console\. If you do, and if your AWS Snowball Edge appliance is connected to the internet, a deployment agent notifies each Lambda function of the updated AWS Greengrass group configuration\. For more information, see [Create a Deployment](http://docs.aws.amazon.com/lambda/latest/dg/create-deployment.html) in the *AWS Greengrass Developer Guide*\.

### Adding New Functions<a name="add-new-functions"></a>

After your Snowball Edge arrives and you unlock it and connect it to the internet, you can add or remove additional Lambda functions\. These new Lambda functions don't have to be triggered by Amazon S3 PUT object actions\. Instead, the event that you programmed to trigger the new functions performs function triggering, as with typical Lambda functions running in an AWS Greengrass group\. 

### Testing Lambda Powered by AWS Greengrass Functions<a name="testing-functions"></a>

While testing your Python\-coded function in the Lambda console, you might encounter errors\. If that happens, see [Retries on Errors](http://docs.aws.amazon.com/lambda/latest/dg/retries-on-errors.html) in the *AWS Lambda Developer Guide*\.