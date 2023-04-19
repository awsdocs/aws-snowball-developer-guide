# Configuring Amazon EKS Anywhere on AWS Snow for disconnected operation<a name="configure-disconnected"></a>

Complete this additional configuration of Amazon EKS Anywhere on the Snowball Edge device while it's connected to a network to prepare Amazon EKS Anywhere to run in an environment without an external network connection\.

To configure Amazon EKS Anywhere for disconnected use with your own local, private Kubernetes registry, see [Registry Mirror configuration](https://anywhere.eks.amazonaws.com/docs/reference/clusterspec/optional/registrymirror/) in the EKS Anywhere documentation\.

If you created a Harbor private registry AMI, follow the procedures in this section\.

**Topics**
+ [Configure the Harbor registry on a Snowball Edge device](#configure-harbor-snow)
+ [Use the Harbor registry on the Amazon EKS Anywhere admin instance](#use-local-registry-eksa-instance)

## Configure the Harbor registry on a Snowball Edge device<a name="configure-harbor-snow"></a>

See [Configure Harbor on a Snowball Edge device](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/container-registry-ami-builder#configure-harbor-on-a-snowball-edge-device)\.

## Use the Harbor registry on the Amazon EKS Anywhere admin instance<a name="use-local-registry-eksa-instance"></a>

See [Import Amazon EKS Anywhere container images to the local Harbor registry on a Snowball Edge device](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/container-registry-ami-builder#import-eks-anywhere-container-images-to-the-local-harbor-registry-on-a-snowball-device)\.