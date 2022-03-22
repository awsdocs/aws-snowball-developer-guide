# Using AWS IoT Greengrass to run pre\-installed software on Amazon EC2 instances<a name="using-green-grass"></a>

AWS IoT Greengrass is an open source Internet of Things \(IoT\) edge runtime and cloud service that helps you build, deploy, and manage IoT applications on your devices\. You can use AWS IoT Greengrass to build software that enables your devices to act locally on the data that they generate, run predictions based on machine learning models, and filter and aggregate device data\. For detailed information about AWS IoT Greengrass, see [What is AWS IoT Greengrass?](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html) in the *AWS IoT Greengrass Version 2 Developer Guide*\.

By using AWS IoT Greengrass on your Snow Family device, you enable the device to collect and analyze data closer to where it is generated, react autonomously to local events, and communicate securely with other devices on the local network\.

## Setting up your Amazon EC2 instance<a name="setup-ec2-gg"></a>

**Note**  
To install AWS IoT Greengrass Version 2 on a Snow Family device, make sure that your device is connected to the internet\. After installation, the internet is not required for a Snow Family device to work with AWS IoT Greengrass\. 

**To set up an EC2 instance for AWS IoT Greengrass V2**

1. On the AWS OpsHub dashboard, in the **Start Green Grass** section, choose **Get Started**\.

1. Choose **Launch instance**\.

1. Configure the instance with the settings that you want\. The instance should have a public IP address and an SSH key\.

1. Choose **Launch** in the launch instance window to launch the instance\.

1. Open the Amazon EC2 console, and choose the **Instance** tab\. Choose the instance and verify that it’s running\. 

   Take note of the public IP address and SSH key name that are associated with the instance\.

1. Connect to the EC2 instance using SSH\. To do so, run the following command on the computer that is connected to your device\. Replace *ssh\-key* with the key you used to launch the EC2 instance\. Replace *public\-ip\-address* with the public IP address of the EC2 instance\.

   ```
   ssh -i ssh-key ec2-user@ public-ip-address
   ```
**Important**  
If your computer uses an earlier version of Microsoft Windows, you might not have the SSH command, or you might have SSH but can’t connect to your EC2 instance\. To connect to your EC2 instance, you can install and configure PuTTY, which is a no\-cost, open source SSH client\. You must convert the SSH key from `.pem` format to PuTTY format and connect to your EC2 instance\. For instructions on how to convert from `.pem` to PuTTY format, see the PuTTY documentation\.

### Installing AWS IoT Greengrass<a name="install-green-grass"></a>

Next, you set up your EC2 instance as an AWS IoT Greengrass Core device that you can use for local development\. 

**To install AWS IoT Greengrass**

1. Use the following command to install the prerequisite software for AWS IoT Greengrass\. This command installs the AWS Command Line Interface \(AWS CLI\) v2, Python 3, and Java 8\.

   ```
   "curl \"https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip\" -o \"awscliv2.zip\" && unzip awscliv2.zip &&sudo ./aws/install && sudo yum -y install python3 java-1.8.0-openjdk" 
   ```

1. Grant the root user permission to run the AWS IoT Greengrass software and modify the root permission from `root ALL=(ALL) ALL` to `root ALL=(ALL:ALL) ALL` in the sudoers config file\.

   ```
   sudo sed -in 's/root\tALL=(ALL)/root\tALL=(ALL:ALL)/' /etc/sudoers
   ```

1. Use the following command to download the AWS IoT Greengrass Core software\.

   ```
   curl -s https://d2s8p88vqu9w66.cloudfront.net/releases/greengrass-nucleus-latest.zip > greengrass-nucleus-latest.zip && unzip greengrass-nucleus-latest.zip -d GreengrassCore  && rm greengrass-nucleus-latest.zip 
   ```

1. Install and configure the AWS IoT Greengrass Core software\. For instructions, see [Getting started with AWS IoT Greengrass V2](https://docs.aws.amazon.com/greengrass/v2/developerguide/getting-started.html) in the *AWS IoT Greengrass Developer Guide*\.

   Skip steps 1–3 and start with step 4\. Steps 1–3 are not needed\.

When you are finished, you will have an AWS IoT Greengrass core running on your Snow Family device for your local use\.