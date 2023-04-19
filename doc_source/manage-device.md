# Managing Your Devices<a name="manage-device"></a>

You use the AWS OpsHub to manage your Snow Family devices\. On the **Device details** page, you can perform the same tasks that you do using the AWS CLI, including changing the alias of your device, rebooting the device, and checking for updates\.

**Topics**
+ [Rebooting your device](#reboot-device)
+ [Shutting down your device](#shutdown-device)
+ [Editing Your Device Alias](#edit-device-alias)
+ [Getting Updates for Your Device and the AWS OpsHub Application](#get-updates)
+ [Managing profiles](#manage-profile)

## Rebooting your device<a name="reboot-device"></a>

Follow these steps to use AWS OpsHub to reboot your Snow device\.

**Important**  
We highly recommend that you suspend all activities on the device before you reboot the device\. Rebooting a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\.

**To reboot a device**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Then choose the device to open the device details page\. 

1. Choose the **Device Power** menu, then choose **Reboot**\. A dialog box appears\.  
![\[Device details page showing Device Power menu open with Reboot chosen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-device-reboot-console.png)

1. In the dialog box, choose **Reboot**\. Your device starts to reboot\.  
![\[Reboot device window showing Reboot button at lower right.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-reboot-window-console.png)

   While the device shuts down, the LCD screen displays a message indicating the device is shutting down\.  
![\[Shutdown message on LCD screen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/shutdown-screen.png)

## Shutting down your device<a name="shutdown-device"></a>

Follow these steps to use AWS OpsHub to shut down your Snow device\.

**Important**  
We highly recommend that you suspend all activities on the device before you shut down the device\. Shutting down a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\.

**To shut down a device**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Then choose the device to open the device details page\.

1. Choose the **Device Power** menu, then choose **Shutdown**\. A dialog box appears\.  
![\[Device details page showing Device Power menu open with Shutdown chosen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-device-shutdown-console.png)

1. In the dialog box, choose **Shutdown**\. Your device starts to shut down\.  
![\[Shutdown device window showing Shutdown button at lower right.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-shutdown-window-console.png)

   While the device shuts down, the LCD screen displays a message indicating the device is shutting down\.  
![\[Shutdown message on LCD screen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/shutdown-screen.png)

## Editing Your Device Alias<a name="edit-device-alias"></a>

Use these steps to edit your device alias using AWS OpsHub\.

**To edit your device's alias**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\. 

1. Choose the **Edit device alias** tab\.  
![\[Device details page showing Edit device alias tab at top right.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-edit-device-alias-button-console.png)

1. For **Device alias**, enter a new name, and choose **Save alias**\.  
![\[Edit device alias window showing Save alias button at lower right.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-edit-device-alias-window-console.png)

## Getting Updates for Your Device and the AWS OpsHub Application<a name="get-updates"></a>

You can check for updates for your device and install them\. You can also configure AWS OpsHub to automatically update the application to the latest version\.



**Updating your device**

Follow these steps to use AWS OpsHub to update your Snow device\.

**To update your device**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\. 

1. Choose the **Check for updates** tab\.

   The **Check for updates** page displays the current software version on your device and the latest software version, if there is one\.  
![\[Check for updates page\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-check-updates-console.png)

1. If there is an update, choose **Download update**\. Otherwise, choose **Close**\.



**Updating your AWS OpsHub application**

AWS OpsHub automatically updates the application to the latest version\. Follow these steps to verify that automatic update is enabled\.

**To verify that automatic updates are enabled for AWS OpsHub**

1. On the AWS OpsHub dashboard, choose** Preferences**\.

1. Open the **Updates** tab\.

1. Verify that **Automatic updates enabled** is selected\. Automatic update is enabled by default\.  
![\[Updates tab showing automatic updates enabled\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-auto-update-console.png)

   If **Automatic updates enabled** is not selected, you will not get the latest version of the AWS OpsHub application\.

## Managing profiles<a name="manage-profile"></a>

You can create a *profile* for persistent storage of your credentials on your local file system\. Using AWS OpsHub, you have the option to create a new profile any time you unlock the device using the device IP address, unlock code, and manifest file\.

You can also use the Snowball Edge Client to create a profile at any time\. See [Configuring a Profile for the Snowball Edge Client](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#client-configuration)\.

To edit or delete profiles, edit the profile file in a text editor\.

**Example `snowball-edge.config` file**  
This example shows a profile file containing three profiles—`SnowDevice1profile`, `SnowDevice2profile`, and `SnowDevice3profile`\.  

```
{"version":1,"profiles":
    {
    "SnowDevice1profile":
        {
            "name":"SnowDevice1profile",
            "jobId":"JID12345678-136f-45b4-b5c2-847db8adc749",
            "unlockCode":"db223-12345-dbe46-44557-c7cc2",
            "manifestPath":"C:\\Users\\Administrator\\.aws\\ops-hub\\manifest\\JID12345678-136f-45b4-b5c2-847db8adc749_manifest-1670622989203.bin",
            "defaultEndpoint":"https://10.16.0.1",
            "isCluster":false,
            "deviceIps":[]
        },
    },
    "SnowDevice2profile":
    {
        "name":"SnowDevice2profile",
        "jobId":"JID12345678-fdb2-436a-a4ff-7c510dec1bae",
        "unlockCode":"b893b-54321-0f65c-6c5e1-7f748",
        "manifestPath":"C:\\Users\\Administrator\\.aws\\ops-hub\\manifest\\JID12345678-fdb2-436a-a4ff-7c510dec1bae_manifest-1670623746908.bin",
        "defaultEndpoint":"https://10.16.0.2",
        "isCluster":false,
        "deviceIps":[]
    },
    "SnowDevice3profile":
    {
        "name":"SnowDevice3profile",
        "jobId":"JID12345678-c384-4a5e-becd-ab5f38888463",
        "unlockCode":"64c89-13524-4d054-13d93-c1b80",
        "manifestPath":"C:\\Users\\Administrator\\.aws\\ops-hub\\manifest\\JID12345678-c384-4a5e-becd-ab5f38888463_manifest-1670623999136.bin",
        "defaultEndpoint":"https://10.16.0.3",
        "isCluster":false,
        "deviceIps":[]
    }
}
```

**To create a profile**

1. Unlock your device locally and sign in according to the instructions in [Unlocking a device locally](connect-unlock-local.md)\.

1. Name the profile and choose **Save profile name**\.

**To edit a profile**

1. In a text editor, open `snowball-edge.config` from `home directory\.aws\snowball\config`\.

1. Edit the file as necessary\. For example, to change the IP address of a device in the profile, change the `defaultEndpoint` entry\.

1. Save and close the file\.

**To delete a profile**

1. Using a text editor, open `snowball-edge.config` from `home directory\.aws\snowball\config`\.

1. Delete the line that contains the profile name, the curly brackets `{` `}`that follow the profile name, and the contents within the those brackets\. 

1. Save and close the file\.