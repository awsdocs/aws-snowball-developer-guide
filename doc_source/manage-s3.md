# Managing Amazon S3 storage<a name="manage-s3"></a>

You can use AWS OpsHub to create and manage Amazon Simple Storage Service \(Amazon S3\) storage on your Snow Family devices\.

**Topics**
+ [Accessing Amazon S3 Storage](#create-s3-storage)
+ [Uploading files to Amazon S3 storage](#upload-file)
+ [Downloading files from Amazon S3 storage](#download-file)
+ [Deleting files from Amazon S3 storage](#delete-file)

## Accessing Amazon S3 Storage<a name="create-s3-storage"></a>

You can upload files to your device and access the files locally\. You can physically move them to another location on the device, or import them back to the AWS Cloud when the device is returned\. 

Snow Family devices use Amazon S3 buckets to store and manage files on your device\.



**To access an S3 bucket**

1. Open the AWS OpsHub application\.

1. In the **Manage file storage** section of the dashboard, choose **Get started**\. 

   If your device has been ordered with the Amazon S3 transfer mechanism, they appear in the **Buckets** section of the **File & object storage** page\. On the **File & object storage** page, you can see details of each bucket\.
**Note**  
If the device was ordered with the NFS transfer mechanism, the bucket name will appear under the mount points section after NFS service is configure and activated\. For more information on using the file interface, see [Transferring Files to Snowball Edge devices using the File Interface](using-fileinterface.md)\.   
![\[File and object storage page showing Amazon S3 buckets on the Snow Family device\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-access-s3-console.png)

## Uploading files to Amazon S3 storage<a name="upload-file"></a>

This video shows how to upload files to Amazon S3 storage using AWS OpsHub\.

[![AWS Videos](http://img.youtube.com/vi/https://www.youtube.com/embed/Bw8rzQhT1nM?start=472/0.jpg)](http://www.youtube.com/watch?v=https://www.youtube.com/embed/Bw8rzQhT1nM?start=472)

**To upload a file**

1. In the **Manage file storage** section on the dashboard, choose **Get started**\. 

   If you have Amazon S3 buckets on your device, they appear in the **Buckets** section on the **File storage** page\. You can see details of each bucket on the page\.

1. Choose the bucket that you want to upload files into\.

1. Choose **Upload** then **Upload files** or drag and drop the files in the bucket, and choose **OK**\.  
![\[Amazon S3 bucket with Upload files chosen from the Upload menu\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-upload-s3-console.png)
**Note**  
To upload larger files, you can use the multipart upload feature in Amazon S3 using the AWS CLI\. For learning more about configuring S3 CLI settings, see [CLI S3 Configuration](https://docs.aws.amazon.com/cli/latest/topic/s3-config.html)\. For information on multipart upload, see [Multipart Upload Overview](https://docs.aws.amazon.com/AmazonS3/latest/dev/mpuoverview.html) in the \.*Amazon Simple Storage Service User Guide*  
Uploading a folder from a local machine to Snowball Edge using the AWS OpsHub is supported\. If the folder size is very large, it takes some time to read the file/folder selection\. Currently, there is no progress tracker for file reading\. However, a progress tracker is displayed once the upload process kicks off\.

## Downloading files from Amazon S3 storage<a name="download-file"></a>



**To download a file**

1. In the **Manage file storage** section of the dashboard, choose **Get started**\. If you have S3 buckets on your device, they appear in the **Buckets** section on the **File storage** page\. You can see details of each bucket on the page\.

1. Choose the bucket that you want to download files from and navigate to the file that you want to download\. Choose one or more files\.  
![\[File and object storage page showing one file selected and the actions menu open showing Download file option.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-download-file-console.png)

1. In the **Actions** menu, choose **Download**\.

1. Choose a location to download the file to, and choose **OK**\.

## Deleting files from Amazon S3 storage<a name="delete-file"></a>

If you no longer need a file, you can delete it from your Amazon S3 bucket\.

**To delete a file**

1. In the **Manage file storage** section of the dashboard, choose **Get started**\. If you have Amazon S3 buckets on your device, they appear in the **Buckets** section on the **File storage** page\. You can see details of each bucket on the page\.

1. Choose the bucket you want to delete files from, and navigate to the file that you want to delete\.

1. On the **Actions** menu, choose **Delete**\.

1. In the dialog box that appears, choose **Confirm delete**\.