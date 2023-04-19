# Unlocking a device<a name="connect-unlock-device-sbe"></a>

When your device arrives at your site, the first step is to connect and unlock it\.

**To connect and unlock your device**

1. Open the flap on your device, locate the power cord, and connect it to a power source\.

1. Connect the device to your network using an Ethernet cable \(typically an RJ45 cable\)\. Then open the front panel and power on the device\.

1. Open the AWS OpsHub application\. If you are a first\-time user, you are prompted to choose a language\. Then choose **Next**\.

1. On the **Get started with OpsHub** page, choose **Sign in to local devices**, and then choose **Sign in**\.

1. On the **Sign in to local devices** page, choose **Snowball Edge** for a single device or **Snowball Edge cluster** for multiple devices, and then choose **Sign in**\.

1. Enter the **Device IP address** and **Unlock code**\. For a Snowball Edge cluster, choose **Add device IP address** to add IP address fields for each device\. Then choose **Choose file** to select the device manifest, and then choose **Sign in**\.

1. \(Optional\) Save your device credentials as a *profile*\. Name the profile and choose **Save profile name**\. For more information about profiles, see [Managing Profiles](manage-device.md#manage-profile)\.

1. On the **Local devices** tab, choose a device to see its details, such as the network interfaces and AWS services that are running on the device\. You can also see details for clusters from this tab, or manage your devices just as you do with the AWS Command Line Interface \(AWS CLI\)\. For more information, see [Managing AWS services on your device](manage-services.md)\.