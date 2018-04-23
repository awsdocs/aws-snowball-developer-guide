# AWS Snowball Developer Guide

-----
*****Copyright &copy; 2018 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

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
   + [Jobs for AWS Snowball Edge Appliances](jobs.md)
      + [Job Statuses](jobstatuses.md)
      + [Import Jobs into Amazon S3](importtype.md)
      + [Export Jobs from Amazon S3](exporttype.md)
      + [Local Compute and Storage Only Jobs](computetype.md)
      + [Cloning a Job in the Console](clonejob.md)
   + [Setting Up Your AWS Access for AWS Snowball Edge](setting-up.md)
+ [Getting Started with an AWS Snowball Edge Appliance](getting-started.md)
   + [Getting Started with AWS Snowball Edge: Your First Job](common-get-start.md)
      + [Create Your First Job](create-job.md)
      + [Receive the Snowball Edge](receive-appliance.md)
      + [Connect to Your Local Network](getting-started-connect.md)
      + [Get Your Credentials and Tools](get-credentials.md)
      + [Download and Install the Snowball Client](download-the-client.md)
      + [Unlock the Snowball Edge](unlockappliance.md)
      + [Use the Snowball Edge](transfer-data.md)
      + [Stop the Snowball Client, and Power Off the Snowball Edge](turnitoff.md)
      + [Disconnect the Snowball Edge](disconnectappliance.md)
      + [Return the Snowball Edge](return-appliance.md)
      + [Monitor the Import Status](monitor-status.md)
      + [Get Your Job Completion Report and Logs in the Console](report.md)
   + [Where Do I Go from Here?](where-to.md)
+ [Best Practices for the AWS Snowball Edge Appliance](BestPractices.md)
   + [How to Transfer Petabytes of Data Efficiently](transfer-petabytes.md)
+ [Using an AWS Snowball Edge](using-appliance.md)
   + [Using the Snowball Client](using-client.md)
      + [Commands for the Snowball Client](using-client-commands.md)
   + [Using the Amazon S3 Adapter](using-adapter.md)
      + [Batching Small Files](batching-small-files.md)
      + [Supported AWS CLI Commands](using-adapter-cli.md)
      + [Supported REST API Actions](using-adapter-supported-api.md)
   + [Using the File Interface for the AWS Snowball Edge](using-fileinterface.md)
   + [Using AWS Lambda with an AWS Snowball Edge](using-lambda.md)
      + [Getting Started with Lambda Powered by AWS Greengrass](function-getting-started.md)
+ [Using an AWS Snowball Edge Cluster](UsingCluster.md)
   + [Administrating a Cluster](administercluster.md)
+ [Shipping Considerations for AWS Snowball](shipping.md)
   + [Shipping an AWS Snowball Edge](mailing-storage.md)
+ [Security for AWS Snowball Edge](security.md)
   + [AWS Key Management Service in AWS Snowball](kms.md)
   + [Authorization with the Amazon S3 API Adapter for AWS Snowball](auth-adapter.md)
   + [Other Security Considerations for AWS Snowball](security-considerations.md)
+ [Authentication and Access Control for AWS Snowball Edge](authentication-and-access-control.md)
   + [Overview of Managing Access Permissions to Your Resources in the AWS Cloud](access-control-overview.md)
   + [Using Identity-Based Policies (IAM Policies) for AWS Snowball](access-control-managing-permissions.md)
   + [AWS Snowball API Permissions: Actions, Resources, and Conditions Reference](snowball-api-permissions-ref.md)
+ [Data Validation with Snowball Edge Jobs](validation.md)
+ [Notifications for the AWS Snowball Edge](notifications.md)
+ [AWS Snowball Edge Specifications](specifications.md)
+ [AWS Snowball Edge Limits](limits.md)
+ [Troubleshooting for an AWS Snowball Edge](troubleshooting.md)
+ [Additional Information for Snowball Edge](appendices.md)
   + [Using the Snowball Client](old-using-client.md)
   + [Clustering Overview](old-clusters.md)
      + [Administrating a Cluster](old-administercluster.md)
+ [Document History](doc-history.md)
+ [AWS Glossary](glossary.md)