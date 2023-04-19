# Logging and Monitoring in AWS Snowball<a name="snowball-edge-security-logging-and-monitoring"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of AWS Snowball and your AWS solutions\. You should collect monitoring data so that you can more easily debug a multi\-point failure if one occurs\. AWS provides several tools for monitoring your AWS Snowball resources and responding to potential incidents:

**AWS CloudTrail Logs**  
CloudTrail provides a record of actions taken by a user, role, or an AWS service in the AWS Snowball Job Management API or when using the AWS Console\. Using the information collected by CloudTrail, you can determine the API request that was made to AWS Snowball service, the IP address from which the request was made, who made the request, when it was made, and additional details\. For more information, see [Logging AWS Snowball Edge API Calls with AWS CloudTrail](logging-using-cloudtrail.md)\.