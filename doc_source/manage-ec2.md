# Using Amazon EC2 compute instances locally<a name="manage-ec2"></a>

You can use AWS OpsHub to run pre\-installed software on virtual servers \(instances\) locally on your device, and also to manage Amazon EC2 instances on your device\. 

**Topics**
+ [Launching an Amazon EC2 instance](#launch-instance)
+ [Stopping an Amazon EC2 instance](#stop-instance)
+ [Starting an Amazon EC2 instance](#start-instance)
+ [Working with key pairs](#working-with-key-pair)
+ [Terminating an Amazon EC2 instance](#terminate-instance)
+ [Using storage volumes locally](#manage-ebs-volumes)
+ [Importing an image into your device as an Amazon EC2 AMI](#ec2-ami-import)
+ [Deleting a snapshot](#delete-snapshot)
+ [Deregistering an AMI](#deregister-ami)

## Launching an Amazon EC2 instance<a name="launch-instance"></a>

Follow these steps to launch an Amazon EC2 instance using AWS OpsHub\.

**To launch an Amazon EC2 instance**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. All your compute resources appear in the **Resources** section\.

1. If you have Amazon EC2 instances running on your device, they appear in the **Instance name** column under **Instances**\. You can see details of each instance on this page\.

1. Choose **Launch instance**\. The launch instance wizard opens\.

1. For **Device**, choose the Snow device that you want to launch the Amazon EC2 instance on\. 

1. For **Image \(AMI\)**, choose an Amazon Machine Image \(AMI\) from the list\. This AMI is used to launch your instance\.

1. For **Instance type**, choose one from the list\.

1. Choose how you want to attach an IP address to the instance\. You have the following options:
   + **Create public IP address \(VNI\)** – Choose this option to create a new IP address using a physical network interface\. Choose a physical network interface and IP address assignment\.
   + **Use existing IP address \(VNI\)** – Choose this option to use an existing IP address and then use existing virtual network interfaces\. Choose a physical network interface and a virtual network interface\.
   + **Do not attach IP address** – Choose this option if you don't want to attach an IP address\. 

1. Choose how you want to attach a key pair to the instance\. You have the following options:

   **Create key pair** – Choose this option to create a new key pair and launch the new instance with this key pair\.

   **Use existing key pair** – Choose this option to use an existing key pair to launch the instance\.

    **Do not attach IP address** – Choose this option if you don't want to attach a key pair\. You must acknowledge that you won't able to connect to this instance unless you already know the password that is built into this AMI\.

   For more information, see [Working with key pairs](#working-with-key-pair)\.

1. Choose **Launch**\. You should see your instance launching in the **Compute instances** section\. The **State** is **Pending** and then changes to **Running** when done\.

## Stopping an Amazon EC2 instance<a name="stop-instance"></a>

Use the following steps to use AWS OpsHub to stop an Amazon EC2 instance\.

**To stop an Amazon EC2 instance**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section of the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. 

   All your compute resources appear in the **Resources** section\.

1. If you have Amazon EC2 instances running on your device, they appear in the **Instance name** column under **Instances**\.

1. Choose the instance that you want to stop, and choose **Stop**\. The **State** changes to **Stopping**, and then to **Stopped** when done\.

## Starting an Amazon EC2 instance<a name="start-instance"></a>

Use these steps to start an Amazon EC2 instance using AWS OpsHub\.

**To start an Amazon EC2 instance**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section of the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. 

   Your compute resources appear in the **Resources** section\.

1. In the **Instance name** column, under **Instances**, find the instance that you want to start\.

1. Choose the instance, and then choose **Start**\. The **State** changes to **Pending**, and then changes to **Running** when done\.

## Working with key pairs<a name="working-with-key-pair"></a>

When you launch an Amazon EC2 instance and intend to connect to it using SSH, you have to provide a key pair\. You can use Amazon EC2 to create a new key pair, or you can import an existing key pair or manage your key pairs\.

**To create, import, or manage key pairs**

1. Open **Compute** on the AWS OpsHub dashboard\.

1. In the navigation pane, choose the **Compute \(EC2\)** page, and then choose the **Key Pairs** tab\. You are redirected to the Amazon EC2 console where you can create, import, or manage your key pairs\.

1. For instructions on how to create and import key pairs, see [Amazon EC2 key pairs and Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#prepare-key-pair) in the *Amazon EC2 User Guide for Linux Instances*\.

## Terminating an Amazon EC2 instance<a name="terminate-instance"></a>

After you terminate an Amazon EC2 instance, you can't restart the instance\.

**To terminate an Amazon EC2 instance**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. You can see all your compute resources in the **Resources** section\.

1. In the **Instance name** column, under **Instances**, find the instance that you want to terminate\.

1. Choose the instance, and choose **Terminate**\. The **State** changes to **Terminating**, and then to **Terminated** when done\. 

   After the instance is terminated, you can't restart it\.

## Using storage volumes locally<a name="manage-ebs-volumes"></a>

Amazon EC2 instances use Amazon EBS volumes for storage\. In this procedure, you create a storage volume and attach it to your instance using AWS OpsHub\.

**To create a storage volume**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. 

1. Choose the **Storage volumes** tab\. If you have storage volumes on your device, the details about the volumes appear under **Storage volumes**\.

1. Choose **Create volume** to open the **Create volume** page\.

1. Choose the device that you want to create the volume on, enter the size \(in GiBs\) that you want to create, and choose the type of volume\.

1. Choose **Submit**\. The **State** is **Creating**, and changes to **Available** when done\. You can see your volume and details about it in the **Volumes** tab\.

**To attach a storage volume to your instance**

1. Choose the volume that you created, and then choose **Attach volume**\.

1. For **Compute instance Id**, choose the instance you want to attach the volume to\.

1. For **Volume Device Name**, enter the device name of your volume \(for example, **/dev/sdh** or **xvdh**\)\.

1. Choose **Attach**\.

If you no longer need the volume, you can detach it from the instance and then delete it\.

## Importing an image into your device as an Amazon EC2 AMI<a name="ec2-ami-import"></a>

You can import a snapshot of your image into your Snowball Edge device and register it as an Amazon EC2 Amazon Machine Image \(AMI\)\. A snapshot is basically a copy of your storage volume that you can use to create an AMI or another storage volume\. By doing this, you can bring your own image from an external source onto your device and launch it as an Amazon EC2 instance\. 

Follow these steps to complete the import of your image\.

1. Upload your snapshot into an Amazon S3 bucket on your device\.

1. Set up the required permissions to grant access to Amazon S3, Amazon EC2, and VM Import/Export, the feature that is used to import and export snapshots\. 

1. Import the snapshot from the S3 bucket into your device as an image\.

1. Register the image as an Amazon EC2 AMI\.

1. Launch the AMI as an Amazon EC2 instance\.

**Note**  
Be aware of the following limitations when uploading snapshots to Snow Family devices\.  
Snow Family devices currently only support importing snapshots that are in the RAW image format\. 
Snow Family devices currently only support importing snapshots with sizes from 1 GB to 1 TB\.

### Step 1: Upload a snapshot into an S3 bucket on your device<a name="upload-snapshot"></a>

You must upload your snapshot to Amazon S3 on your device before you import it\. This is because snapshots can only be imported from Amazon S3 available on your device or cluster\. During the import process, you choose the S3 bucket on your device to store the image in\.

**To upload a snapshot to Amazon S3**
+ To create an S3 bucket, see [Creating Amazon S3 Storage](https://docs.aws.amazon.com/snowball/latest/developer-guide/manage-s3.html#create-s3-storage)\.

  To upload a snapshot to an S3 bucket, see [Uploading Files to Amazon S3 Storage](https://docs.aws.amazon.com/snowball/latest/developer-guide/manage-s3.html#upload-file)\.

### Step 2: Import the snapshot from an S3 bucket<a name="import-snapshot"></a>

When your snapshot is uploaded to Amazon S3, you can import it to your device\. All snapshots that have been imported or are in the process of being imported are shown in **Snapshots** tab\.

**To import the snapshot to your device**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. All your compute resources appear in the **Resources** section\.

1. Choose the **Snapshots** tab to see all the snapshots that have been imported to your device\. The image file in Amazon S3 is a \.raw file that is imported to your device as a snapshot\. You can filter by snapshot ID or the state of the snapshot to find specific snapshots\. You can choose a snapshot ID to see details of that snapshot\.

1. Choose the snapshot that you want to import, and choose **Import snapshot** to open the **Import snapshot** page\.

1. For **Device**, choose the IP address of the Snow Family device that you want to import to\.

1. For **Import description** and **Snapshot description**, enter a description for each\.

1. In the **Role** list, choose a role to use for the import\. Snow Family devices use VM Import/Export to import snapshots\. AWS assumes this role and uses it to import the snapshot on your behalf\. If you don't have a role, open the AWS Identity and Access Management \(IAM\) console, where you can create role\. The role also needs a policy that has the required VM Import/Export permissions to perform the import\. You must attach this policy to the role\. 

   The following is an example of the policy\.

   ```
   {
      "Version":"2012-10-17",
      "Statement":[
         {
            "Effect":"Allow",
            "Principal":{
               "Service":"vmie.amazonaws.com"
            },
            "Action":"sts:AssumeRole"
         }
      ]
   }
   ```

   Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

   The role you create should have minimum permissions to access Amazon S3 The following is example of a minimum policy\. 

   ```
   {
      "Version":"2012-10-17",
      "Statement":[
         {
            "Effect":"Allow",
            "Action":[
               "s3:GetBucketLocation",
               "s3:GetObject",
               "s3:ListBucket",
               "s3:GetMetadata"
            ],
            "Resource":[
               "arn:aws:s3:::import-snapshot-bucket-name",
               "arn:aws:s3:::import-snapshot-bucket-name/*"
            ]
         }
      ]
   }
   ```

1. Choose **Browse S3** and choose the S3 bucket that contains the snapshot that you want to import\. Choose the snapshot, and choose **Submit**\. The snapshot begins to download onto your device\. You can choose the snapshot ID to see the details\. You can cancel the import process from this page\.

### Step 3: Register the snapshot as an Amazon EC2 AMI<a name="register-snapshot"></a>

The process of creating an Amazon EC2 AMI from an image imported as a snapshot is known as *registering*\. Images that are imported to your device must be registered before they can be launched as Amazon EC2 instances\.

**To register an image imported as a snapshot**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. All your compute resources appear in the **Resources** section\.

1. Choose the **Images** tab\. You can filter the images by name, ID, or state to find a specific image\.

1. Choose the image that you want to register, and choose **Register image**\.

1. On the **Register image** page, provide a **Name** and **Description**\.

1. For **Root volume**, specify the name of the root device\.

   In the **Block device** section, you can change the size of the volume and the volume type\.

1. If you want the volume to be deleted when the instance is terminated, choose **Delete on termination**\.

1. If you want to add more volumes, choose **Add new volume**\.

1. When you are done, choose **Submit**\.

### Step 4: Launch the Amazon EC2 AMI<a name="launch-ami"></a>


+ For more information, see [Launching an Amazon EC2 instance](https://docs.aws.amazon.com/snowball/latest/snowcone-guide/manage-ec2.html#launch-instance)\.

## Deleting a snapshot<a name="delete-snapshot"></a>

If you no longer need a snapshot, you can delete it from your device\. The image file in Amazon S3 is a \.raw file that is imported to your device as a snapshot\. If the snapshot that you are deleting is used by an image, it can't be deleted\. After import is completed, you can also delete the \.raw file that you uploaded to Amazon S3 on your device\.

**To delete a snapshot**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. All your compute resources appear in the **Resources** section\.

1. Choose the **Snapshot** tab to see all snapshots that have been imported\. You can filter by snapshot ID or state of the snapshot to find specific snapshots\. 

1. Choose the snapshot that you want to delete, and choose **Delete**\. You can choose multiple snapshots\.

1. In the **Delete snapshot confirmation** box, choose **Delete snapshot**\. If your deletion is successful, the snapshot is removed from the list under the **Snapshots** tab\. 

## Deregistering an AMI<a name="deregister-ami"></a>



**To deregister an AMI**

1. Open the AWS OpsHub application\.

1. In the **Start computing** section on the dashboard, choose **Get started**\. Or, choose the **Services** menu at the top, and then choose **Compute \(EC2\)** to open the **Compute** page\. All your compute resources appear in the **Resources** section\.

1. Choose the **Images** tab\. All your images are listed\. You can filter the images by name, ID, or state to find a specific image\.

1. Choose the image that you want to deregister, and choose **Deregister**\.

1.  In the confirmation dialog box, confirm the image ID and choose **Deregister image**\. When deregistering is successful, the image is removed from the list of images\. 