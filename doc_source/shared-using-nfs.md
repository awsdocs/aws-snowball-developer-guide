# Using NFS for Offline Data Transfer<a name="shared-using-nfs"></a>

Your Snow Family device contains a file interface that provides access to the internal device storage\. To import your data offline to Amazon S3 with your Snow Family device, you connect the device to your on\-premises network and then use AWS OpsHub to unlock it\. You can copy data from on\-premises storage devices to the Snow Family device through the NFS file interface\. 

After you copy the data to the Snow Family device, the E Ink shipping label will be updated to ensure that the device is automatically sent to the correct AWS facility\. You can track the Snow Family device by using Amazon SNS generated text messages or emails, and the console\. For information about AWS OpsHub, see [Using AWS OpsHub for Snow Family to Manage Devices](aws-opshub.md)\.

**Note**  
File names are object keys in your local S3 bucket on the Snow Family device\. The key name is a sequence of Unicode characters whose UTF\-8 encoding is at most 1,024 bytes long\. We recommend using NFSv4\.1 where possible and encode file names with Unicode UTF\-8 to ensure a successful data import\. File names that are not encoded with UTF\-8 might not be uploaded to S3 or might be uploaded to S3 with a different file name depending on the NFS encoding you use\.  
Ensure that the maximum length of your file path is less than 1024 characters\. Snow Family devices do not support file paths that are greater that 1024 characters\. Exceeding this file path length will result in file import errors\.  
For more information, see [Object keys](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon Simple Storage Service User Guide*\.

You can transfer up to 8 TB with a single Snowcone device and transfer larger datasets with multiple devices, either in parallel, or sequentially\. For example, you can transfer 24 TB of data with three Snowcone devices\. For larger data transfers jobs, you can use the Snowball Edge Storage Optimized device\. You can transfer up to 80 TB with a single Snowball Edge Storage Optimized device and transfer larger datasets with multiple devices, either in parallel, or sequentially\.

**Note**  
You can only transfer up to 40M files using a single Snow Family device\. If you require to transfer more than 40M files in a single job, please batch the files in order to reduce the file numbers per each transfer\. Individual files can be of any size with a maximum file size of 5 TB for Snowball Edge devices with the NFS file interface and 150 GB for Snowball Edge devices with the S3 interface\.
You can provide CIDR blocks for IP ranges that are allowed to mount the NFS shares exposed by the device\. For example, `10.0.0.0/16`\. If you don't provide allowed CIDR blocks, all mount requests will be denied\. For details, see [ Restricting Access to NFS Shares When NFS is Running](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#sbe-restrict-access)\.
For NFS based transfers, standard POSIX style meta\-data will be added to your objects as they get imported to Amazon S3 from Snowball Edge\. In addition, you'll see meta\-data "x\-amz\-meta\-user\-agent aws\-datasync" as we currently use AWS DataSync as part of the internal import mechanism to Amazon S3 for Snowball Edge import with NFS option\. 

## NFS configuration for Snow Family devices<a name="NFS-interface-configuration"></a>

NFS is ubiquitous \(existing or being everywhere at the same time\)\. Every laptop, workstation, and server has an IP connection and every modern operating system has a built\-in NFS client\. Object storage systems typically use the Amazon S3 API which is less ubiquitous than NFS, especially in the private data center\. Amazon S3 does not support NFS\. Hence before ordering the Snow Family device, you must decide to use either the Amazon S3 interface or NFS interface\. If you choose the NFS interface, mount NFS bucket of the Snow Family device as a volume\.

**Prerequisite**  

+ 2 IP addresses:
  + One for physical network interface to activate Snow Family device \(e\.g\. 192\.168\.0\.9\)
  + The 2nd for virtual network interface to mount the Snow Family device NFS volume \(e\.g\. 192\.168\.0\.10\)
+ Workstation

### Configure Snow Family devices<a name="How-to-configure-SBE"></a>

**Confirm the NFS service is active**  


```
snowballEdge describe-service --service-id nfs --profile sbe1
{
  "ServiceId" : "nfs",
  "Status" : {
    "State" : "ACTIVE"
  }
}
```

If the value of the `State` name is `Active`, you can mount the Snow Family device NFS volume, otherwise you have to re\-start the service or create virtual network interface\.

### Create a virtual network interface and start the NFS service<a name="virtual-network-IFC-StartNFSService"></a>

**Check if virtual network interface exists**  


```
$ snowballEdge describe-virtual-network-interfaces --profile sbe1
```

**Identify physical interface ID**  


```
$ snowballEdge describe-device --profile sbe1
```

**Create virtual network interface and identify the virtual network interface \(VNI\) ARN**  


```
$snowballEdge create-virtual-network-interface \
     --physical-network-interface-id s.ni-abcd1234 \
     --ip-address-assignment STATIC \
     --static-ip-address-configuration IpAddress=192.168.0.10,Netmask=255.255.255.0
     --profile sbe1
```

**Start the NFS service**  


```
$ snowballEdge start-service --virtual-network-interface-arns arn:aws:snowball-device:::interface/s.ni-8712e3a5cb180e65d --service-id nfs --service-configuration AllowedHosts=0.0.0.0/0 —profile sbe1
```

**Check service status**  


```
$ snowballEdge describe-service --service-id nfs --profile sbe1

{
 "ServiceId" : "nfs",
 "Status" : {
 "State" : "ACTIVE"
 },
 "Endpoints" : [ {
 "Protocol" : "nfs",
 "Port" : 2049,
 "Host" : "192.168.0.10"
 } ],
 "ServiceConfiguration" : {
 "AllowedHosts" : [ "192.168.0.6/32", "11.160.2.156/32", "192.168.0.10/32" ]
 }
}
```

### Mount the Snow Family device NFS volume<a name="MountSBE"></a>

On the workstation, you can mount the Snow Family device volume which is the bucket name of NFS storage\.

```
$ sudo mkdir /mnt/local
$ sudo mount -t nfs 192.168.0.10:/buckets/your-nfs-bucket-name /mnt/local
```

After mounting SBE volume, you can check the volume size with ‘df’ command\.

```
$ df -h* */mnt/local
Filesystem            Size  Used Avail Use% Mounted on
192.168.0.10          80TB  20G   79TB  1%  /mnt/local
```

**Note**  
Check capacity of mounting point **/mnt/local** , shows near “80TB” available capacity for storage optimized Snow Family devices, as an example\. 
For more information, see [NFS data transfer for Storage Optimized devices](https://aws.amazon.com/about-aws/whats-new/2021/08/aws-snowball-edge-storage-optimized-nfs-data-transfer/)\.

## Troubleshooting NFS issues<a name="troubleshoot-nfs"></a>

The following are errors you might encounter when using NFS on Snow Family devices\.

**I Get a DEACTIVATED error message**  
You get this message if you turn off your Snow Family device without first stopping the NFS service\. The next time you start NFS, it might fail with a DEACTIVATED error message\. 

For example: Starting the service on your Snowball Edge\.

`snowballEdge start-service --service-id nfs --virtual-network-interface-arns arn:aws:snowball-device:::interface/s.ni-84991da69040a7xxx` 

 You can determine the status of the service by using the `describe-service` command\. 

```
snowballEdge describe-service --service-id nfs
{
  "ServiceId" : "nfs",
  "Status" : {
    "State" : "DEACTIVATED"
  }
}
```

**How To Correct the Issue**  
To correct the problem, stop and restart the NFS service using the following steps\.

 Step 1: Use the `describe-service` command to determine the status of the service:

```
snowballEdge describe-service --service-id nfs
{
  "ServiceId" : "nfs",
  "Status" : {
    "State" : "DEACTIVATED"
  }
}
```

Step 2: Use the `stop-service` command to stop the NFS service:

```
snowballEdge stop-service --service-id nfs --profile 11
```

Step 3: Use the `start-service` command to start the NFS service normally:

```
snowballEdge start-service  --virtual-network-interface-arns arn:aws:snowball-device:::interface/s.ni-8712e3a5cb180e65d --service-id nfs  --service-configuration  AllowedHosts=0.0.0.0/0  --profile 11
```

Step 4: Use the `describe-service` command to make sure the service is ACTIVE:

snowballEdge describe\-service \-\-service\-id nfs

```
{
 "ServiceId" : "nfs",
 "Status" : {
 "State" : "ACTIVE"
 },
 "Endpoints" : [ {
 "Protocol" : "nfs",
 "Port" : 2049,
 "Host" : "192.168.0.10"
 } ],
 "ServiceConfiguration" : {
 "AllowedHosts" : [ "192.168.0.6/32", "11.160.2.156/32", "192.168.0.10/32" ]
 }
}
```