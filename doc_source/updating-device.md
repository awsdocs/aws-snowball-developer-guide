# Updating software on Snowball Edge devices<a name="updating-device"></a>

You can download software updates from AWS and install them on Snowball Edge devices in your on\-premises environments\. These updates happen in the background\. You can continue to use your devices as normal while the latest software is downloaded securely from AWS to your device\. However, to apply downloaded updates, you must restart the device\.

Software updates provided by AWS for Snowball Edge/Snowcone devices \(Appliances\) are Appliance Software as per Section 9 of the Service Terms\.

The software updates are provided solely for the purpose of installing the software updates on the applicable Appliance on behalf of AWS\. You will not \(or attempt to\), and will not permit or authorize third parties to \(or attempt to\) \(i\) make any copies of the software updates other than those necessary to install the software updates on the applicable Appliance, or \(ii\) circumvent or disable any features or measures in the software updates, including, but not limited to, any encryption applied to the software update\. Once the software updates have been installed on the applicable Appliance, you agree to delete the software updates from any and all media utilized in installing the software updates to the Appliance\.

**Warning**  
We highly recommend that you suspend all activity on your device before restarting it\. Restarting a device stops running instances, interrupts any writing to local Amazon S3 buckets, and stops any write operations from the file interface without clearing the cache\. All of these processes can result in lost data\.

**Topics**
+ [Prerequisites](#prereq-updating-device)
+ [Downloading updates](#download-updates)
+ [Installing updates](#install-updates)
+ [Update the SSL certificate](#update-ssl-cert)

## Prerequisites<a name="prereq-updating-device"></a>

Before you can update your device, the following prerequisites must be met:
+ You've created your job, have the device on\-premises, and you've unlocked it\. For more information, see [Getting Started](https://docs.aws.amazon.com/snowball/latest/developer-guide/getting-started.html)\.
+ Updating Snowball Edge devices is done through the Snowball Edge client\. The Snowball Edge client must be downloaded and installed on a computer in your local environment that has a network connection to the device you want to update\. For more information, see [Using the Snowball Edge Client](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client.html)\.
+ \(Optional\) We recommend that you configure a profile for the Snowball Edge client\. For more information, see [Configuring a Profile for the Snowball Edge Client](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#client-configuration)\.

After you complete these tasks, you can download and install updates for Snowball Edge devices\.

## Downloading updates<a name="download-updates"></a>

There are two primary ways that you can download an update for Snowball Edge devices: 
+ You can trigger manual updates at any time using specific Snowball Edge client commands\.
+ You can programmatically determine a time to automatically update the device\.

The following procedure outlines the process of manually downloading updates\. For information about automatically updating your Snowball Edge; device, see `snowballEdge configure-auto-update-strategy` in [Updating a Snowball Edge](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#update-client-commands)\.

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

## Installing updates<a name="install-updates"></a>

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

   To stop a service running on your Snowball Edge device, you can use the `snowballEdge stop-service` command\. 

   The Amazon S3, Amazon EC2, AWS STS, and IAM services cannot be stopped\.

1. Run the `snowballEdge list-services` command to list the currently running services on the device\.

1. Run the `snowballEdge describe-service` command for each of the running services, to see their status\.

1. Use this information to stop those services \(setting the services to the `INACTIVE` state\)\.

1. When all the services on the device have stopped, run the `snowballEdge reboot-device` command **twice**\. This command immediately power\-cycles the device to complete installation of the downloaded software updates\.

1. When the device powers on after the second reboot, open a terminal window and use the `snowballEdge unlock-device` command to unlock the device\.

1. Run the `snowballEdge check-for-updates` command\. This command returns the latest available version of the Snowball Edge software, and also the current version that is installed on the device\.

You have now successfully updated your device and confirmed that your device is up to date with the latest Snowball Edge software\.

## Update the SSL certificate<a name="update-ssl-cert"></a>

If you plan to keep your Snowball Edge device for more than 360 days, you will need to update the Secure Sockets Layer \(SSL\) certificate on the device to avoid interruption of your use of the device\. If the certificate expires, you will not be able to use the device and will have to return it to AWS\.

This topic explains how to determine when the certificate will expire and how to update your device\.

**Note**  
Request an update from AWS at least two weeks before the certificate will expire to avoid interruption of your use of the device\.

1. Use the `snowballEdge describe-device-software` command to determine when the certificate will expire\. In the output of the command, the value of `CertificateExpiry` includes the date and time at which the certificate will expire\.  
**Example of `describe-device-software` output**  

   ```
   Installed version: 101
   Installing version: 102
   Install State: Downloading
   CertificateExpiry : Thur Jan 01 00:00:00 UTC 1970
   ```

1. Contact AWS Support and request an SSL certificate update\.

1. AWS Support will provide an update file\. [Download](#download-updates) and [install](#install-updates) the update file\.

1. Use the new unlock code and manifest file when [Unlocking the Snowball Edge](https://docs.aws.amazon.com/latest/developer-guide/unlockdevice.html)\.