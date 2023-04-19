# Using an Amazon EC2 AMI on Your Device<a name="using-ami"></a>

To use an Amazon Machine Image \(AMI\) on your AWS Snow Family device, you must first add it to the device\. You can add an AMI in the following ways:
+ Upload the AMI when you order the device\.
+ Add the AMI when your device arrives at your site\.

Amazon EC2 compute instances that come with your Snow Family devices are launched based on the Amazon EC2 AMIs that you add to your device\. Amazon EC2 AMIs support both Linux and Microsoft Windows operating systems\.

**Linux**  
The following Linux operating systems are supported:
+ [Amazon Linux 2 for Snow Family](https://aws.amazon.com/marketplace/pp/B08Q76DLTM/             )
+ [CentOS 7 \(x86\_64\) \- with Updates HVM](https://aws.amazon.com/marketplace/pp/B00O7WM7QW)
+ [Ubuntu 16\.04 LTS \- Xenial \(HVM\)](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)

**Windows**  
The following Windows operating systems are supported:
+ Windows Server 2012 R2
+ Windows Server 2016
+ Windows Server 2019

You can add Windows AMIs to your device by importing your Windows virtual machine \(VM\) image into AWS using VM Import/Export\. Or, you can import the image into your device right after the device is deployed to your site\. For more information, see [Adding a Microsoft Windows AMI](#windows-ami)\. 

**Note**  
Windows AMIs that originated in AWS can't be added to your device\.

 Snow Family supports the Bring Your Own License \(BYOL\) model\. For more information, see [Adding a Microsoft Windows AMI](#windows-ami)\. 

**Topics**
+ [Adding an AMI When Ordering Your Device](#add-ami-order)
+ [Adding an AMI from AWS Marketplace](#add-marketplace-ami)
+ [Adding an AMI Locally](#add-ami-locally)
+ [Adding a Microsoft Windows AMI](#windows-ami)
+ [Importing a VM Image into Your Device](#import-vm-image)

## Adding an AMI When Ordering Your Device<a name="add-ami-order"></a>

When you order your device, you can add AMIs to the device by choosing **Enable Compute with EC2** in the AWS Snow Family Management Console\. When you choose **Add AMI**, you see the **Source AMI name** list that contains all the AMIs that can be loaded onto your device\. The AMIs fall into the following categories:
+ **AMIs from AWS Marketplace** — These are AMIs created from the list of supported AMIs\. For information about creating an AMI from the supported AMIs from AWS Marketplace, see [Adding an AMI from AWS Marketplace](#add-marketplace-ami)\.
+ **AMIs uploaded using VM Import/Export** — When you order your device, the AMIs that were uploaded using VM Import/Export are listed in the console\. For more information, see [Importing a VM as an Image Using VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/vmimport-image-import.html) in the *VM Import/Export User Guide*\. For information about supported virtualization environments, see [VM Import/Export Requirements](https://docs.aws.amazon.com/vm-import/latest/userguide/vmie_prereqs.html)\.

## Adding an AMI from AWS Marketplace<a name="add-marketplace-ami"></a>

Follow these steps to add an AMI from AWS Marketplace:

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Launch a new instance of a supported AMI in AWS Marketplace\.
**Note**  
When you launch your instance, make sure that the storage size you assign to the instance is appropriate for your use case\. In the Amazon EC2 console, you do this in the **Add storage** step\.   
For a list of the supported compute instance storage volumes and sizes on a Snowball Edge device, see [Amazon Elastic Compute Cloud endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/ec2-service.html) in the *AWS General Reference*\.

1. Install and configure the applications that you want to run on the Snowball Edge, and make sure that they work as expected\.
**Important**  
Only single volume AMIs are supported\.
The EBS volume in your AMI should be 10 TB or less\. We recommend that you provision the EBS volume size needed for the data in the AMI\. This will help decrease the time it takes to export your AMI and load it into your device\. You can resize or add more volumes to your instance after your device is deployed\.
The EBS snapshot in your AMI must not be encrypted\.

1. Make a copy of the PEM or PPK file that you used for the SSH key pair when you created this instance\. Save this file to the server that you plan to use to communicate with the Snowball Edge device\. Make a note of the path to this file because you will need it when you use SSH to connect to the EC2 instance on your device\.
**Important**  
If you don't follow this procedure, you can't connect to your instances with SSH when you receive your Snowball Edge device\.

1. Save the instance as an AMI\. For more information, see [Amazon EC2 User Guide for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html) in the *Amazon EC2 User Guide for Linux Instances\.*

1. Repeat steps 1–4 for each of the instances that you want to connect to using SSH\. Be sure to make copies of each of the SSH key pairs, and keep track of the AMIs that they're associated with\.

1. Now, when you order your device, these AMIs are available to add to your device\. 

## Adding an AMI Locally<a name="add-ami-locally"></a>

When the device arrives on your site, you can add new AMIs to it\. For instructions, see [Importing an Image into Your Device as an Amazon EC2 AMI](ec2-ami-import-cli.md)\. Keep in mind that although all VMs are supported, only supported AMIs have been tested for full functionality\.

**Note**  
When you use VM Import/Export to add AMIs to your device or import a VM after your device is deployed, you can add VMs that use any operating system\. However, only supported operating systems have been tested and validated on Snow Family devices\. You are responsible for adhering to the terms and conditions of any operating system or software that is in the virtual image that you import onto your device\.  
For AWS services to function properly on a Snowball Edge, you must allow the ports for the services\. For details, see [Ports Required to Use AWS Services on an AWS Snowball Edge Device](port-requirements.md)\.

## Adding a Microsoft Windows AMI<a name="windows-ami"></a>

For virtual machines \(VMs\) that use a supported Windows operating system, you can add the AMI by importing your Windows VM image into AWS using VM Import/Export, or by importing it into your device directly after it is deployed to your site\.

**Bring Your Own License \(BYOL\)**  
Snowball Edge supports importing Microsoft Windows AMIs onto your device with your own license\. Bring Your Own License \(BYOL\) is the process of bringing an AMI that you own with its on\-premises license to AWS\. AWS provides both shared and dedicated deployment options for the BYOL option\.

 You can add your Windows VM image to your device by importing it into AWS using VM Import/Export or by importing it into your device directly after it is deployed to your site\. You can't add Windows AMIs that originated in AWS\. Therefore, you must create and import your own Windows VM image and bring your own license if you want to use the AMI on your Snow Family device\. For more information about Windows licensing and BYOL, see [Amazon Web Services and Microsoft: Frequently Asked Questions](https://aws.amazon.com/windows/faq/)\. 

### Creating a Windows VM Image to Import into Your Device<a name="create-windows-image"></a>

To create a Windows VM image, you need a virtualization environment, such as VirtualBox, which is supported for the Windows and macOS operating systems\. When you create a VM for Snow devices, we recommend that you allocate at least two cores with at least 4 GB of RAM\. When the VM is up and running, you must install your operating system \(Windows Server 2012, 2016, or 2019\)\. To install the required drivers for the Snow Family device, follow the instructions in this section\.

For a Windows AMI to run on a Snow device, you must add specific drivers to the device\. Specifically, you must add the VirtIO, FLR, NetVCM, Vioinput, Viorng, Vioscsi, Vioserial, and Vistor drivers\. You can [download the VirtIO file](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.185-2/virtio-win-0.1.185.iso) that contains all the required drivers\.

**Note**  
If you plan to import your VM image directly to your deployed Snow device, the VM image file must be in the RAW format\. 

**To create a Windows image**

1. On your Microsoft Windows computer, choose **Start** and enter **devmgmt\.msc** to open **Device Manager**\.

1. In the main menu, choose **Actions**, and then choose **Add legacy hardware**\.

1. In the wizard, choose **Next**\.

1. Choose **Install the hardware that I manually select from a list \(advanced\)**, and choose **Next**\.

1. Choose **Show All Devices** and choose **Next**\.

1. Choose **Have Disk**, open the **Copy manufacturer’s files from** list, and browse to the ISO file\.

1. In the ISO file, browse to the `Driver\W2K8R2\amd64` directory, and then find the `.INF` file\.

1. Choose the **\.INF** file, choose **Open**, and then choose **OK**\.

1. When you see the driver name, choose **Next**, and then choose **Next** two more times\. Then choose **Finish**\. 

   This installs a device using the new driver\. The actual hardware doesn't exist, so you will see a yellow exclamation mark that indicates an issue on the device\. You must fix this issue\. 

**To fix the hardware issue**

1. Open the context \(right\-click\) menu for the device that has the exclamation mark\.

1. Choose **Uninstall**, clear **Delete the driver software for this device**, and choose **OK**\. 

   The driver is installed, and you are ready to launch the AMI on your device\.

## Importing a VM Image into Your Device<a name="import-vm-image"></a>

After you prepare your VM image, you can use one of the options to import the image to your device\. 
+ **In the cloud using VM Import/Export** — When you import your VM image into AWS and register it as an AMI, you can add it to your device when you place an order from the AWS Snow Family Management Console\. For more information, see [Importing a VM as an Image Using VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/vmimport-image-import.html) in the *VM Import/Export User Guide*\.
+ **Locally on your device that is deployed at your site** — You can import your VM image directly into your device using AWS OpsHub for Snow Family or the AWS Command Line Interface \(AWS CLI\)\.

  For information about using AWS OpsHub, see [Using Amazon EC2 Compute Instances Locally](https://docs.aws.amazon.com/snowball/latest/developer-guide/manage-ec2.html)\.

  For information about using the AWS CLI, see [Importing an Image into Your Device as an Amazon EC2 AMI](ec2-ami-import-cli.md)\.