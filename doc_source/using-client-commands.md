# Commands for the Snowball Edge Client<a name="using-client-commands"></a>

Following, you can find information on the Snowball Edge client commands, including examples of use and sample outputs\.

**Topics**
+ [Configuring a Profile for the Snowball Edge Client](#client-configuration)
+ [Getting Your QR Code for NFC Validation](#client-qr-code)
+ [Snowball Edge client version](#cli-version)
+ [Unlocking Snowball Edge Devices](#setting-up-client)
+ [Updating a Snowball Edge](#update-client-commands)
+ [Getting Credentials](#client-credentials)
+ [Starting a Service on Your Snowball Edge](#edge-start-service)
+ [Stopping a Service on Your Snowball Edge](#edge-stop-service)
+ [Getting Your Certificate for Transferring Data](#snowball-edge-certificates-cli)
+ [Starting NFS and Restricting Access](#sbe-start-nfs)
+ [Restricting Access to NFS Shares When NFS is Running](#sbe-restrict-access)
+ [AWS Snowball Edge Logs](#logs)
+ [Getting Device Status](#client-status)
+ [Getting Service Status](#client-service-status)
+ [Removing a Node from a Cluster](#client-cluster-remove)
+ [Adding a Node to a Cluster](#client-cluster-add)
+ [Creating Tags for Your Device](#client-create-tags)
+ [Deleting Tags from Your Device](#client-delete-tags)
+ [Describing Tags on Your Device](#client-describe-tags)
+ [Creating a Direct Network Interface](#sbe-networking-create-dni)
+ [Getting Information About a Direct Network Interface](#sbe-networking-describe-dni)
+ [Updating a Direct Network Interface](#sbe-networking-update-dni)
+ [Deleting a Direct Network Interface](#sbe-networking-delete-dni)
+ [Setting Time Servers](#client-set-ntp)
+ [Checking Time Sources](#client-describe-ntp)

## Configuring a Profile for the Snowball Edge Client<a name="client-configuration"></a>

Every time you run a command for the Snowball Edge client, you provide your manifest file, unlock code, and an IP address\. You can get the first two of these from the AWS Snow Family Management Console or the job management API\. For more information about getting your manifest and unlock code, see [Getting Credentials](#client-credentials)\.

You have the option of using the `snowballEdge configure` command to store the path to the manifest, the 29\-character unlock code, and the endpoint as a profile\. After configuration, you can use other Snowball Edge client commands without having to manually enter these values for a particular job\. After you configure the Snowball Edge client, the information is saved in a plaintext JSON format to `home directory/.aws/snowball/config/snowball-edge.config`\. 

The endpoint is the IP address, with `https://` added to it\. You can locate the IP address for the AWS Snowball Edge device on the AWS Snowball Edge device LCD display\. When the AWS Snowball Edge device is connected to your network for the first time, it automatically gets a DHCP IP address, if a DHCP server is available\. If you want to use a different IP address, you can change it from the LCD display\. For more information, see [Using an AWS Snowball Edge Device](using-device.md)\.

**Important**  
Anyone who can access the configuration file can access the data on your Snowball Edge devices or clusters\. Managing local access control for this file is one of your administrative responsibilities\.

**Usage**

You can use this command in two ways: inline, or when prompted\. This usage example shows the prompted method\.

```
snowballEdge configure
```

**Example Output**  

```
Configuration will stored at home directory\.aws\snowball\config\snowball-edge.config
Snowball Edge Manifest Path: /Path/to/manifest/file
Unlock Code: 29 character unlock code
Default Endpoint: https://192.0.2.0
```

You can have multiple profiles if you have multiple jobs at once, or if you want the option of managing a cluster from different endpoints\. For more information about multiple AWS CLI profiles, see [Named profiles](https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html) in the *AWS Command Line Interface User Guide*\.

## Getting Your QR Code for NFC Validation<a name="client-qr-code"></a>

You can use this command to generate a device\-specific QR code for use with the AWS Snowball Edge Verification App\. You can download this app from the Apple App Store or the Google Play store\. For more information about NFC validation, see [Validating NFC Tags](data-protection-device.md#nfc-validation)\.

**Usage**

```
snowballEdge get-app-qr-code --output-file ~/downloads/snowball-qr-code.png
```

**Example Output**  

```
QR code is saved to ~/downloads/snowball-qr-code.png
```

## Snowball Edge client version<a name="cli-version"></a>

Use the `snowball version` command to see the version of the Snowball Edge command line interface \(CLI\) client\.

### Usage<a name="cli-version-usage"></a>

```
    snowball version                
```

### Example output<a name="cli-version-output"></a>

```
    Snowball client version: 1.2.0  Build 254                
```

## Unlocking Snowball Edge Devices<a name="setting-up-client"></a>

To unlock a standalone AWS Snowball Edge device, run the `snowballEdge unlock-device` command\. To unlock a cluster, use the `snowballEdge unlock-cluster` command\. These commands authenticate your access to the AWS Snowball Edge device\.

**Note**  
To unlock the devices associated with your job, the devices must be on\-site, plugged into power and the network, and turned on\. In addition, the LCD display on the front of the AWS Snowball Edge device must indicate that the device is ready for use\.

**Usage**

```
snowballEdge unlock-device --endpoint https://192.0.2.0 --manifest-file Path/to/manifest/file --unlock-code 01234-abcde-ABCDE-01234
```

**Example Single Device Unlock Input**  

```
snowballEdge unlock-device --endpoint https://192.0.2.0 --manifest-file /usr/home/manifest.bin --unlock-code 01234-abcde-ABCDE-01234
```

**Example Single Device Unlock Output**  

```
Your Snowball Edge device is unlocking. You may determine the unlock state of your device using the describe-device command. Your Snowball Edge device will be available for use when it is in the UNLOCKED state.
```

**Cluster Usage**

When you unlock a cluster, you provide the endpoint for one of your nodes, and all the IP addresses for the other devices in your cluster\.

```
snowballEdge unlock-cluster --endpoint https://192.0.2.0 --manifest-file Path/to/manifest/file --unlock-code 01234-abcde-ABCDE-01234 --device-ip-addresses 192.0.2.0 192.0.2.1 192.0.2.2 192.0.2.3 192.0.2.4
```

**Example Cluster Unlock Output**  

```
Your Snowball Edge Cluster is unlocking. You may determine the unlock state of your cluster using the describe-device command. Your Snowball Edge Cluster will be available for use when your Snowball Edge devices are in the UNLOCKED state.
```

## Updating a Snowball Edge<a name="update-client-commands"></a>

Use the following commands to download and install updates for your Snowball Edge device\. For procedures that use these commands, see [Updating software on Snowball Edge devices](updating-device.md)\.

`snowballEdge check-for-updates` – Returns version information about the Snowball Edge software available in the cloud, and the current version installed on the device\. 

**Usage \(configured Snowball Edge client\)**

```
snowballEdge check-for-updates
```

**Example Output**  

```
Latest version: 102
Installed version: 101
```

`snowballEdge describe-device-software` – Returns the current software version for the device\. Additionally, if the update is being downloaded, the download state is also displayed\. If a software update is in progress, the version manifest of update, and state of installation is also displayed\. Following is a list of possible outputs:
+ `NA` – No software updates are currently in progress\.
+ `Downloading` – New software is being downloaded\.
+ `Installing` – New software is being installed\.
+ `Requires Reboot` – New software has been installed, and the device needs to be restarted\.
**Warning**  
We highly recommend that you suspend all activity on the device before you restart the device\. Restarting a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\. All of these processes can result in lost data\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge describe-device-software
```

**Example Output**  

```
Installed version: 101
Installing version: 102
Install State: Downloading
```

`snowballEdge download-updates` – Starts downloading the latest software updates for your Snowball Edge\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge download-updates
```

**Example Output**  

```
Download started. Run describe-device-software API for additional information.
```

`snowballEdge install-updates` – Starts installing the latest software updates for your Snowball Edge that were already downloaded\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge install-updates
```

**Example Output**  

```
Installation started.
```

`snowballEdge reboot-device` – Reboots the device\.

**Warning**  
We highly recommend that you suspend all activity on the device before you restart the device\. Restarting a device stops running instances, interrupts any writing to Amazon S3 buckets on the device, and stops any write operations from the file interface without clearing the cache\. All of these processes can result in lost data\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge reboot-device
```

**Example Output**  

```
Rebooting device now.
```

`snowballEdge configure-auto-update-strategies` – Configures an automatic update strategy\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge configure-auto-update-strategy --auto-check autoCheck [--auto-check-frequency
autoCheckFreq] --auto-download autoDownload
[--auto-download-frequency autoDownloadFreq]
--auto-install autoInstall
[--auto-install-frequency autoInstallFreq]
--auto-reboot autoReboot [--endpoint
endpoint]
```

**Example Output**  

```
Successfully configured auto update strategy. Run describe-auto-update-strategies for additional information.
```

`snowballEdge describe-auto-update-strategies` – Returns any currently configured automatic update strategy\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge describe-auto-update-strategies
```

**Example Output**  

```
auto-update-strategy {[
auto-check:true,
auto-check-frequency: "0 0 * * FRI", // CRON Expression String, Every Friday at midnight
auto-download:true,
auto-download-frequency: "0 0 * * SAT", // CRON Expression String, Every Saturday at
midnight
auto-install:true,
auto-install-frequency: "0 13 * * Sun", // CRON Expression String, Every Saturday at
midnight
auto-reboot: false;
]}
```

## Getting Credentials<a name="client-credentials"></a>

Using the `snowballEdge list-access-keys` and `snowballEdge get-secret-access-key` commands, you can get the credentials of the admin user of your AWS account on Snowball Edge\. You can use these credentials to create AWS Identity and Access Management \(IAM users\) and roles, and to authenticate your requests when using the AWS CLI or with an AWS SDK\. These credentials are only associated with an individual job for Snowball Edge, and you can use them only on the device or cluster of devices\. The device or devices don't have any IAM permissions in the AWS Cloud\.

**Note**  
If you're using the AWS CLI with the Snowball Edge, you must use these credentials when you configure the CLI\. For information about configuring credentials for the AWS CLI, see [Configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-quick-configuration) in the *AWS Command Line Interface User Guide*\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge list-access-keys
```

**Example Output**  

```
{
  "AccessKeyIds" : [ "AKIAIOSFODNN7EXAMPLE" ]
}
```

**Usage \(configured Snowball Edge client\)**

```
snowballEdge get-secret-access-key --access-key-id Access Key
```

**Example Output**  

```
[snowballEdge]
aws_access_key_id = AKIAIOSFODNN7EXAMPLE
aws_secret_access_key = wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

## Starting a Service on Your Snowball Edge<a name="edge-start-service"></a>

Snowball Edge devices support multiple services, in addition to Amazon S3\. These include compute instances, the file interface, and AWS IoT Greengrass\. Amazon S3 and Amazon EC2 are always on by default, and can't be stopped or restarted with the Snowball Edge client\. However, the file interface and AWS IoT Greengrass can be started with the `snowballEdge start-service` command\. To get the service ID for each service, you can use the `snowballEdge list-services` command\.

Before you run this command, create a single virtual network interface to bind to the service that you're starting\. For more information, see [Creating a Virtual Network Interface](using-ec2-edge-client.md#ec2-edge-create-vnic)\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge start-service --service-id service_id --virtual-network-interface-arns virtual-network-interface-arn
```

**Example Output**  

```
Starting the AWS service on your Snowball Edge. You can determine the status of the AWS service using the describe-service command.
```

## Stopping a Service on Your Snowball Edge<a name="edge-stop-service"></a>

To stop a service running on your Snowball Edge, you can use the `snowballEdge stop-service` command\. 

The Amazon S3, Amazon EC2, AWS STS, and IAM services cannot be stopped\.

**Warning**  
Data loss can occur if the file interface is stopped before remaining buffered data is written to the device\. For more information on using the file interface, see [Transferring Files to Snowball Edge devices using the File Interface](using-fileinterface.md)\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge stop-service --service-id service_id
```

**Example Output**  

```
Stopping the AWS service on your Snowball Edge. You can determine the status of the AWS service using the describe-service command.
```

## Getting Your Certificate for Transferring Data<a name="snowball-edge-certificates-cli"></a>

To transfer data to a Snowball Edge, use the Amazon S3 interface\. To use the S3 interface over the HTTPS protocol, you must provide a certificate\. The certificates are generated by each Snowball Edge device\. If you unlock your Snowball Edge device with a different IP address, a new certificate is generated and the old certificate is no longer valid to use with the endpoint\. You can get the new, updated certificate from the Snowball Edge again using the `get-certificate` command\.

You can list these certificates and download them from your Snowball Edge device with the following commands:
+ `list-certificates` – Lists the Amazon Resource Names \(ARNs\) for the certificates available for use\.

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge list-certificates
  ```  
**Example Output**  

  ```
  {
    "Certificates" : [ {
      "CertificateArn" : "arn:aws:snowball-device:::certificate/78EXAMPLE516EXAMPLEf538EXAMPLEa7",
      "SubjectAlternativeNames" : [ "192.0.2.0" ]
    } ]
  }
  ```
+ `get-certificate` – Gets a specific certificate, based on the ARN provided\.

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge get-certificate --certificate-arn arn:aws:snowball-device:::certificate/78EXAMPLE516EXAMPLEf538EXAMPLEa7
  ```  
**Example Output**  

  ```
  -----BEGIN CERTIFICATE-----
  Certificate
  -----END CERTIFICATE-----
  ```

  For information about configuring your certificate, see [Specifying the S3 Interface as the AWS CLI Endpoint](using-adapter.md#using-adapter-cli-endpoint)\.

## Starting NFS and Restricting Access<a name="sbe-start-nfs"></a>

**Important**  
Don't start the NFS service if you intend to use Amazon Elastic Block Store \(Amazon EBS\)\. The first time NFS is started, all storage is allocated to NFS\. It is not possible to reallocate NFS storage to Amazon EBS, even if the NFS service is stopped\.  
You can provide CIDR blocks for IP ranges that are allowed to mount the NFS shares exposed by the device\. For example, `10.0.0.0/16`\. If you don't provide allowed CIDR blocks, all mount requests will be denied\.  
Be aware that data transferred through NFS is not encrypted in transit\.  
Other than the allowed hosts by CIDR blocks, Snowcone doesn't provide an authentication or authorization mechanism for the NFS shares\.

Start NFS with the `snowballEdge start-service` command\. To get the service ID for the NFS service, you can use the `snowballEdge list-services` command\.

Before you run this command, create a single virtual network interface to bind to the service that you're starting\. For more information, see [Creating a Virtual Network Interface](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-ec2-edge-client.html#ec2-edge-create-vnic)\. You can restrict access to your file shares and data in your Amazon S3 buckets and see what restrictions are currently in place\. You do this by allocating CIDR blocks for allowed hosts that can access your file share and S3 buckets when you start the NFS service\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge start-service --service-id nfs --virtual-network-interface-arns arn:aws:snowball-device:::interface/s.ni-12345fgh45678j --service-configuration AllowedHosts=ip address-1/32,ip address-2/24
```

**Example Output**  

```
Starting the service on your Snowball Edge. You can determine the status of the service using the describe-service command.
```

## Restricting Access to NFS Shares When NFS is Running<a name="sbe-restrict-access"></a>

You can restrict access your file shares and data in your Amazon S3 buckets after you have started NFS\. You can see what restrictions are currently in place, and give each bucket different access restrictions\. You do this by allocating CIDR blocks for hosts that can access your file share and S3 buckets when you start the NFS service\. The following is an example command\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge start-service \
    --service-id nfs \
    --virtual-network-interface-arns virtual-network-interface-arn --service-configuration AllowedHosts=ip-address-1/32,ip-address-1/24
```

To see the current restrictions, use the `describe-service` command\.

```
 snowballEdge describe-service --service-id nfs
```

## AWS Snowball Edge Logs<a name="logs"></a>

When you transfer data between your on\-premises data center and a Snowball Edge, logs are automatically generated\. If you encounter unexpected errors during data transfer to the device, you can use the following commands to save a copy of the logs to your local server\.

There are three commands related to logs:
+ `list-logs` – Returns a list of logs in JSON format\. This list reports the size of the logs in bytes, the ARN for the logs, the service ID for the logs, and the type of logs\. 

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge list-logs
  ```  
**Example Output**  

  ```
  {
    "Logs" : [ {
      "LogArn" : "arn:aws:snowball-device:::log/s3-storage-JIEXAMPLE2f-1234-4953-a7c4-dfEXAMPLE709",
      "LogType" : "SUPPORT",
      "ServiceId" : "s3",
      "EstimatedSizeBytes" : 53132614
    }, {
      "LogArn" : "arn:aws:snowball-device:::log/fileinterface-JIDEXAMPLEf-1234-4953-a7c4-dfEXAMPLE709",
      "LogType" : "CUSTOMER",
      "ServiceId" : "fileinterface",
      "EstimatedSizeBytes" : 4446
    }]
  }
  ```
+ `get-log` – Downloads a copy of a specific log from the Snowball Edge to your server at a specified path\. `CUSTOMER` logs are saved in the `.zip` format, and you can extract this type of log to view its contents\. `SUPPORT` logs are encrypted and can only be read by AWS Support engineers\. You have the option of specifying a name and a path for the log\. 

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge get-log --log-arn arn:aws:snowball-device:::log/fileinterface-JIDEXAMPLEf-1234-4953-a7c4-dfEXAMPLE709
  ```  
**Example Output**  

  ```
  Logs are being saved to download/path/snowball-edge-logs-1515EXAMPLE88.bin
  ```
+ `get-support-logs` – Downloads a copy of all the `SUPPORT` type of logs from the Snowball Edge to your service at a specified path\.

  **Usage \(configured Snowball Edge client\)**

  Snowball Edge client

  ```
  snowballEdge get-support-logs
  ```  
**Example Output**  

  ```
  Logs are being saved to download/path/snowball-edge-logs-1515716135711.bin
  ```

**Important**  
`CUSTOMER` type might contain sensitive information about your own data\. To protect this potentially sensitive information, we strongly suggest that you delete these logs once you're done with them\.

## Getting Device Status<a name="client-status"></a>

You can determine the status and general health of your Snowball Edge devices with the following Snowball Edge client commands:
+ `describe-device`

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge describe-device
  ```  
**Example Output**  

  ```
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
      "PhysicalNetworkInterfaceId" : "s.ni-EXAMPLE0a3a6499fd",
      "PhysicalConnectorType" : "SFP_PLUS",
      "IpAddressAssignment" : "DHCP",
      "IpAddress" : "192.168.1.231",
      "Netmask" : "255.255.255.0",
      "DefaultGateway" : "192.0.2.3",
      "MacAddress" : "EX:AM:PL:E0:90:12"
    } ]
  }
  ```
+ `describe-cluster`

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge describe-cluster
  ```  
**Example Output**  

  ```
  {
    "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5",
    "Devices" : [ {
      "DeviceId" : "JIDEXAMPLE2-bc53-4618-a538-917EXAMPLE94",
      "UnlockStatus" : {
        "State" : "UNLOCKED"
      },
      "ActiveNetworkInterface" : {
        "IpAddress" : "192.0.2.0"
      },
      "ClusterAssociation" : {
        "State" : "ASSOCIATED",
        "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5"
      },
      "NetworkReachability" : {
        "State" : "REACHABLE"
      }
    }, {
      "DeviceId" : "JIDEXAMPLE2-bc53-4618-a538-917EXAMPLE94",
      "UnlockStatus" : {
        "State" : "UNLOCKED"
      },
      "ActiveNetworkInterface" : {
        "IpAddress" : "192.0.2.1"
      },
      "ClusterAssociation" : {
        "State" : "ASSOCIATED",
        "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5"
      },
      "NetworkReachability" : {
        "State" : "REACHABLE"
      }
    }, {
      "DeviceId" : "JIDEXAMPLE2-bc53-4618-a538-917EXAMPLE94",
      "UnlockStatus" : {
        "State" : "UNLOCKED"
      },
      "ActiveNetworkInterface" : {
        "IpAddress" : "192.0.2.2"
      },
      "ClusterAssociation" : {
        "State" : "ASSOCIATED",
        "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5"
      },
      "NetworkReachability" : {
        "State" : "REACHABLE"
      }
    }, {
      "DeviceId" : "JIDEXAMPLE2-bc53-4618-a538-917EXAMPLE94",
      "UnlockStatus" : {
        "State" : "UNLOCKED"
      },
      "ActiveNetworkInterface" : {
        "IpAddress" : "192.0.2.3"
      },
      "ClusterAssociation" : {
        "State" : "ASSOCIATED",
        "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5"
      },
      "NetworkReachability" : {
        "State" : "REACHABLE"
      }
    }, {
      "DeviceId" : "JIDEXAMPLE2-bc53-4618-a538-917EXAMPLE94",
      "UnlockStatus" : {
        "State" : "UNLOCKED"
      },
      "ActiveNetworkInterface" : {
        "IpAddress" : "192.0.2.4"
      },
      "ClusterAssociation" : {
        "State" : "ASSOCIATED",
        "ClusterId" : "CIDEXAMPLE7-5402-4c19-9feb-7c9EXAMPLEd5"
      },
      "NetworkReachability" : {
        "State" : "REACHABLE"
      }
    } ]
  }
  ```

## Getting Service Status<a name="client-service-status"></a>

You can determine the status and general health of the services running on Snowball Edge devices with the `describe-service` command\. You can first run the `list-services` command to see what services are running\.
+ `list-services`

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge list-services
  ```  
**Example Output**  

  ```
  {
    "ServiceIds" : [ “greengrass”, "fileinterface", "s3", "ec2" ]
  }
  ```
+ `describe-service`

  This command returns a status value for a service\. It also includes state information that might be helpful in resolving issues you encounter with the service\. Those states are as follows\.
  + `ACTIVE` – The service is running and available for use\.
  + `ACTIVATING` – The service is starting up, but it is not yet available for use\.
  + `DEACTIVATING` – The service is in the process of shutting down\.
  + `INACTIVE` – The service is not running and is not available for use\.

  **Usage \(configured Snowball Edge client\)**

  ```
  snowballEdge describe-service --service-id service-id
  ```  
**Example Output**  

  ```
  {
  "ServiceId" : "s3",
    "Status" : {
      "State" : "ACTIVE"
    },
  "Storage" : {
  "TotalSpaceBytes" : 99608745492480,
  "FreeSpaceBytes" : 99608744468480
  },
  "Endpoints" : [ {
  "Protocol" : "http",
  "Port" : 8080,
  "Host" : "192.0.2.0"
  }, {
  "Protocol" : "https",
  "Port" : 8443,
  "Host" : "192.0.2.0",
  "CertificateAssociation" : {
  "CertificateArn" : "arn:aws:snowball-device:::certificate/6d955EXAMPLEdb71798146EXAMPLE3f0"
  }
  } ]
  }
  ```

## Removing a Node from a Cluster<a name="client-cluster-remove"></a>

The `disassociate-device` command removes a node from a Snowball Edge cluster\. If you want to replace an unhealthy node, use this command\. For more information about clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\.

**Important**  
Use the `disassociate-device` command only when you are removing an unhealthy node\. This command fails and returns an error if you try to remove a healthy node\.

Don't use this command to remove a node that was accidentally powered off or disconnected from the network and is therefore temporarily unavailable to the rest of the cluster\. Nodes removed with this command can't be added to any cluster, and must be returned to AWS\.

If a node was accidentally powered off or disconnected from the network, plug the node back into power and the network, and use the `associate-device` command\. You can't use the `disassociate-device` command to disassociate a node if it's powered on and healthy\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge disassociate-device --device-id Job ID for the Device
```

**Example Output**  

```
Disassociating your Snowball Edge device from the cluster. Your Snowball Edge device will be disassociated from the cluster when it is in the "DISASSOCIATED" state. You can use the describe-cluster command to determine the state of your cluster.
```

## Adding a Node to a Cluster<a name="client-cluster-add"></a>

The `associate-device` command adds a node to a cluster of Snowball Edge devices\. If you power off a node, it reverts from being unlocked to being locked\. To unlock that node, you can use this command\. Use this command to replace an unavailable node with a new node that you ordered as a replacement\. For more information about clusters, see [Using an AWS Snowball Edge Cluster](UsingCluster.md)\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge associate-device --device-ip-address IP Address
```

**Example Output**  

```
Associating your Snowball Edge device with the cluster. Your Snowball Edge device will be associated with the cluster when it is in the ASSOCIATED state. You can use the describe-cluster command to determine the state of your cluster.
```

## Creating Tags for Your Device<a name="client-create-tags"></a>

Adds or overwrites the specified tags on your device\. You can create a maximum of 50 tags\. Each tag consists of a key\-value pair\. The value is optional\. 

**Note**  
Don't put sensitive data in your tags\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge create-tags --tag Key=Name,Value=user-test --tag Key=Stage,Value=beta
```

For more information, run the `describe-tags` command\.

**Example Output**  

```
Tag(s) [Key=Name,Value=test, Key=Stage,Value=beta] created.
```

## Deleting Tags from Your Device<a name="client-delete-tags"></a>

The `delete-tags` command deletes the specified tags from your Snowball Edge device\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge delete-tags --tag Key=Stage,Value=beta
    Tag(s) [Key=Stage,Value=beta] deleted.
```

For more information, run the `describe-tags` command\.

**Note**  
If you want to delete multiple tags at the same time, you can specify multiple key\-value pairs, like the following:  
 `delete-tags --tag Key=Name,Value=test --tag Key=Stage,Value=Beta`  
If you specify a tag key without a tag value, any tag with this key regardless of its value is deleted\. If you specify a tag key with an empty string as the tag value, only tags that have an empty string as the value are deleted\.

## Describing Tags on Your Device<a name="client-describe-tags"></a>

The `describe-tags` command describes the tags on your Snowball Edge device\.

**Usage \(configured Snowball Edge client\)**

```
snowballEdge describe-tags
```

For more information, run the `describe-tags` command\.

**Example Output**  

```
{
  "Tags" : [ {
    "Key" : "Name",
    "Value" : "user-test"
  }, {
    "Key" : "Stage",
    "Value" : "beta"
  } ]
}
```

## Creating a Direct Network Interface<a name="sbe-networking-create-dni"></a>
+ `create-direct-network-interface ` – Creates a direct network interface \(DNI\)\. Creates a direct network interface to use with Amazon EC2 compute instances on your device\. You can find the direct network interfaces available on your device by using the `describe-direct-network-interfaces` command\. 

**Usage \(configured Snowball Edge client\)**

```
snowballEdge create-direct-network-interface [--endpoint endpoint] [--instance-id instanceId] [--mac macAddress]
                                [--manifest-file manifestFile] [--physical-network-interface-id physicalNetworkInterfaceId] 
                                [--profile profile] [--unlock-code unlockCode] [--vlan vlanId]
```

## Getting Information About a Direct Network Interface<a name="sbe-networking-describe-dni"></a>
+ `describe-direct-network-interface ` – Gets the direct network interfaces on your device\. A direct network interface can be used to configure networking for Amazon EC2 compute instances and services on your device\. You can create a new direct network interface by using the `create-direct-network-interface` command\. 

**Usage \(configured Snowball Edge client\)**

```
snowballEdge describe-direct-network-interfaces [--endpoint endpoint] [--manifest-file manifestFile] [--profile profile] [--unlock-code unlockCode]
```

## Updating a Direct Network Interface<a name="sbe-networking-update-dni"></a>
+ `update-direct-network-interface ` – Updates a direct network interface\. Use this command to update a direct network interface that will be used with Amazon EC2 compute instances on your device\. You can find the direct network interfaces that are available on your device by using the `describe-direct-network`\-interfaces command\. When you are modifying a network interface that is attached to an Amazon EC2 instance, the interface will first be detached\. 

**Usage \(configured Snowball Edge client\)**

```
snowballEdge update-direct-network-interface [--direct-network-interface-arn directNetworkInterfaceArn] [--endpoint endpoint] 
                                [--mac macAddress]
                                [--manifest-file manifestFile] [--profile profile] [--unlock-code unlockCode] 
                                [--vlan vlanId] [--attach-instance-id instanceId | --detach]
```

## Deleting a Direct Network Interface<a name="sbe-networking-delete-dni"></a>
+ `delete-direct-network-interface` – Deletes a direct network interface that is no longer in use\. To delete a direct network interface associated with your Amazon EC2 compute instance, you must first disassociate the direct network interface from your instance\. 

**Usage \(configured Snowball Edge client\)**

```
snowballEdge delete-direct-network-interface [--direct-network-interface-arn directNetworkInterfaceArn] [--endpoint endpoint] 
                                [--manifest-file manifestFile] [--profile profile] [--unlock-code unlockCode]
```

## Setting Time Servers<a name="client-set-ntp"></a>

You can set up an external Network Time Protocol \(NTP\) server\. You can use the NTP CLI commands when the device is in both locked and unlocked states\. The manifest and unlock code are required\. You can set these either with the `snowballEdge configure` command or by using the `--manifest-file` and `--unlock-code` options\. Note that you can use the `snowballEdge` CLI on both AWS Snowcone Edge and AWS Snowcone\.

It is your responsibility to provide a secure NTP time server\. To set which NTP time servers the device connects to, use the `update-time-servers` CLI command\.

**Note**  
The `update-time-servers` command will override the previous NTP time servers settings\.

**Supported NTP device types and software versions**  
NTP isn't available on any version 2 storage and compute device types\. Snowball Edge version 3 storage and compute device types with software version 77 or later support NTP, however\. To check if NTP is enabled, use the Snowball Edge CLI command `describe-time-sources`\.

**Usage**

```
snowballEdge update-time-servers time.google.com
```

**Example Output**  

```
Updating time servers now.
```

## Checking Time Sources<a name="client-describe-ntp"></a>

To see which NTP time sources the device are currently connected to, use the `describe-time-sources` Snowball Edge CLI command\.

**Usage**

```
snowballEdge describe-time-sources
```

**Example Output**  

```
{
  "Sources" : [ {
    "Address" : "172.31.2.71",
    "State" : "LOST",
    "Type" : "PEER",
    "Stratum" : 10
  }, {
    "Address" : "172.31.3.203",
    "State" : "LOST",
    "Type" : "PEER",
    "Stratum" : 10
  }, {
    "Address" : "172.31.0.178",
    "State" : "LOST",
    "Type" : "PEER",
    "Stratum" : 10
  }, {
    "Address" : "172.31.3.178",
    "State" : "LOST",
    "Type" : "PEER",
    "Stratum" : 10
  }, {
    "Address" : "216.239.35.12",
    "State" : "CURRENT",
    "Type" : "SERVER",
    "Stratum" : 1
  } ]
}
```

The `describe-time-sources` command returns a list of time source states\. Each time source state contains the `Address`, `State`, `Type`, and `Stratum` fields\. Following are the meanings of these fields\.
+ `Address` – The DNS name / IP address of the time source\.
+ `State` – The current connection status between the device and that time source\. There are five possible states:\.
  + `CURRENT` – The time source is currently being used to synchronize time\.
  + `COMBINED` – The time source is combined with the current source\.
  + `EXCLUDED` – The time source is excluded by the combining algorithm\.
  + `LOST` – The connection with the time source has been lost\.
  + `UNACCEPTABLE` – An invalid time source where the combining algorithm has deemed to be either a falseticker or has too much variability\.
+ `Type` – An NTP time source can be either a server or a peer\. Servers can be set by the `update-time-servers` command\. Peers can only be other Snowball Edge devices in the cluster and are automatically set up when the cluster is associated\.
+ `Stratum` – This field shows the stratum of the source\. Stratum 1 indicates a source with a locally attached reference clock\. A source that is synchronized to a stratum 1 source is at stratum 2\. A source that is synchronized to a stratum 2 source is at stratum 3, and so on\.\.

An NTP time source can either be a server or a peer\. A server can be set by the user with the `update-time-servers` command, whereas a peer could only be other Snowball Edge devices in the cluster\. In the example output, `describe-time-sources` is called on a Snowball Edge that is in a cluster of 5\. The output contains 4 peers and 1 server\. The peers have a stratum of 10 while the server has a stratum of 1; therefore, the server is selected to be the current time source\.