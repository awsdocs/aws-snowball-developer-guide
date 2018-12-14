--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Validating NFC Tags<a name="nfc-validation"></a>

Snowball Edge devices have three options for device configurations\. Snowball Edge Compute Optimized devices \(with or without the GPU\) have NFC tags built into them\. You can scan these tags with the AWS Snowball Edge Verification App, available on iOS and Android\. Scanning and validating these NFC tags can help you verify that your device has not been tampered with before you use it\.

Validating NFC tags includes using the Snowball client to generate a device\-specific QR code to verify that the tags you're scanning are for the right device\.

The following procedure describes how to validate the NFC tags on a Snowball Edge device\. Before you get started, make sure you've performed the following first five steps of the getting started exercise:

1. Create your first job\. For more information, see [Create Your First Job](create-job.md)\.

1. Receive the device\. For more information, see [Receive the Snowball Edge](receive-device.md)\.

1. Connect to your local network\. For more information, see [Connect to Your Local Network](getting-started-connect.md)\.

1. Get your credentials and tools\. For more information, see [Get Your Credentials and Tools](get-credentials.md)\.

1. Download and install the Snowball client\. For more information, see [Download and Install the Snowball Client](download-the-client.md)\.

**To validate the NFC tags in a Snowball Edge Compute Optimized device**

1. Run the `snowballEdge get-app-qr-code` Snowball client command\. If you run this command for a node in a cluster, provide the serial number \(`--device-sn`\) to get a QR code for a single node\. Repeat this step for each node in the cluster\. For more information on using this command, see [Getting Your QR Code for NFC Validation](using-client-commands.md#client-qr-code)\.

   The QR code is saved to a location of your choice as a \.png file\.

1.  Navigate to the \.png file that you saved, and open it so that you can scan the QR code with the app\.

1. Download and install the AWS Snowball Edge Verification App from the Google Play store on the Android phone that you're using to scan the NFC tags\.

1. Start the app, and follow the on\-screen instructions\.
**Warning**  
We strongly recommend that you use the app a second time and repeat the scanning process described preceding for the four remaining NFC tags before you use the device\.   
When a device is returned to AWS, we scan all eight tags to ensure that the device isn't tampered with\. If any of the tags are inert, the data on the device isn't imported, and we will contact you about the issue\.

You've now successfully scanned and validated the NFC tags for your device\. 

If you encounter issues while scanning, try the following:
+ Confirm that your device has the Snowball Edge Compute Optimized options \(with or without GPU\)\.
+ Download the app on another phone, and try again\.
+ Move the device to an isolated area of the room, away from interference from other NFC tags, and try again\.
+ If issues persist, contact [AWS Support](https://aws.amazon.com/premiumsupport/)\.