# Unlocking a device<a name="connect-unlock-device"></a>

When your device arrives at your site, the first step is to connect and unlock it\. AWS OpsHub lets you sign in, unlock, and manage devices using the following methods:
+ **Locally** – To sign in to a device locally, you must power on the device and connect it to your local network\. Then provide an unlock code and a manifest file\.
+ **Remotely** – To sign in to a device remotely, you must power on the device and make sure that it can connect to `device-order-region.amazonaws.com` through your network\. Then provide the AWS Identity and Access Management \(IAM\) credentials \(access key and secret key\) for the AWS account that is linked to your device\.

  For information on enabling remote management and creating an associated account, see [Enabling Snow Device Management ](aws-sdm.md#enable-sdm)\.

**Topics**
+ [Unlocking a device locally](connect-unlock-local.md)
+ [Unlocking a device remotely](connect-unlock-remote.md)