# Using NFS file shares to manage file storage<a name="manage-nfs"></a>

You can use AWS OpsHub to upload files to your device and move them to other locations or the AWS Cloud when you return the device, or use AWS DataSync to transfer files\.



**Topics**
+ [Mounting NFS on a Windows client](#mount-nfs-on-window-client)
+ [Configuring NFS automatically \(quick setup\)](#auto-configure-nfs)
+ [Configuring NFS manually](#configure-with-snowcone)
+ [Stopping data transfer](#stop-nfs)

You can configure your Snow Family device as an NFS file system and use your native file system to manage files on your device\. You can upload files from an on\-premises location to your device and then transfer the files to AWS or move them to other locations\. You can use the AWS OpsHub defaults to configure NFS automatically or you can configure it manually yourself\.

**Note**  
Available storage space on the Snowcone device is not accurate until the NFS service is started\.  
You can provide CIDR blocks of IP ranges that are allowed to mount the NFS shares exposed by the device\. For example, `10.0.0.0/16`\. If you don't provide allowed CIDR blocks, all mount requests will be denied\.  
Be aware that data transferred through NFS is not encrypted in transit\.  
Other than the allowed hosts by CIDR blocks, your Snow Family device doesn't provide any authentication or authorization mechanism for the NFS shares\.

**Note**  
File names are object keys\. The name for a key is a sequence of Unicode characters whose UTF\-8 encoding is at most 1,024 bytes long\. We recommend using NFSv4\.1 where possible and encode file names with Unicode UTF\-8 to ensure a successful data import\. File names that are not encoded with UTF\-8 might not be uploaded to S3 or might be uploaded to S3 with a different file name, depending on the NFS encoding that you use\.  
Ensure that the maximum length of your file path is less than 1024 characters\. Snow Family devices do not support file paths that are greater that 1024 characters\. Exceeding this file path length will result in file import errors\.  
For more information, see [Working with object metadata](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMetadata.html#object-keys) in the *Amazon Simple Storage Service User Guide*\.

## Mounting NFS on a Windows client<a name="mount-nfs-on-window-client"></a>

If your client computer is using Windows 10 Enterprise or Windows 7 Enterprise, you first must start NFS service on Windows before you configure NFS in the AWS OpsHub application\.

**To mount NFS on a Windows client**

1. On your client computer, open **Start**, choose **Control Panel** and choose **Programs**\.

1. Choose **Turn Windows features on or off**\.

1. Under **Services for NFS**, choose **Client for NFS** and choose **OK**\.

## Configuring NFS automatically \(quick setup\)<a name="auto-configure-nfs"></a>

The NFS service is not running on the device by default so you need to start it to enable data transfer on the device\. With a few clicks, your Snow Family device can automatically figure NFS for you, or you can configure it manually yourself\. 

**Note**  
In Linux, mounting and unmount NFS endpoints requires root permissions\.

**To start and enable NFS on your Snow Family device automatically**

1. In the **Transfer data** section on the dashboard, choose **Enable & start**\. This could take a minute or two to complete\.   
![\[File storage dashboard showing Enable and start button.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub_enable_start_nfs_console.png)

1. When the NFS service is started, the IP address of the NFS server is shown on the dashboard and the **Transfer data** section indicates that the service is active\.

1. Choose **Open in Explorer** \(in Windows and Linux\) to open the file share in your client's file browser and start transferring files from your client to your Snow Family device\. You can copy and paste, or drag and drop files from your client computer into the file share\. In Windows, your file share looks like the following `buckets(\\12.123.45.679)(Z:)`\.

   

## Configuring NFS manually<a name="configure-with-snowcone"></a>

You can manually configure NFS by providing IP address \(VNI\) and restrict access to your file share\.

This video shows how to configure NFS manually using AWS OpsHub\.

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/StMa2A7X2yA?start=78&end=119/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/StMa2A7X2yA?start=78&end=119)

**To configure NFS manually**

1. At the bottom of **Transfer data** section, on the dashboard, choose **Configure manually**\. 

1. Choose **Enable & start** to open the **Start NFS** wizard\. The **Physical network interface** field is populated\. ![\[The Start NFS wizard\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-nfs-console.png) 

1. Choose **Create IP address \(VNI\)** or choose **Use existing IP address**\.

1. If you choose **Create IP address \(VNI\)**, then choose **DHCP** or **Static IP** in the **IP Address assignment** list box\.
**Important**  
If you use a DHCP network, it is possible that the NFS client's IP address could be reassigned by the DCHP server\. This can happen after the device has been disconnected and the IP addresses are recycled\. If you set an allowed host range and the address of the client changes, another client can pick up that address\. In this case, the new client will have access to the share\. To prevent this, use DHCP reservations or static IP addresses\.

   If you choose **Use existing IP address**, then choose a virtual interface from the **Virtual network interface** list box\.

1. **Restrict NFS to allowed hosts** is selected by default\. This restricts access to the NFS service to hosts you allow but you can choose **Allow all hosts**\. We recommend restricting access\. For more information about using NFS, see [Using NFS for Offline Data Transfer](https://docs.aws.amazon.com/snowball/latest/developer-guide/shared-using-nfs.html)\.

1. In the **Allowed hosts** text box, provide the CIDR blocks of hosts that you want to allow to connect to the NFS service\. For example, `10.0.0.0/16`\.

1. Choose **Add allowed host** to add more hosts to allow\.

1. Choose **Start NFS**\. It could take about a minute or two to start\. NFS uses 1 GB of ram and one of your CPUs\. This limits the number of instances available\.
**Important**  
Don't turn off your device while the service is starting\.

1. From the **Network File System \(NFS\) resource** section, the **State** of the NFS service shows as **Active**\. Use the copy icon to copy the IP address of the NFS service\. You will need this IP address for connect your NFS service when are ready to transfer files\.

1. In the **Mount paths** box, you can filter and look for your endpoints\.

1. For **Endpoint name**, choose an endpoint from the list, and choose **Mount NFS endpoint**\. In Linux, mounting and unmount NFS endpoints requires root permissions\. This endpoint is configured with the S3 bucket you specified when you ordered the device\. The endpoint is shown under **NFS endpoints**\. The endpoint is configured as an NFS file and shares\. It appears as a drive letter and you can use your native operating system to drag and drop files onto and out of your device\. 

   The following are the default mount options:
   + Windows: `mount -o nolock rsize=128 wsize=128 mtype=hard ipaddress:/buckets/BucketName *`
   + Linux: `mount -t nfs ipaddress:/buckets/BucketName mount_point`
   + macOS: `mount -t nfs -o vers=3,rsize=131072,wsize=131072,nolocks,hard,retrans=2 ipaddress:/buckets/$bucketname mount_point`

1. Choose the icon next to the drive letter to open the file share in your client's file browser\. Then start transferring files from your client to your Snow Family device\. You can copy and paste, or drag and drop files from your client computer into the file share\. In Windows, your file share looks like the following: `buckets(\\12.123.45.679)(Z:)`

## Stopping data transfer<a name="stop-nfs"></a>



**To stop data transfer**

1. From the dashboard, choose **Services** and then choose **File Storage**\.

1. On the **File Storage** page, choose **Disable data transfer**\. It usually takes up to 2 minutes for the NFS endpoints to disappear from the dashboard\.