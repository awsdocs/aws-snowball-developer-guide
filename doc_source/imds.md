# Using Instance Metadata Service for Snow with Amazon EC2 instances<a name="imds"></a>

IMDS for Snow provides Instance Metadata Service \(IMDS\) for Amazon EC2 instances on Snow\. Instance metadata is categories of information about instances\. It includes categories such as *host name*, *events*, and *security groups*\. Using IMDS for Snow, you can use instance metadata to access user data that you specified when launching your Amazon EC2 instance\. For example, you can use IMDS for Snow to specify parameters for configuring your instance, or include these parameters in a simple script\. You can build generic AMIs and use user data to modify the configuration files supplied at launch time\.

To learn about instance metadata and user data and Snow EC2 instances, see [Supported Instance Metadata and User Data](https://docs.aws.amazon.com/snowball/latest/developer-guide/edge-compute-instance-metadata.html) in this guide\.

**Important**  
Although you can only access instance metadata and user data from within the instance itself, the data is not protected by authentication or cryptographic methods\. Anyone who has direct access to the instance, and potentially any software running on the instance, can view its metadata\. Therefore, you should not store sensitive data, such as passwords or long\-lived encryption keys, as user data\.

**Note**  
The examples in this section use the IPv4 address of the instance metadata service: 169\.254\.169\.254\. We do not support the retrieval of instance metadata using the link\-local IPv6 address\.

**Topics**
+ [IMDS versions](imds-versions.md)
+ [Examples of retrieving instance metadata using IMDSv1 and IMDSv2](imds-code-examples.md)