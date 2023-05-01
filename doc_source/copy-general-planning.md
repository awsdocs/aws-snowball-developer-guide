# Planning Your Large Transfer<a name="copy-general-planning"></a>

We recommend that you plan and calibrate large data transfers between the AWS Snowball Edge devices that you have on site and your servers using the guidelines in the following sections\.

**Topics**
+ [Step 1: Understand What You're Moving to the Cloud](#understand-the-transfer)
+ [Step 2: Calculate Your Target Transfer Rate](#calculate-rate)
+ [Step 3: Determine How Many AWS Snowball Edge Devices You Need](#number-of-snowballs)
+ [Step 4: Create Your Jobs](#make-jobs)
+ [Step 5: Separate Your Data into Transfer Segments](#prepare-segments)

## Step 1: Understand What You're Moving to the Cloud<a name="understand-the-transfer"></a>

Before you create your first job using an AWS Snowball Edge device, ensure that you know the size of the data that you want to transfer, where it is currently stored, and the destination that you want to transfer it to\. For data transfers that are a petabyte in scale or larger, this administrative housekeeping makes it much easier when your AWS Snowball Edge devices arrive\.

If you're migrating data into the AWS Cloud for the first time, we recommend that you design a cloud migration model\. Cloud migration doesn’t happen overnight\. It requires a careful planning process to ensure that all systems work as expected\.

When you're done with this step, you should know the total amount of data that you're going to move into the cloud\.

## Step 2: Calculate Your Target Transfer Rate<a name="calculate-rate"></a>

It's important to estimate how quickly you can transfer data to the Snowball Edge devices that are connected to each of your servers\. This estimated speed equals your target transfer rate\. This rate is the rate at which you can expect data to move into an AWS Snowball Edge device given the realities of your local network architecture\.

**Note**  
For large data transfers, we recommend using the Amazon S3 adapter to transfer your data\.

Capture a baseline transfer rate by calculating the transfer of a representative subset of your data to the Snowball Edge device, or by creating a 10 GB sample file to measure the throughput\.

While determining your target transfer speed, keep in mind that you can change the speed by changing the network speed, the size of the files being transferred, and the speed at which data can be read from your local servers\. The Amazon S3 adapter copies data to the AWS Snowball Edge device as quickly as your conditions allow\.

## Step 3: Determine How Many AWS Snowball Edge Devices You Need<a name="number-of-snowballs"></a>

Using the total amount of data that you plan to move into the cloud, the estimated transfer speed, and the number of days that you want to allow to move the data into AWS, determine how many Snowball Edge devices you need for your large\-scale data migration\. Depending on the device type, Snowball Edge devices have approximately 39\.5 TB or 80 TB of usable space\. For example, if you want to move 300 TB of data to AWS over 10 days and you have a transfer speed of 250 MB/s, you need four Snowball Edge devices\.

## Step 4: Create Your Jobs<a name="make-jobs"></a>

After you know how many AWS Snowball Edge devices you need, you can create an import job for each device\. Because each AWS Snowball Edge device import job involves a single Snowball Edge device, you must create multiple import jobs\. For more information, see [Creating an AWS Snowball Edge Job](https://docs.aws.amazon.com/snowball/latest/developer-guide/create-job-common.html)\.

## Step 5: Separate Your Data into Transfer Segments<a name="prepare-segments"></a>

As a best practice for large data transfers involving multiple jobs, we recommend that you separate your data into a number of smaller, more manageable data transfer segments\. This allows you to transfer segments one at a time, or multiple segments in parallel\. When planning your segments, make sure that the data for the segments combined fit on the AWS Snowball Edge device for the job\. For example, you can separate your transfer into segments in any of the following ways:
+ You can create 10 segments of 8 TB each for an AWS Snowball Edge device\.
+ For large files, each file can be an individual segment up to the 5 TB size limit for objects in Amazon S3\.
+ Each segment can be a different size, and each individual segment can be made up of the same kind of data—for example, small files in one segment, compressed archives in another, large files in another segment, and so on\. This approach can help you to determine your average transfer rate for different types of files\.

**Note**  
Metadata operations are performed for each file that's transferred\. Regardless of a file's size, this overhead remains the same\. Therefore, you get faster performance by compressing small files into a larger bundle, batching your files, or transferring larger individual files\.

Creating data transfer segments can make it easier for you to quickly resolve transfer issues because trying to troubleshoot a large, heterogeneous transfer after the transfer runs for a day or more can be complex\.

When you've finished planning your petabyte\-scale data transfer, we recommend that you transfer a few segments onto the AWS Snowball Edge device from your server to calibrate your speed and total transfer time\.