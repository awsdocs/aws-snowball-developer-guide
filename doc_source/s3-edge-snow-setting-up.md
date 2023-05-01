# Setting up using the Snowball Edge client CLI<a name="s3-edge-snow-setting-up"></a>

You can set up your cluster with the Snowball Edge client CLI\.

**Note**  
If you prefer a more user\-friendly experience, you can set up your cluster using AWS OpsHub\. See [Set up Amazon S3 compatible storage on Snow Family devices using AWS OpsHub](https://docs.aws.amazon.com/\snowball\latest\developer-guide\s3-edge-snow-opshub.html) in this guide\.

## Prerequisites<a name="s3-snow-prereq"></a>

This section describes how to set up and configure the CLI when using Amazon S3 compatible storage on Snow Family devices\.

**To set up the device**

1. Download and install the [latest Snowball Edge client CLI](https://docs.aws.amazon.com/snowball/latest/developer-guide/download-the-client.html)\. 

1. Run the following commands to configure your folders\.

   ```
   chmod u+x new_cli/bin/snowballEdge
   chmod u+x new_cli/jre/bin/java
   ```

1. Add `new_cli/bin` to your `$PATH`\.

1. Run the command `snowballEdge configure`\. You receive a response similar to the following: 

   ```
   Configuration will be stored at /home/marymajor/.aws/snowball/config/snowball-edge.config
   ```

1. Enter the following information:
   + The manifest path\.
   + An unlock code\.
   + The default endpoint\. Specify the IP address for any device in your cluster\. To test if the default endpoints are available from the client, use a command similar to the following:

     ```
     telnet snowball_ip port_number where the port number is; 9091 
     (Activation port), 22 (ssh) and 8080 (http endpoint for s3)
     ```

## Setting up IAM<a name="setting-up-s3-on-snow-iam"></a>

AWS Identity and Access Management \(IAM\) helps you to enable granular access to AWS resources that run on your Snowball Edge devices\. You use IAM to control who is authenticated \(signed in\) and authorized \(has permissions\) to use resources\.

IAM is supported locally on your device\. You can use the local IAM service to create roles and attach IAM policies to them\. You can use these policies to allow the access necessary to perform assigned tasks\.

The following example allows full access to the Amazon S3 API:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "*"
            
        }
    ]
}
```

For more IAM policy examples, see the [AWS Snowball Edge Developer Guide](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-local-iam.html#policy-examples)\.

## Setting up Snowball Edge<a name="setting-up-s3-on-snow-cluster"></a>

The following instructions walk you through how to set up a Snowball Edge device or cluster\.

1. Unlock your Snowball Edge device or cluster of devices by running the following command:
   + For a single device:

     ```
     snowballEdge unlock-device --endpoint https://snow-device-ip
     ```
   + For a cluster:

     ```
     snowballEdge unlock-cluster
     ```

1. Run the following command and make sure that your devices are in an `UNLOCKED` state:
   + For a single device:

     ```
     snowballEdge describe-device --endpoint https://snow-device-ip
     ```
   + For a cluster:

     ```
     snowballEdge describe-cluster --device-ip-addresses [snow-device-1-ip] [snow-device-2-ip] /
         [snow-device-3-ip] [snow-device-4-ip] [snow-device-5-ip] /
         [snow-device-6-ip]
     ```

1. For each device \(whether you have one or a cluster\), to start Amazon S3 compatible storage on Snow Family devices, do the following:

   1. Fetch the device's `PhysicalNetworkInterfaceId` by running the following `describe-device` command:

      ```
      snowballEdge describe-device --endpoint https://snow-device-ip
      ```

   1. Run the following `create-virtual-network-interface` command twice to create the virtual network interfaces \(VNIs\) for the `s3control` \(for bucket operations\) and `s3api` \(for object operations\) endpoints\.

      ```
      snowballEdge create-virtual-network-interface --ip-address-assignment dhcp --manifest-file manifest --physical-network-interface-id "PhysicalNetworkInterfaceId" --unlock-code snowball --endpoint https://snow-device-ip
      ```

      For details about these commands, see [Creating a Virtual Network Interface](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-ec2-edge-client.html#ec2-edge-create-vnic)\.
**Note**  
Starting Amazon S3 compatible storage on Snow Family devices consumes device resources\.

1. Start the service by running the following `start-service` command\. which includes the IP addresses of your devices and the Amazon Resource Names \(ARNs\) of the VNIs that you created for the `s3control` and `s3api` endpoints:

   To start the service for a cluster:

   ```
   snowballEdge start-service --service-id s3-snow --device-ip-addresses snow-device-1-ip snow-device-2-ip snow-device-3-ip --virtual-network-interface-arns vni-arn-1 vni-arn-2 vni-arn-3  vni-arn-4 vni-arn-5 vni-arn-6
   ```

   To start the service on a single device:

   ```
   snowballEdge start-service --service-id s3-snow --device-ip-addresses snow-device-1-ip --virtual-network-interface-arns vni-arn-1 vni-arn-2
   ```

   For `--virtual-network-interface-arns`, include ARNs for all the VNIs that you created in the previous step\. Separate each ARN using a space\.

1. Run the following `describe-service` command for a cluster:

   ```
   snowballEdge describe-service --service-id s3-snow \ 
     --device-ip-addresses snow-device-1-ip snow-device-2-ip snow-device-3-ip
   ```

   Run the following `describe-service` command for a single device:

   ```
   snowballEdge describe-service --service-id s3-snow
   ```

   Wait until service status is `Active`\.