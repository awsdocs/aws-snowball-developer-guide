# Step 1: Choose a job type<a name="plan-job"></a>

The first step in creating a job is to determine the type of job that you need and to start planning it using the AWS Snow Family Management Console\.

**To choose your job type**

1. Sign in to the AWS Management Console, and open the [AWS Snow Family Management Console](https://console.aws.amazon.com/snowfamily/home)\. If this is your first time creating a job in this AWS Region, you will see the **AWS Snow Family** page\. Otherwise you will see the list of existing jobs\.

1. If this is your first job, choose **Order an AWS Snow Family device**\. If you're expecting multiple jobs to migrate over 500 TB of data, choose **Create your large data migration plan greater than 500 TB**\. Otherwise, choose **Create Job** in the left navigation bar\. Choose **Next step** to open the **Plan your job** page\.

1. In the **Job name** section, provide a name for your job in the **Job name** box\.

1. Depending on your use case, choose one of the following job types:
   + **Import into Amazon S3** – Choose this option to have AWS ship an empty Snowball Edge device to you\. You connect the device to your local network and run the Snowball Edge client\. You copy data onto the device using NFS share or the S3 adapter, ship it back to AWS, and your data is uploaded to AWS\.
   + **Export from Amazon S3** – Choose this option to export data from your Amazon S3 bucket to your device\. AWS loads your data on the device and ships it to you\. You connect the device to your local network and run the Snowball Edge client\. You copy data from your device to your servers\. When you are done, ship the device to AWS, and your data is erased from the device\.
   + **Local compute and storage only** – Perform compute and storage workloads on the device without transferring data\. 
   + **Import virtual tapes into AWS Storage Gateway** – AWS ships an empty Snow Family device configured as a Tape Gateway\. You transfer the data to the device in the form of virtual tapes, and ship it back\. AWS ingests the data and displays it as virtual tapes in the AWS Storage Gateway console\. Your data is then erased from the device\.

1. Choose **Next** to continue\.