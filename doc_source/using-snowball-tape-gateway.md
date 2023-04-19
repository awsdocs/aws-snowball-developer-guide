# Using an AWS Snowball Edge device with a Tape Gateway<a name="using-snowball-tape-gateway"></a>

Using an AWS Snowball Edge device with a Tape Gateway provides a secure, offline solution for migrating your tape data\. A Snowball Edge device with a Tape Gateway lets you to migrate petabytes of data stored on physical tapes to AWS without changing your existing tape\-based backup workflows, and without extreme network infrastructure or bandwidth\-usage requirements\. A standard Tape Gateway temporarily stores your tape data in the gateway cache and uses your network connection to transfer the data asynchronously to the AWS Cloud\. However, a Snowball Edge device with a Tape Gateway stores your tape data on the device itself until you return it to AWS, and uses your network connection only for device\-management traffic\.

A Tape Gateway is a type of AWS Storage Gateway—a virtual appliance that emulates a physical tape library and works with your existing backup software to help you transfer data into the AWS Cloud\. After you receive your Snowball Edge device, you unlock it, set up a Tape Gateway on it, copy your tape data to it, and then ship it back to AWS\. AWS then stores your tape data in secure, durable, and low\-cost Amazon S3 Glacier Flexible Retrieval or S3 Glacier Deep Archive storage\. With this combination of technologies, you can migrate your tape data to AWS in situations where you have network\-connectivity limitations, bandwidth constraints, or high connection costs\. Moving tape data to AWS helps you decrease your physical\-tape infrastructure expenses and gain online access to your tape\-based data at any time\.

The following sections provide detailed instructions on ordering, deploying, using, and troubleshooting a Snowball Edge device with a Tape Gateway\. For more information about creating and managing a Tape Gateway on your Snowball Edge device, see [Using a Tape Gateway on an AWS Snowball Edge device](https://docs.aws.amazon.com/storagegateway/latest/userguide/using-tape-gateway-snowball.html) in the *AWS Storage Gateway User Guide*\.

## Ordering a Snowball Edge device with a Tape Gateway<a name="ordering-snowball-tape-gateway"></a>

Use the following procedure to order a Snowball Edge device preinstalled with a Tape Gateway and the hardware specifications necessary to back up your tape data\. For more detailed information about ordering Snow Family devices, see [Creating an AWS Snowball Edge Job](create-job-common.md)\.

**To order your device**

1. Sign in to the AWS Management Console, open the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home), and select the AWS Region where you want to order your device\.

1. On the **AWS Snow Family** page, choose **Order an AWS Snow Family device**\.

1. For **Snow Family jobs**, choose **Import virtual tapes into AWS Storage Gateway**\.

1. For **Snow job assistance**, review the best practices and resources provided, then indicate your acknowledgement\.

1. For **Shipping address**, choose where you want to ship your device\.

1. For **Shipping speed**, choose how quickly you want to receive your device\.

1. For **Job name**, enter a name to identify this job and its associated device\.

1. For **Choose your Snow device**, choose **Snowball Edge Storage Optimized**\.
**Note**  
**Snowball Edge Storage Optimized** is the only Snow Family device that supports a Tape Gateway\.

1. For **Encryption**, choose the AWS Key Management Service \(AWS KMS\) key that you want to use to encrypt your data\.

1. For **Set notifications**, choose the Amazon Simple Notification Service \(Amazon SNS\) topic through which you will receive status notifications about your job order\.

1. For each subsection on the **Review and create your job** page, make sure that the options you selected are correct\. To make changes, choose **Edit**\. When you're finished, choose **Create job** to complete your order\.

Now that your order has been placed, you can track it on the **Jobs** page of the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. From there, you can also download and install the Snow Family management software—AWS OpsHub for Snow Family—while you wait for your Snowball Edge device to arrive\.

## Deploying a Snowball Edge device with a Tape Gateway<a name="deploying-snowball-tape-gateway"></a>

