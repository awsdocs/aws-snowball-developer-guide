# Unlocking a device locally<a name="connect-unlock-local"></a>

This video shows how to unlock a Snow Family device locally using AWS OpsHub\.

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/StMa2A7X2yA?start=36&end=70/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/StMa2A7X2yA?start=36&end=70)

**To connect and unlock your device locally**

1. Open the flap on your device, locate the power cord, and connect it to a power source\.

1. Connect the device to your network using an Ethernet cable \(typically an RJ45 cable\), then open the front panel and power on the device\.

1. Open the AWS OpsHub application\. If you are a first\-time user, you are prompted to choose a language\. Then choose **Next**\.

1. On the **Get started with OpsHub** page, choose **Sign in to local devices**, and then choose **Sign in**\.  
![\[Get started with AWS OpsHub page\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-unlock-local-console.png)

1. On the **Sign in to local devices** page, choose your Snow Family devices type, and then choose **Sign in**\.

   If you don't have a device, you can [order one](https://docs.aws.amazon.com/snowball/latest/developer-guide/getting-started.html)\.

1. On the **Sign in** page, enter the **Device IP address** and **Unlock code**\. To select the device manifest, choose **Choose file**, and then choose **Sign in**\.  
![\[AWS OpsHub sign in page\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-sign-in-local-console.png)

1. \(Optional\) Save your device's credentials as a *profile*\. Name the profile and choose **Save profile name**\. For more information about profiles, see [Managing profiles](manage-device.md#manage-profile)\.

1. On the **Local devices** tab, choose a device to see its details, such as the network interfaces and AWS services that are running on the device\. You can also see details for clusters from this tab, or manage your devices just as you do with the AWS Command Line Interface \(AWS CLI\)\. For more information, see [Managing AWS services on your device](manage-services.md)\.

   For devices that have AWS Snow Device Management installed, you can choose **Enable remote management** to turn on the feature\. For more information, see [Using AWS Snow Device Management to Manage Devices](aws-sdm.md)\.