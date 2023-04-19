# Unlocking a device remotely<a name="connect-unlock-remote"></a>

**To connect and unlock your device remotely**

1. Open the flap on your device, locate the power cord, and connect it to a power source\.

1. Connect the device to your network using an Ethernet cable \(typically an RJ45 cable\), then open the front panel and power on the device\.
**Note**  
To be unlocked remotely, your device must be able to connect to `device-order-region.amazonaws.com`\.

1. Open the AWS OpsHub application\. If you are a first\-time user, you are prompted to choose a language\. Then choose **Next**\.

1. On the **Get started with OpsHub** page, choose **Sign into remote devices**, and then choose **Sign in**\.  
![\[Get started with AWS OpsHub page with Sign into remote devices chosen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-unlock-remote-console.png)

1. On the **Sign in to remote devices** page, enter the AWS Identity and Access Management \(IAM\) credentials \(access key and secret key\) for the AWS account that is linked to your device, and then choose **Sign in**\.  
![\[Sign in to remote devices page\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-remote-unlock-console.png)

1. At the top of the **Remote devices** tab, choose the region of the Snow device to unlock remotely\.  
![\[Remote devices tab with region menu highlighted.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-remote-region-console.png)

1. On the **Remote devices** tab, choose your device to see its details, such as its state and network interfaces\. Then choose **Unlock** to unlock the device\.   
![\[Device information details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-remote-console.png)

   From the remote device's details page, you can also reboot your devices and manage them just as you do with the AWS Command Line Interface \(AWS CLI\)\. To view remote devices in different AWS Regions, choose the current Region on the navigation bar, and then choose the Region that you want to view\. For more information, see [Managing AWS services on your device](manage-services.md)\.