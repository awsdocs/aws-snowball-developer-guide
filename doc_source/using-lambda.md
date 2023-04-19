# Using AWS Lambda with an AWS Snowball Edge<a name="using-lambda"></a>

Following, you can find an overview of AWS Lambda powered by AWS IoT Greengrass as used in an AWS Snowball Edge device\. With this feature, you can run Lambda functions locally on a Snowball Edge\. To use Lambda powered by AWS IoT Greengrass functions with Snowball Edge, you must create your jobs in an AWS Region supported by AWS IoT Greengrass\. For a list of valid AWS Regions, see [AWS IoT Greengrass](https://docs.aws.amazon.com/general/latest/gr/greengrassv2.html) in the *AWS General Reference*\. Lambda on Snowball Edge is available, wherever Lambda and Snowball Edge are available\.

If you created your job before July 17, 2018, this information doesn't apply to your device\.

**Note**  
These features are only supported in the following AWS Regions:  
Asia Pacific \(Tokyo\)
Asia Pacific \(Sydney\)
Canada \(Central\)
US East \(N\. Virginia\)
US West \(Oregon\)

## Before You Start<a name="function-recommendations"></a>

Before you create a Python\-language Lambda function to run on your Snowball Edge, we recommend that you familiarize yourself with the following services, concepts, and related topics\.

### Prerequisites for AWS IoT Greengrass<a name="greengrass-rec"></a>

AWS IoT Greengrass is software that extends AWS Cloud capabilities to local devices\. AWS IoT Greengrass makes it possible for local devices to collect and analyze data closer to the source of information, while also securely communicating with each other on local networks\. More specifically, developers who use AWS IoT Greengrass can author serverless code \(Lambda functions\) in the AWS Cloud\. They can then conveniently deploy this code to devices for local execution of applications\.

The following AWS IoT Greengrass concepts are important to understand when using AWS IoT Greengrass with a Snowball Edge:
+ **AWS IoT Greengrass requirements** – For a full list of AWS IoT Greengrass requirements, see [Requirements](https://docs.aws.amazon.com/greengrass/latest/developerguide/gg-gs.html#gg-requirements) in the *AWS IoT Greengrass Developer Guide*\. 
+ **AWS IoT Greengrass core** – Each Snowball Edge has the AWS IoT Greengrass core software\. For more information about the AWS IoT Greengrass core software, see [Greengrass Core Software](https://docs.aws.amazon.com/greengrass/latest/developerguide/what-is-gg.html#gg-core) in the *AWS IoT Greengrass Developer Guide*\.
+ **AWS IoT Greengrass group** – A Snowball Edge is part of an AWS IoT Greengrass group as the group's core device\. For more information about groups, see [AWS Greengrass IoT Groups](https://docs.aws.amazon.com/greengrass/latest/developerguide/what-is-gg.html#gg-group) in the *AWS IoT Greengrass Developer Guide*\.
+ **MQTT** – AWS IoT Greengrass uses the industry\-standard, lightweight Message Queue Telemetry Transport \(MQTT\) protocol to communicate within a group\. Within a Snowball Edge, there is an IoT device associated with the Amazon S3 interface\. When data is written using [Amazon S3 PUT object](https://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUT.html) operations on buckets specified at job creation, these operations trigger MQTT messages\. These messages in turn trigger any associated Lambda functions\. In addition, any MQTT\-compatible device or software in your AWS IoT Greengrass group can trigger the Lambda functions, if you define the related MQTT message to do so\.
+ **Associated service role** – Before you can use AWS IoT Greengrass with a Snowball Edge as a core device, you must associate an AWS IoT Greengrass service role with your account\. This association allows AWS IoT Greengrass to access your Lambda functions and AWS IoT resources\. For more information, see [Associating an AWS IoT Greengrass Service Role with Your Account](function-getting-started.md#gg-associate-role)\.

### Prerequisites for AWS Lambda<a name="lambda-rec"></a>

AWS Lambda is a compute service that lets you run code without provisioning or managing servers\. The following Lambda concepts are important to understand when using Lambda with a Snowball Edge:
+ **Lambda functions** – Your custom code, uploaded and published to Lambda and used on a Snowball Edge\. For more information, see [Lambda Functions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-introduction-function.html) in the *AWS Lambda Developer Guide*\.
+ **Lambda console** – The console in which you upload, update, and publish your Python\-language Lambda functions for use on a Snowball Edge\. For a sample on how to use the [Lambda console](https://console.aws.amazon.com/lambda), see [Step 2: Create a HelloWorld Lambda Function and Explore the Console](https://docs.aws.amazon.com/lambda/latest/dg/getting-started-create-function.html) in the *AWS Lambda Developer Guide*\.
+ **Python** – The high\-level programming language used for your Lambda functions powered by AWS IoT Greengrass on a Snowball Edge\. AWS IoT Greengrass supports Python version 2\.7\.

### Related Topics<a name="function-related"></a>

The following topics are related to running AWS Lambda powered by AWS IoT Greengrass functions on a Snowball Edge:
+ [Limitations for Lambda Powered by AWS IoT Greengrass](function-limits.md)
+ [Customer Managed Policy Examples](access-policy-examples-for-sdk-cli.md)

**Next:**  
[Getting Started with Lambda Powered by AWS IoT Greengrass](function-getting-started.md)