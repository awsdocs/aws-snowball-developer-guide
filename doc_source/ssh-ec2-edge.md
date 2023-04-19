# Using SSH to Connect to Your Compute Instance on a Snowball Edge<a name="ssh-ec2-edge"></a>

To use SSH to connect to your compute instances on AWS Snowball Edge devices, you must first provide the SSH key to the Amazon Machine Image \(AMI\) before creating your job\. For more information, see [Configuring an AMI to Use SSH to Connect to Compute Instances Launched on the Device](create-ec2-edge-job.md#important-create-ec2-edge-job)\. If you haven't followed that procedure, you can't use SSH to connect to your instances\.

**To connect to your instance with SSH**

1. Make sure that your device is powered on, connected to the network, and unlocked\. For more information, see [Connecting to Your Local Network](getting-started-connect.md)\.

1. Make sure that you have your network settings configured for your compute instances\. For more information, see [Network Configuration for Compute Instances](snowcone-network-config-ec2.md)\.

1. Check your notes to find the PEM or PPK key pair that you used for this specific instance\. Make a copy of those files somewhere on your computer\. Make a note of the path to the PEM file\.

1. Connect to your instance through SSH as in the following example command\. The IP address is the IP address of the virtual network interface \(VNIC\) that you set up in [Network Configuration for Compute Instances](snowcone-network-config-ec2.md)\.

   ```
   ssh -i path/to/PEM/key/file instance-user-name@192.0.2.0
   ```

   For more information, see [Connecting to Your Linux Instance Using SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html) in the* Amazon EC2 User Guide for Linux Instances\.*