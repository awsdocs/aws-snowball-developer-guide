# Using NFS for Offline Data Transfer<a name="shared-using-nfs"></a>

**Note**  
The NFS interface for Snowball Edge devices is only available on NFS based data transfer type jobs\. This is only available if specified at job creation\. Do keep in mind that the other Snow services \(S3 interface, File interface, etc\.\) will not be available when selecting this transfer type\.

Your Snow Family device contains a file interface that provides access to the internal device storage\. To import your data offline to Amazon S3 with your Snow Family device, you connect the device to your on\-premises network and then use AWS OpsHub to unlock it\. You can copy data from on\-premises storage devices to the Snow Family device through the NFS file interface\. 

After you copy the data to the Snow Family device, the E Ink shipping label will be updated to ensure that the device is automatically sent to the correct AWS facility\. You can track the Snow Family device by using Amazon SNS generated text messages or emails, and the console\. For information about AWS OpsHub, see [Using AWS OpsHub for Snow Family to Manage Devices](aws-opshub.md)\.

**Note**  
File names are object keys in your local S3 bucket on the Snow Family device\. The key name is a sequence of Unicode characters whose UTF\-8 encoding is at most 1,024 bytes long\. We recommend using NFSv4\.1 where possible and encode file names with Unicode UTF\-8 to ensure a successful data import\. File names that are not encoded with UTF\-8 might not be uploaded to S3 or might be uploaded to S3 with a different file name depending on the NFS encoding you use\.  
Ensure that the maximum length of your file path is less than 1024 characters\. Snow Family devices do not support file paths that are greater that 1024 characters\. Exceeding this file path length will result in file import errors\.  
For more information, see [Object keys](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html#object-keys) in the *Amazon Simple Storage Service User Guide*\.

You can transfer up to 8 TB with a single Snowcone device and transfer larger datasets with multiple devices, either in parallel, or sequentially\. For example, you can transfer 24 TB of data with three Snowcone devices\. For larger data transfers jobs, you can use the Snowball Edge Storage Optimized device\. You can transfer up to 80 TB with a single Snowball Edge Storage Optimized device and transfer larger datasets with multiple devices, either in parallel, or sequentially\.

**Note**  
You can provide CIDR blocks for IP ranges that are allowed to mount the NFS shares exposed by the device\. For example, `10.0.0.0/16`\. If you don't provide allowed CIDR blocks, all mount requests will be denied\. For details, see [ Restricting Access to NFS Shares When NFS is Running](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#sbe-restrict-access)\.
Be aware that data transferred through NFS is not encrypted in transit\.
Other than the allowed hosts by CIDR blocks, your Snow Family device doesn't provide an authentication or authorization mechanism for the NFS shares\.
For local compute jobs, the device doesn't ship with NFS configure on it so your data will not be imported into Amazon S3\.

## Troubleshooting NFS Issues<a name="troubleshoot-nfs"></a>

The following are errors you might encounter when using NFS on \.

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