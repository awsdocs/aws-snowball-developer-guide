# Using Amazon EC2 Compute Instances<a name="using-ec2"></a>

This section provides an overview of using Amazon EC2 compute instances on an AWS Snowball Edge device, including conceptual information, procedures, and examples\.

**Topics**
+ [Overview](#ec2-overview-edge)
+ [Pricing for Compute Instances on Snowball Edge](#pricing-for-ec2-edge)
+ [Using an Amazon EC2 AMI on Your Device](using-ami.md)
+ [Importing an Image into Your Device as an Amazon EC2 AMI](ec2-ami-import-cli.md)
+ [Using the AWS CLI and API Operations on Snowball Edge](using-ec2-cli-specify-region.md)
+ [Quotas for Compute Instances on a Snowball Edge Device](ec2-edge-limits.md)
+ [Creating a Compute Job](create-ec2-edge-job.md)
+ [Network Configuration for Compute Instances](network-config-ec2.md)
+ [Using SSH to Connect to Your Compute Instance on a Snowball Edge](ssh-ec2-edge.md)
+ [Transferring Data from EC2 Compute Instances to S3 Buckets on the Same Snowball Edge](data-transfer-ec2-s3-edge.md)
+ [Snowball Edge Client Commands for Compute Instances](using-ec2-edge-client.md)
+ [Using the Amazon EC2 Endpoint](using-ec2-endpoint.md)
+ [Autostarting Amazon EC2 Instances with Launch Templates](ec2-autostart.md)
+ [Using Instance Metadata Service for Snow with Amazon EC2 instances](imds.md)
+ [Using Block Storage with Your Amazon EC2 Instances](edge-ebs.md)
+ [Security Groups in Snowball Edge Devices](edge-security-groups.md)
+ [Supported Instance Metadata and User Data](edge-compute-instance-metadata.md)
+ [Stopping EC2 Instances](#managing-ec2-instances)
+ [Troubleshooting Compute Instances on Snowball Edge Devices](troubleshooting-ec2-edge.md)

## Overview<a name="ec2-overview-edge"></a>

You can run Amazon EC2 compute instances hosted on a Snowball Edge with the `sbe1`, `sbe-c`, and `sbe-g` instance types\. The `sbe1` instance type works on devices with the Snowball Edge Storage Optimized option\. The `sbe-c` instance type works on devices with the Snowball Edge Compute Optimized option\. Both the `sbe-c` and `sbe-g` instance types work on devices with the Snowball Edge Compute Optimized with GPU option\. For a list of supported instance types, see [Quotas for Compute Instances on a Snowball Edge Device](ec2-edge-limits.md)\.

All three compute instance types supported for use on Snowball Edge device options are unique to Snowball Edge devices\. Like their cloud\-based counterparts, these instances require Amazon Machine Images \(AMIs\) to launch\. You choose the AMI to be that base image for an instance in the cloud, before you create your Snowball Edge job\.

To use a compute instance on a Snowball Edge, create a job and specify your AMIs\. You can do this using the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home), the AWS CLI, or one of the AWS SDKs\. Typically, there are some housekeeping prerequisites that you must perform before creating your job, to use your instances\.

After your device arrives, you can start managing your AMIs and instances\. You can manage your compute instances on a Snowball Edge through an Amazon EC2–compatible endpoint\. This type of endpoint supports many of the Amazon EC2 CLI commands and actions for the AWS SDKs\. You can't use the AWS Management Console on the Snowball Edge to manage your AMIs and compute instances\.

When you're done with your device, return it to AWS\. If the device was used in an import job, the data transferred using the Amazon S3 adapter or the NFS interface is imported into Amazon S3\. Otherwise, we perform a complete erasure of the device when it is returned to AWS\. This erasure follows the National Institute of Standards and Technology \(NIST\) 800\-88 standards\.

**Important**  
Using encrypted AMIs on Snowball Edge devices is not supported\.
Data in compute instances running on a Snowball Edge isn't imported into AWS\.

## Pricing for Compute Instances on Snowball Edge<a name="pricing-for-ec2-edge"></a>

There are additional costs associated with using compute instances\. For more information, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

## Stopping EC2 Instances<a name="managing-ec2-instances"></a>

To avoid accidentally deleting the Amazon EC2 instances that you create on your device, don't shut down your instances from the operating system\. For example, don't use the `shutdown` or `reboot` commands\. Shutting down an instance from within the operating system has the same effect as calling the [terminate\-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html) command\.

Instead, use the [stop\-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/stop-instances.html) command to suspend Amazon EC2 instances that you want to preserve\.