# Using AWS IoT Greengrass to run pre\-installed software on Amazon EC2 instances<a name="using-green-grass"></a>

AWS IoT Greengrass is an open source Internet of Things \(IoT\) edge runtime and cloud service that helps you build, deploy, and manage IoT applications on your devices\. You can use AWS IoT Greengrass to build software that enables your devices to act locally on the data that they generate, run predictions based on machine learning models, and filter and aggregate device data\. For detailed information about AWS IoT Greengrass, see [What is AWS IoT Greengrass?](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html) in the *AWS IoT Greengrass Version 2 Developer Guide*\.

By using AWS IoT Greengrass on your Snow Family device, you enable the device to collect and analyze data closer to where it is generated, react autonomously to local events, and communicate securely with other devices on the local network\.

## Setting up your Amazon EC2 instance<a name="setup-ec2-gg"></a>

**Note**  
To install AWS IoT Greengrass Version 2 on a Snow Family device, make sure that your device is connected to the internet\. After installation, the internet is not required for a Snow Family device to work with AWS IoT Greengrass\. 

**To set up an EC2 instance for AWS IoT Greengrass V2**

1. Launch an Amazon EC2 instance with a public IP Address and an SSH key:

   1. Using the AWS CLI: [run\-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)\.

   1. Using AWS OpsHub: [Launching an Amazon EC2 instance](https://docs.aws.amazon.com/snowball/latest/developer-guide/manage-ec2.html#launch-instance)\.
**Note**  
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
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip &&sudo ./aws/install && sudo yum -y install python3 java-1.8.0-openjdk
   ```

1. Grant the root user permission to run the AWS IoT Greengrass software and modify the root permission from `root ALL=(ALL) ALL` to `root ALL=(ALL:ALL) ALL` in the sudoers config file\.

   ```
   sudo sed -in 's/root\tALL=(ALL)/root\tALL=(ALL:ALL)/' /etc/sudoers
   ```

1. Use the following commands to provide credentials to allow you to install AWS IoT Greengrass Core software\. Replace the example values with your credentials:

   ```
   export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE 
   export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
   ```
**Note**  
These are credentials from the IAM user in the AWS Region, not the Snow Family device\.

1. Use the following command to install the AWS IoT Greengrass Core software\. The command creates AWS resources that the core software requires to operate and sets up the core software as a system service that runs when the AMI boots up\.

   Replace the following parameters in the command:
   + `region`: The AWS Region in which to find or create resources\.
   + `MyGreengrassCore`: The name of the AWS IoT thing for your AWS IoT Greengrass core device\.
   + `MyGreengrassCoreGroup`: The name of the AWS IoT thing group for your AWS IoT Greengrass core device\.

   ```
   sudo -E java -Droot="/greengrass/v2" -Dlog.store=FILE \
       -jar ./GreengrassInstaller/lib/Greengrass.jar \
       --aws-region region \
       --thing-name MyGreengrassCore \
       --thing-group-name MyGreengrassCoreGroup \
       --thing-policy-name GreengrassV2IoTThingPolicy \
       --tes-role-name GreengrassV2TokenExchangeRole \
       --tes-role-alias-name GreengrassCoreTokenExchangeRoleAlias \
       --component-default-user ggc_user:ggc_group \
       --provision true \
       --setup-system-service true \
       --deploy-dev-tools true
   ```
**Note**  
This command is for an Amazon EC2 instance running an Amazon Linux 2 AMI\. For a Windows AMI, see [Install the AWS IoT Greengrass Core software](https://docs.aws.amazon.com/greengrass/v2/developerguide/install-greengrass-core-v2.html)\.

When you are finished, you will have an AWS IoT Greengrass core running on your Snow Family device for your local use\.