After you receive your Snowball Edge device with a Tape Gateway, use the following procedure to connect and unlock it, launch the Tape Gateway application service on it, and obtain the IP address for the Tape Gateway\. The Tape Gateway IP address is different from the IP address of the Snowball Edge device as a whole, and is required for activating the Tape Gateway in the AWS Storage Gateway console\. You must activate the Tape Gateway before you can start backing up your tape data\.

**To deploy your device**

1. Connect the device to your local network and note its IP address\. For more information, see [Connecting to Your Local Network](getting-started-connect.md)\.

1. On a computer connected to the same local network as your device, download and install the latest version of AWS OpsHub for Snow Family from the **Jobs** page of the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. For more information, see [Using AWS OpsHub for Snow Family to Manage Devices](aws-opshub.md)\.

1. Obtain the job manifest and unlock code for your device from the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. For more information, see [Getting Your Credentials and Tools](get-credentials.md)\.

1. Using AWS OpsHub for Snow Family and the credentials and IP address that you obtained in the previous steps, sign in and unlock the device\. For more information, see [Unlocking a device](connect-unlock-device-sbe.md)\.

1. In AWS OpsHub for Snow Family, do the following to start the Tape Gateway application service on your device:

   1. From the **Local devices** page, choose the job name associated with your device to view its management dashboard\.

   1. Under **Services**, choose **Tape Gateway**, then choose **Start service**\.

   1. In the dialog box that appears, choose a virtual network interface for the Tape Gateway application service to use\. Note the IP address of the interface that you select\. This is the Tape Gateway IP address, which you will need when you activate the Tape Gateway in the AWS Storage Gateway console\.

   1. Choose **Start service**\.

