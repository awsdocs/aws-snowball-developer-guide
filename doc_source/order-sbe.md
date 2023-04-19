# Ordering a Snowball Edge device for use with Amazon EKS Anywhere on AWS Snow<a name="order-sbe"></a>

To order your Snowball Edge compute optimized or compute optimized with GPU device, see [Creating a Snowball Edge job](create-job-common.md) in this guide and keep these items in mind during the ordering process:
+ In step 1, choose the **Local compute and storage only** job type\.
+ In step 2, choose the **Snowball Edge Compute Optimized** or **Snowball Edge Compute Optimized with GPU** device type\.
+ In step 3, choose **EKS Anywhere on AWS Snow**, then choose the Kubernetes version and EKS Anywhere version that you need\.
+ Choose AMIs to include on your device, including the EKS Distro AMI \(see [Create an Ubuntu EKS Distro AMI](eksa-gettingstarted.md#create-eksd-ami)\) and, optionally, the Harbor AMI that you built \(see [Build a Harbor AMI](eksa-gettingstarted.md#existing-private-registry)\)\.
+ If you need multiple Snowball Edge devices for high availability, choose the number of devices that you need from **High Availability**\.

After you receive your Snowball Edge device or devices, configure Amazon EKS Anywhere according to [Configuring and running Amazon EKS Anywhere on Snowball Edge devices](eksa-configuration.md)\.