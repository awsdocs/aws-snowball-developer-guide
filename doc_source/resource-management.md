# Resource Management<a name="resource-management"></a>

Consider the following best practices for managing jobs and resources on your AWS Snowball Edge device\.
+ The 10 free days for performing your on\-premises data transfer start the day after the AWS Snowball Edge device arrives at your data center\. This applies only to Snowball Edge device types\.
+ The **Job created** status is the only status in which you can cancel a job\. When a job changes to a different status, you can't cancel the job\. This applies to clusters\.
+ For import jobs, don't delete your local copies of the transferred data until the import into Amazon S3 is successful\. As part of your process, be sure to verify the results of the data transfer\.