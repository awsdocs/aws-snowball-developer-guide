# Updating Software on an AWS Snowball Edge<a name="updating-device"></a>

You can download software updates from AWS and install them on AWS Snowball Edge devices in your on\-premises environments\. These updates happen in the background\. You can continue to use your devices as normal while the latest software is downloaded securely from AWS to your device\. However, to apply downloaded updates, you must restart the device\.

**Warning**  
We highly recommend that you suspend all activity on your device before restarting it\. Restarting a device stops running instances, interrupts any writing to local Amazon S3 buckets, and stops any write operations from the file interface without clearing the cache\. All of these processes can result in lost data\.

**Topics**
+ [Prerequisites](#prereq-updating-device)
+ [Downloading Updates](#download-updates)
+ [Installing Updates](#install-updates)

## Prerequisites<a name="prereq-updating-device"></a>

Before you can update your device, the following prerequisites must be met:
+ You've created your job, have the device on\-premises, and you've unlocked it\. For more information, see [Getting Started](getting-started.md)\.
+ Updating a Snowball Edge is done through the Snowball Edge client\. The Snowball Edge client must be downloaded and installed on a computer in your local environment that has a network connection to the device you want to update\. For more information, see [Using the Snowball Edge Client](using-client.md)\.
+ \(Optional\) We recommend that you configure a profile for the Snowball Edge client\. For more information, see [Configuring a Profile for the Snowball Edge Client](using-client-commands.md#client-configuration)\.

After you complete these tasks, you can download and install updates for Snowball Edge devices\.

## Downloading Updates<a name="download-updates"></a>

There are two primary ways that you can download an update for a Snowball Edge device: 
+ You can trigger manual updates at any time using specific Snowball Edge client commands\.
+ You can programmatically determine a time to automatically update the device\.

The following procedure outlines the process of manually downloading updates\. For information about automatically updating your Snowball Edge device, see `snowballEdge configure-auto-update-strategy` in [Updating a Snowball Edge](using-client-commands.md#update-client-commands)\.

**Note**  
If your device has no access to the internet, you can download an update file using the [GetSoftwareUpdates](https://docs.aws.amazon.com/snowball/latest/api-reference/API_GetSoftwareUpdates.html) API\. Then point to a local file location when you call `download-updates` using the `--uri` option, as in the following example\.  

```
snowballEdge download-updates --uri file:///tmp/local-update
```

**To check for and download Snowball Edge software updates**

1. Open a terminal window, and ensure that the Snowball Edge device is unlocked using the `snowballEdge describe-device` command\. If the device is locked, use the `snowballEdge unlock-device` command to unlock it\.

1. When the device is unlocked, run the `snowballEdge check-for-updates` command\. This command returns the latest available version of the Snowball Edge software, and also the current version installed on the device\.

1. If your device software is out of date, run the `snowballEdge download-updates` command\.
**Note**  
If your device is not connected to the internet, first download an update file using the [GetSoftwareUpdates](https://docs.aws.amazon.com/snowball/latest/api-reference/API_GetSoftwareUpdates.html) API\. Then run the `snowballEdge download-updates` command using the `--uri` option with a local path to the file that you downloaded, as in the following example\.  

   ```
   snowballEdge download-updates --uri file:///tmp/local-update
   ```

1. You can check the status of this download with the `snowballEdge describe-device-software` command\. While an update is downloading, you display the status using this command\. 

**Example output**  
 `Install State: Downloading`

## Installing Updates<a name="install-updates"></a>

After downloading updates, you must install them and restart your device for the updates to take effect\. The following procedure guides you through manually installing updates\.

**To install Snowball Edge software updates that were already downloaded**

1. Open a terminal window, and ensure that the Snowball Edge device is unlocked using the `snowballEdge describe-device` command\. If the device is locked, use the `snowballEdge unlock-device` command to unlock it\.

1. Run the `snowballEdge install-updates` command\.

1. You can check the status of this installation with the `snowballEdge describe-device-software` command\. While an update is installing, you display the status with this command\.

**Example output**  
`Install State: Installing //Possible values[NA, Installing, Requires Reboot]`

   You’ve successfully installed a software update for your Snowball Edge device\. Installing an update does not automatically apply the update to the device\. To finish installing the update, the device must be restarted\.

   We highly recommend that you suspend all activity on the device before you restart the device\. Restarting a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\.
**Warning**  
Restarting your Snowball Edge device without stopping all activity on the device can result in lost data\.

   To stop a service running on your Snowball Edge, you can use the `snowballEdge stop-service` command\. 

   The Amazon S3, Amazon EC2, AWS STS, and IAM services cannot be stopped\.

1. Run the `snowballEdge list-services` command to list the currently running services on the device\.

1. Run the `snowballEdge describe-service` command for each of the running services, to see their status\.

1. Use this information to stop those services \(setting the services to the `INACTIVE` state\)\.

1. When all the services on the device have stopped, run the `snowballEdge reboot-device` command\. This command immediately power\-cycles the device to complete installation of the downloaded software updates\.

1. After the device powers on, open a terminal window and use the `snowballEdge unlock-device` command to unlock the device\.

1. Run the `snowballEdge check-for-updates` command\. This command returns the latest available version of the Snowball Edge software, and also the current version that is installed on the device\.

You have now successfully updated your device and confirmed that your device is up to date with the latest Snowball Edge software\.