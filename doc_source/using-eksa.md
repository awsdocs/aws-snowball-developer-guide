# Using Amazon EKS Anywhere on AWS Snow<a name="using-eksa"></a>

Amazon EKS Anywhere on AWS Snow helps you to create and operate Kubernetes clusters on Snow Family devices\. Kubernetes is open\-source software that's used for automating deployment, scaling, and management of containerized applications\. You can use Amazon EKS Anywhere on a Snowball Edge device with or without an external network connection\. To use Amazon EKS Anywhere on a device without an external network connection, provide a container registry to run on the Snowball Edge device\. For general information about Amazon EKS Anywhere, see the [Amazon EKS Anywhere documentation](https://anywhere.eks.amazonaws.com/docs/)\.

Using Amazon EKS Anywhere on AWS Snow provides you with these capabilities:
+ Provision a Kubernetes \(K8s\) cluster with Amazon EKS Anywhere CLI \(eksctl anywhere\) on Snowball Edge compute\-optimized devices\. You can provision Amazon EKS Anywhere on a single Snowball Edge device or three or more devices for high availability\.
+ Support for Cilium Container Network Interface \(CNI\)\.
+ Support for Ubuntu 20\.04 as the node operating system\.

This diagram illustrates an Amazon EKS Anywhere cluster deployed on a Snowball Edge device\.

![\[Diagram depicting Amazon EKS Anywhere on AWS Snow cluster deployed on a Snowball Edge device and relationships between components.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/eskaarch.jpg)

To see which Kubernetes versions are supported, see [Version support](https://anywhere.eks.amazonaws.com/docs/reference/support/support-versions/) in the Amazon EKS Anywhere documentation\.

For more information about Amazon EKS Anywhere on AWS Snow, see the [Amazon EKS Anywhere documentation](https://anywhere.eks.amazonaws.com/docs/)\.

**Topics**
+ [Actions to complete before ordering a Snowball Edge device for Amazon EKS Anywhere on AWS Snow](eksa-gettingstarted.md)
+ [Ordering a Snowball Edge device for use with Amazon EKS Anywhere on AWS Snow](order-sbe.md)
+ [Configuring and running Amazon EKS Anywhere on Snowball Edge devices](eksa-configuration.md)
+ [Configuring Amazon EKS Anywhere on AWS Snow for disconnected operation](configure-disconnected.md)
+ [Create, upgrade, and delete Amazon EKS Anywhere clusters on Snowball Edge devices](CrUD-clusters.md)
+ [Troubleshooting Amazon EKS Anywhere clusters on Snowball Edge devices](troubleshooting-eksa.md)