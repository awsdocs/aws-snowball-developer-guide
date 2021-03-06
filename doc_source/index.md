# AWS Snowball Edge Developer Guide AWS Snowball Edge

-----
*****Copyright &copy; 2020 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is an AWS Snowball Edge?](whatisedge.md)
   + [AWS Snowball Device Differences](device-differences.md)
   + [How AWS Snowball Works with the Snowball Edge](how-it-works.md)
   + [Setting Up Your AWS Access for AWS Snowball Edge](setting-up.md)
+ [Understanding AWS Snowball Edge Jobs](jobs.md)
   + [Job Statuses](jobstatuses.md)
   + [Import Jobs into Amazon S3](importtype.md)
   + [Export Jobs from Amazon S3](exporttype.md)
   + [Local Compute and Storage Only Jobs](computetype.md)
   + [Cloning a Job in the Console](clonejob.md)
+ [Getting Started with an AWS Snowball Edge Device](getting-started.md)
   + [Getting Started with AWS Snowball Edge: Your First Job](common-get-start.md)
      + [Create Your First Job](create-job.md)
      + [Receive the Snowball Edge](receive-device.md)
      + [Connect to Your Local Network](getting-started-connect.md)
      + [Get Your Credentials and Tools](get-credentials.md)
      + [Download and Install the Snowball Client](download-the-client.md)
      + [Unlock the Snowball Edge](unlockdevice.md)
      + [Set Up Local Users](setup-local-iam.md)
      + [Use the Snowball Edge](transfer-data.md)
      + [Stop the Snowball Client, and Power Off the Snowball Edge](turnitoff.md)
      + [Disconnect the Snowball Edge](disconnectdevice.md)
      + [Return the Snowball Edge](return-device.md)
      + [Monitor the Import Status](monitor-status.md)
      + [Get Your Job Completion Report and Logs in the Console](report.md)
   + [Where Do I Go from Here?](where-to.md)
+ [Best Practices for the AWS Snowball Edge Device](BestPractices.md)
   + [How to Transfer Petabytes of Data Efficiently](transfer-petabytes.md)
+ [Using an AWS Snowball Edge Device](using-device.md)
   + [Using the Snowball Client](using-client.md)
      + [Commands for the Snowball Client](using-client-commands.md)
   + [Transferring Files Using the Amazon S3 Adapter](using-adapter.md)
      + [Batching Small Files](batching-small-files.md)
      + [Supported AWS CLI Commands](using-adapter-cli.md)
      + [Supported REST API Actions](using-adapter-supported-api.md)
   + [Transferring Files to AWS Snowball Edge Using the File Interface](using-fileinterface.md)
   + [Using AWS Lambda with an AWS Snowball Edge](using-lambda.md)
      + [Getting Started with Lambda Powered by AWS IoT Greengrass](function-getting-started.md)
   + [Using Amazon EC2 Compute Instances](using-ec2.md)
      + [Using the AWS CLI and API Operations on Snowball Edge](using-ec2-cli-specify-region.md)
      + [Quotas for Compute Instances on a Snowball Edge](ec2-edge-limits.md)
      + [Creating a Job with Compute Instances](create-ec2-edge-job.md)
      + [Network Configuration for Compute Instances](network-config-ec2-edge.md)
      + [Connecting to Your Compute Instance on a Snowball Edge Using SSH](ssh-ec2-edge.md)
      + [Transferring Data from Amazon EC2 Compute Instances to Amazon S3 Buckets on the Same Snowball Edge](data-transfer-ec2-s3-edge.md)
      + [Snowball Client Commands for Compute Instances](using-ec2-edge-client.md)
      + [Using the Amazon EC2 Endpoint](using-ec2-endpoint.md)
      + [Autostarting Amazon EC2 Instances with Launch Templates](ec2-autostart.md)
      + [Using Block Storage With Your Amazon EC2 Instances](edge-ebs.md)
      + [Security Groups in Snowball Edge Devices](edge-security-groups.md)
      + [Supported Instance Metadata and User Data](edge-compute-instance-metadata.md)
      + [Troubleshooting Compute Instances on Snowball Edge Devices](troubleshooting-ec2-edge.md)
   + [Using IAM Locally](using-local-iam.md)
   + [Using AWS Security Token Service](using-sts.md)
   + [Ports Required to Use AWS Services on an AWS Snowball Edge Device](port-requirements.md)
+ [Using an AWS Snowball Edge Cluster](UsingCluster.md)
   + [Administrating a Cluster](administercluster.md)
+ [Updating software on a AWS Snowball Edge](updating-device.md)
+ [Shipping Considerations for AWS Snowball](shipping.md)
   + [Shipping an AWS Snowball Edge](mailing-storage.md)
+ [Using AWS OpsHub for Snow Family to Manage Devices](aws-opshub.md)
   + [Unlocking a Device](connect-unlock-device.md)
   + [Managing AWS Services on Your Device](manage-services.md)
      + [Using Amazon EC2 Compute Instances Locally](manage-ec2.md)
      + [Managing an Amazon EC2 Cluster](manage-clusters.md)
      + [Managing Amazon S3 Storage](manage-s3.md)
   + [Managing Your Devices](manage-device.md)
   + [Automating Your Management Tasks](automate-task.md)
+ [Security for AWS Snowball Edge](security.md)
   + [Data Protection in Snowball Edge](data-protection.md)
      + [Protecting Data in the Cloud](data-protection-cloud.md)
         + [Encryption for AWS Snowball Edge](encryption.md)
         + [AWS Key Management Service in AWS Snowball Edge](kms.md)
      + [Protecting Data On Your Device](data-protection-device.md)
   + [Identity and Access Management in Snowball](snowball-edge-iam.md)
      + [Access Control for Snow Family Console and Creating Jobs](authentication-and-access-control.md)
         + [Access Control in the AWS Cloud](access-control.md)
         + [Using Identity-Based Policies (IAM Policies) for AWS Snowball](access-control-managing-permissions.md)
            + [Customer Managed Policy Examples](access-policy-examples-for-sdk-cli.md)
   + [Logging and Monitoring in Snowball](snowball-edge-security-logging-and-monitoring.md)
   + [Compliance Validation for Snowball](snowball-edge-compliance.md)
   + [Resilience](disaster-recovery-resiliency.md)
   + [Infrastructure Security in Snowball](infrastructure-security.md)
+ [Data Validation with Snowball Edge Jobs](validation.md)
+ [Notifications for the AWS Snowball Edge](notifications.md)
+ [Logging AWS Snowball Edge API Calls with AWS CloudTrail](logging-using-cloudtrail.md)
+ [AWS Snowball Edge Specifications](specifications.md)
+ [AWS Snowball Edge Quotas](limits.md)
+ [Troubleshooting for an AWS Snowball Edge](troubleshooting.md)
+ [Additional Information for Snowball Edge](appendices.md)
   + [Using the Snowball Client](old-using-client.md)
   + [Clustering Overview](old-clusters.md)
      + [Administrating a Cluster](old-administercluster.md)
   + [Using the File Interface for the AWS Snowball Edge](using-fileinterface-old.md)
   + [Using AWS Lambda with an AWS Snowball Edge](using-lambda-old.md)
      + [Getting Started with Lambda Powered by AWS IoT Greengrass](function-getting-started-old.md)
+ [API Reference](sbe-api.md)
+ [Document History](doc-history.md)
+ [AWS glossary](glossary.md)