# Step 3: Choose your features and options<a name="import-job-details"></a>

Choose the features and options to include in your AWS Snow Family device job, including Amazon EKS Anywhere for Snow, an AWS IoT Greengrass instance, and remote device management capability\.

**To choose your features and options**

1. In the **Amazon EKS Anywhere on AWS Snow** section, to include Amazon EKS Anywhere on AWS Snow, select **Include Amazon EKS Anywhere on AWS Snow** and then do the following\.

   1. In the **Kubernetes information** field, choose the version of Kubernetes used by the Kubernetes nodes you want to use in Amazon EKS Anywhere on the Snowball Edge device\.

   1. In the **Select Amazon EKS Anywhere install version** field, choose the version of Amazon EKS Anywhere you want to use on the Snowball Edge device\.

   1. In the **Build your own AMI** section, choose the AMIs you have built for Amazon EKS Anywhere\. See [Actions to complete before ordering a Snowball Edge device for Amazon EKS Anywhere on AWS Snow](eksa-gettingstarted.md)\.

   1. In the **High availability** section, to operate Amazon EKS Anywhere clusters across multiple Snowball Edge devices, choose the number of devices to include in your order\.

1. In the **AWS IoT Greengrass on Snow** section, to include a validated AMI for IoT workloads, select **Install AWS IoT Greengrass validated AMI on my Snow device**\.

1. To enable remote management of your Snow Family device by AWS OpsHub or Snowball Edge Client, select **Manage your Snow device remotely with AWS OpsHub or Snowball client**\.

1. Select the **Next** button\.