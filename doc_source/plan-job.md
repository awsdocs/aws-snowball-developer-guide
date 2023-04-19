# Step 1: Plan Your Job<a name="plan-job"></a>

The first step in creating a job is to determine the type of job that you need and to start planning it using the AWS Snow Family Management Console\.

**To plan your job**

1. Sign in to the AWS Management Console, and open the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. If this is your first time creating a job in this AWS Region, you will see the **AWS Snow Family** page\. Otherwise you will see the list of pre\-existing jobs\.

1.  If this is your first job, choose **Order an AWS Snow family device** otherwise choose **Create Job** located in the left navigation bar\. Choose **Next step** to open the **Plan your job** page\.

1. Depending on your use case, choose one of the following job types:
   + **Import into Amazon S3** – Choose this option to have ship an empty Snowball Edge device to you\. You connect the device to your local network and run the Snowball Edge client\. You copy data onto the device using NFS share, ship it back to AWS, and your data is uploaded to AWS\.
   + **Export from Amazon S3** – Choose this option to export data from your Amazon S3 bucket to your device\. AWS loads your data on the device and ships it to you\. You connect the device to your local network and run the Snowball Edge client\. You copy data from your device to your servers\. When you are done, ship the device to AWS, and your data is erased from the device\.
   + **Local compute and storage only** – Choose this option to perform compute and storage workloads on the device without transferring any data\. 

1. To increase storage capacity and durability, you can order multiple devices in a cluster\.

   If you choose **Local compute and storage only**, and if you want to create a cluster, enter a name for the cluster and the number of devices that you want in the cluster\. The number of devices must be between 5 and 10 in the **Make this a cluster \- optional** section\. For more information about clusters, see [Using a Snowball Edge Cluster](https://docs.aws.amazon.com/snowball/latest/developer-guide/UsingCluster.html)\.

1. Choose **Next** to continue\.