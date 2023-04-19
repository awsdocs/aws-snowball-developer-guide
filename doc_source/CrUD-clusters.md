# Create, upgrade, and delete Amazon EKS Anywhere clusters on Snowball Edge devices<a name="CrUD-clusters"></a>

If you want to create a cluster in a static IP address range, ensure that you don’t create other clusters on your Snowball Edge devices in the same IP address range\. If you want to create another cluster using DHCP addressing on your Snowball Edge devices, ensure that all static IP address ranges that you use for clusters are not in the DHCP pool subnet\.

**Note**  
Best practice: Create a cluster and wait until it is successfully provisioned and running, then create another one\.

To create, upgrade, and delete Amazon EKS Anywhere clusters, refer to [Snow getstarted](https://anywhere.eks.amazonaws.com/docs/getting-started/production-environment/snow-getstarted/)\.

To upgrade an Amazon EKS Anywhere admin AMI or EKS Distro AMI, contact AWS Support\. AWS Support will provide a Snowball Edge update containing the upgraded AMI\. Then, download and install the Snowball Edge update\. See [Downloading updates](updating-device.md#download-updates) and [Installing updates](updating-device.md#install-updates)\.

After you upgrade your Amazon EKS Anywhere AMI, you need to start a new Amazon EKS Anywhere admin instance\. See [Run an Amazon EKS Anywhere admin instance](eksa-configuration.md#start-admin-instance)\. Then, copy key files, the cluster folder, credentials, and certificates from the previous admin instance to the upgraded instance\. These are in a folder that's named for the cluster\.

## Clean up resources<a name="clean-up-resources"></a>

If you create multiple clusters on your Snowball Edge devices and don't delete them correctly or if there is a problem in the cluster and the cluster creates replacement nodes after resuming, there will be resource leak\. You can use a sample script tool to clean your Amazon EKS Anywhere admin instance and your Snowball Edge devices\. See [Amazon EKS Anywhere on AWS Snow cleanup tools](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/cleanup-tools#eks-anywhere-on-snow-cleanup-tools)\.