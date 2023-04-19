# Managing Your Devices<a name="manage-device"></a>

You use the AWS OpsHub to manage your Snow Family devices\. On the **Device details** page, you can perform the same tasks that you do using the AWS CLI, including changing the alias of your device, rebooting the device, and checking for updates\.

**Topics**
+ [Rebooting Your Device](#reboot-device)
+ [Editing Your Device Alias](#edit-device-alias)
+ [Getting Updates for Your Device and the AWS OpsHub Application](#get-updates)
+ [Managing Profiles](#manage-profile)

## Rebooting Your Device<a name="reboot-device"></a>

Follow these steps to use AWS OpsHub to reboot your Snow device\.

**Important**  
We highly recommend that you suspend all activities on the device before you reboot the device\. Rebooting a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\.

**To reboot a device**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Then choose the device to open the device details page\. 

1. Choose the **Reboot device** tab, and in the dialog box that appears, choose **Reboot device**\. Your device starts to reboot\.

## Editing Your Device Alias<a name="edit-device-alias"></a>

Use these steps to edit your device alias using AWS OpsHub\.

**To edit your device's alias**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\. 

1. Choose the **Edit device alias** tab\.

1. For **Device alias**, enter a new name, and choose **Save alias**\.

## Getting Updates for Your Device and the AWS OpsHub Application<a name="get-updates"></a>

You can check for updates for your device and install them\. You can also configure AWS OpsHub to automatically update the application to the latest version\.



**Updating your device**

Follow these steps to use AWS OpsHub to update your Snow device\.

**To update your device**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\. 

1. Choose the **Check for updates** tab\.

   The **Check for updates** page displays the current software version on your device and the latest software version, if there is one\.

1. If there is an update, choose **Update**\. Otherwise, choose **Close**\.



**Updating your AWS OpsHub application**

AWS OpsHub automatically updates the application to the latest version\. Follow these steps to verify that automatic update is enabled\.

**To verify that automatic updates are enabled for AWS OpsHub**

1. On the AWS OpsHub dashboard, choose** Preferences**\.

1. Open the **Updates** tab\.

1. Verify that **Automatic updates enabled** is selected\. Automatic update is enabled by default\.

   If **Automatic updates enabled** is not selected, you will not get the latest version of the AWS OpsHub application\.

## Managing Profiles<a name="manage-profile"></a>

A *profile* is a persistent storage of your credentials on your local file system\. You can create a profile when you first unlock your device, or you can create one after your device is running\. You can create new profiles, edit existing profiles, or delete them\.

**To create a profile**

1. In the upper\-right corner of the application, choose your name, and then choose **Manage profile**\.

1. On the **Manage profiles** page, choose **Create profile**\. You create a profile for each device\. 

   If your device is locked, see [Unlocking a device](connect-unlock-device-sbe.md) for instructions\.

1. Provide the name for the profile, the IP address of your device, and the unlock code\.

1. Choose **Upload**, upload the manifest, and then choose **Create device**\. 

   You now have a new profile for your device\. You use this profile to log in to the device\.

**To edit a profile**

1. In the upper\-right corner of the application, choose your name, and then choose **Manage profile**\.

   All your profiles appear on the page\.

1. On the **Manage profiles** page, choose the profile that you want to edit\. 

1. On the next page, choose **Edit**\. Make the changes that you want for your device, and choose **Save device**\.

**To delete a profile**

1. In the upper\-right corner of the application, choose your name, and then choose **Manage profile**\.

   All your profiles appear on the page\.

1. Choose the profile that you want to delete, and choose **Delete profile**\.