Now that your Snowball Edge device is deployed, the Tape Gateway application service is running, and you've obtained the Tape Gateway IP address, you must activate the gateway in the AWS Storage Gateway console\. To do this, choose **Open Storage Gateway management console** from your device's AWS OpsHub management dashboard, then follow the procedures described in [Using a Tape Gateway on an AWS Snowball Edge device](https://docs.aws.amazon.com/storagegateway/latest/userguide/using-tape-gateway-snowball.html) in the *AWS Storage Gateway User Guide*\.

## Troubleshooting and best practices for a Snowball Edge device with a Tape Gateway<a name="troubleshooting-best-practices-snowball-tape-gateway"></a>

To avoid problems and keep your Snowball Edge device with a Tape Gateway running smoothly, refer to the following tips and guidelines:
+ After you order, receive, and deploy your Snowball Edge device, you must create and activate your Tape Gateway from the same AWS Region\. Attempting to create and activate the Tape Gateway in any AWS Region other than where the Snowball Edge was ordered is not supported, and will not work\.
+ To back up your tape data using your Snowball Edge device with a Tape Gateway, connect the virtual tape devices on the gateway to a Windows or Linux client on your network, and then access them using your preferred backup software\. For more information about connecting the gateway to a client and testing it with your backup software, see [Using Your Tape Gateway](https://docs.aws.amazon.com/storagegateway/latest/userguide/GettingStarted-create-tape-gateway.html) in the *AWS Storage Gateway User Guide*\.
+ When a virtual tape is in the **Available** state in the Storage Gateway console, it is ready to be mounted using your preferred backup software, and its full capacity is reserved in physical storage on the Snowball Edge device\. When you eject a virtual tape, its status changes from **Available** to **In transit to VTS**, and only the specific amount of data written to the tape remains reserved on the Snowball Edge device\. You don't need to eject virtual tapes from your backup software before shipping your Snowball Edge device back to AWS\. Any virtual tapes left in the **Available** state are automatically ejected during the data\-transfer process at the AWS facility\.
+ After you copy the data to your Snowball Edge device, you can schedule a pickup appointment to ship the device back to AWS\. The E Ink shipping label is automatically updated to ensure that the device is sent to the correct AWS facility\. For more information, see [Shipping an AWS Snowball Edge](mailing-storage.md)\.

  You can track the device by using Amazon SNS generated text messages and emails\.
+ After your tape data is successfully transferred to the AWS Cloud and your Snowball Edge job is complete, you must manually delete the associated Tape Gateway using the Storage Gateway console\.
+ In rare cases, data corruption or other technical difficulties might prevent AWS from transferring specific virtual tapes to the AWS Cloud after receiving your Snowball Edge device\. In such a case, you must use the Storage Gateway console to delete the virtual tapes that failed to transfer before you can re\-attempt the transfer on another Snowball Edge device\.
+ A Snowball Edge device with a Tape Gateway supports only importing virtual tape data to AWS, and cannot be used to access data that has already been imported\. To access your imported tape data, set up a standard Tape Gateway hosted on a virtual machine, hardware appliance, or Amazon EC2 instance, and transfer the data from AWS over a network connection\.
+ A Snowball Edge device that is configured for a Tape Gateway is not intended for use with other Snowball Edge services or resources, such as Amazon S3, Network File System \(NFS\) file systems, AWS Lambda, or Amazon EC2\. To use those services or resources, you must create a new Snowball Edge job to order a separate, appropriately configured device\. For instructions, see [Creating an AWS Snowball Edge Job](create-job-common.md)\.
+ To troubleshoot a Snowball Edge device with a Tape Gateway, or if directed to do so by AWS Support, you might need to connect to your gateway's local console\. The local console is a configuration interface that runs on the Snowball Edge device that's hosting your gateway\. You can use this local console to perform maintenance tasks specific to the gateway on that device\. For more information, see [Performing Maintenance Tasks on the Local Console](https://docs.aws.amazon.com/storagegateway/latest/userguide/manage-on-premises.html) in the *AWS Storage Gateway User Guide*\.

  To access the local console for the Tape Gateway running on your Snowball Edge device:

  1. From the command prompt on a computer connected to the same local network as your device, run the following command: 

     `ssh user_name@xxx.xxx.xxx.xxx`

     To run this command, replace *`user_name`* with your local console user name, and replace *`xxx.xxx.xxx.xxx`* with the Tape Gateway IP address that you obtained when you launched the Tape Gateway on your Snowball Edge device\. For instructions on how to obtain the Tape Gateway IP address, see [Deploying a Snowball Edge device with a Tape Gateway](#deploying-snowball-tape-gateway)\.

  1. Enter your password\.
**Note**  
If this is your first time logging in to the local console on this device, the default user name is `admin`, and the default password is `password`\. Change the default password immediately after you log in\. For more information, see [Logging in to the Local Console Using Default Credentials](https://docs.aws.amazon.com/storagegateway/latest/userguide/manage-on-premises-common.html#LocalConsole-login-common) in the *AWS Storage Gateway User Guide*\.

## Using the AWS Snow Family API with a Snowball Edge device with a Tape Gateway<a name="using-sgw-api-tape-gateway-snowball"></a>

The AWS Snow Family API and AWS Command Line Interface \(AWS CLI\) work the same for a Snowball Edge device with a Tape Gateway as they do for a standard Snowball Edge device, with the following exceptions:
+ After you receive your Snowball Edge device and use the `unlock-device --manifest-file` AWS CLI command to unlock it, you can use the `list-services` command to return the `ServiceId` for the Tape Gateway application service\. You must provide this value to start the Tape Gateway application service on your device\.

  ```
  snowballEdge list-services
  {
      "ServiceIds" : [ "tapegateway" ]
  }
  ```
+ You can use the `describe-device` command to return the `PhysicalNetworkInterfaceId` for each physical network interface on your Snowball Edge device\. You must provide this value when you create the virtual network interface for the Tape Gateway application service\.

  ```
  snowballEdge describe-device
  
  {
    "DeviceId" : "JID-EXAMPLE12345-123-456-7-890",
    "UnlockStatus" : {
      "State" : "UNLOCKED"
    },
    "ActiveNetworkInterface" : {
      "IpAddress" : "192.0.2.0"
    },
    "PhysicalNetworkInterfaces" : [ {
      "PhysicalNetworkInterfaceId" : "s.ni-EXAMPLEd9ecbf03e3",
      "PhysicalConnectorType" : "RJ45",
      "IpAddressAssignment" : "STATIC",
      "IpAddress" : "0.0.0.0",
      "Netmask" : "0.0.0.0",
      "DefaultGateway" : "192.0.2.1",
      "MacAddress" : "EX:AM:PL:E0:12:34"
    }, {
      "PhysicalNetworkInterfaceId" : "s.ni-EXAMPLE4c3840068f",
      "PhysicalConnectorType" : "QSFP",
      "IpAddressAssignment" : "STATIC",
      "IpAddress" : "0.0.0.0",
      "Netmask" : "0.0.0.0",
      "DefaultGateway" : "192.0.2.2",
      "MacAddress" : "EX:AM:PL:E0:56:78"
    }, {
      "PhysicalNetworkInterfaceId" : "s.ni-abcd1234",
      "PhysicalConnectorType" : "SFP_PLUS",
      "IpAddressAssignment" : "DHCP",
      "IpAddress" : "192.168.1.231",
      "Netmask" : "255.255.255.0",
      "DefaultGateway" : "192.0.2.3",
      "MacAddress" : "EX:AM:PL:E0:90:12"
    } ]
  }
  ```
+ You can use the `create-virtual-network-interface` command to create the virtual network interface for the Tape Gateway application service\. You must provide the `PhysicalNetworkInterfaceId` and specify the method of IP address assignment, such as `DHCP`\. This command returns the `VirtualNetworkInterfaceArn` that you must provide when you start the Tape Gateway application service on your device\.

  ```
  snowballEdge create-virtual-network-interface \ --physical-network-interface-id s.ni-abcd1234 \ --ip-address-assignment DHCP
  
  {
       "VirtualNetworkInterface" : {
           "VirtualNetworkInterfaceArn" : "arn:aws:snowball-device:::interface/s.ni-abcd1234",
           "PhysicalNetworkInterfaceId" : "s.ni-abcd1234",
           "IpAddressAssignment" : "DHCP",
           "IpAddress" : "192.0.2.0",
           "Netmask" : "255.255.255.0",
           "DefaultGateway" : "192.0.2.10",
           "MacAddress" : "1a:2b:3c:4d:5e:6f"
       }
  }
  ```
+ You can use the `start-service` command to start the Tape Gateway application service on your Snowball Edge device\. You must provide the `ServiceId` and `VirtualNetworkInterfaceArn` for the Tape Gateway application service\.

  ```
  snowballEdge start-service \
  --service-id tapegateway \
  --virtual-network-interface-arns arn:aws:snowball-device:::interface/s.ni-abcd1234abcd1234
  ```
+ You can use the `describe-service` command to check whether the Tape Gateway application service is active\. You must provide the Tape Gateway `ServiceId`\.

  ```
  snowballEdge describe-service —service-id service-id
                  
                      {
  "ServiceId" : "tapegateway",
    "Status" : {
      "State" : "ACTIVE"
    },
  "Storage" : {
  "TotalSpaceBytes" : 99608745492480,
  "FreeSpaceBytes" : 99608744468480
  },
  "Endpoints" : [ {
  "Protocol" : "iSCSI",
  "Port" : 860,
  "Host" : "192.0.2.0"
  }, {
  "Protocol" : "iSCSI",
  "Port" : 3260,
  "Host" : "192.0.2.0",
  } ]
  }
  ```

For more detailed information about the Snow Family API, see the [AWS Snow Family API Reference](https://docs.aws.amazon.com/snowball/latest/api-reference/api-reference.html)\.