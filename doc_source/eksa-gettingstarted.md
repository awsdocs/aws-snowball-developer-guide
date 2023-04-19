# Actions to complete before ordering a Snowball Edge device for Amazon EKS Anywhere on AWS Snow<a name="eksa-gettingstarted"></a>

At this time, Amazon EKS Anywhere is compatible with Snowball Edge compute\-optimized and compute\-optimized with graphics processing unit \(GPU\) devices\. Before you order a Snowball Edge device, there are a few things you should do to prepare\. 
+ Build and supply an operating system image to use to create virtual machines on the device\.
+ Your network must have a static IP address available for the K8s control plan endpoint and allow Address Resolution Protocol \(ARP\)\.
+ Your Snowball Edge device must have specific ports open\. For more information about ports, see [Ports and protocols](https://anywhere.eks.amazonaws.com/docs/reference/ports/) in the Amazon EKS Anywhere documentation\.

**Topics**
+ [Create an Ubuntu EKS Distro AMI](#create-eksd-ami)
+ [Build a Harbor AMI](#existing-private-registry)

## Create an Ubuntu EKS Distro AMI<a name="create-eksd-ami"></a>

To create the Ubuntu EKS Distro AMI, see [Build Snow node images](https://anywhere.eks.amazonaws.com/docs/reference/artifacts/#build-snow-node-images)\.

The name of the generated AMI will follow the pattern `capa-ami-ubuntu-20.04-version-timestamp`\. For example, `capa-ami-ubuntu-20.04-v1.24-1672424524`\.

## Build a Harbor AMI<a name="existing-private-registry"></a>

Set up a Harbor private registry AMI to include on the Snowball Edge device so you can use Amazon EKS Anywhere on the device without an external network connection\. If you won't be using Amazon EKS Anywhere while the Snowball Edge device is disconnected from the external network, or if you have a private Kubernetes registry in an AMI to use on the device, you can skip this section\.

To create the Harbor local registry AMI, see [Build a Harbor AMI](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/container-registry-ami-builder#build-harbor-ami)\.