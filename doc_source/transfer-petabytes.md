--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# How to Transfer Petabytes of Data Efficiently<a name="transfer-petabytes"></a>

When transferring petabytes of data, we recommend that you plan and calibrate your data transfer between the AWS Snowball Edge appliances you have onsite and your servers according to the following guidelines\.

## Planning Your Large Transfer<a name="copy-general-planning"></a>

To plan your petabyte\-scale data transfer, we recommend the following steps:


+ [Step 1: Understand What You're Moving to the Cloud](#understand-the-transfer)
+ [Step 2: Calculate Your Target Transfer Rate](#calculate-rate)
+ [Step 3: Determine How Many AWS Snowball Edge appliances You Need](#number-of-snowballs)
+ [Step 4: Create Your Jobs](#make-jobs)
+ [Step 5: Separate Your Data into Transfer Segments](#prepare-segments)

### Step 1: Understand What You're Moving to the Cloud<a name="understand-the-transfer"></a>

Before you create your first job using AWS Snowball Edge appliances, you should make sure you know what data you want to transfer, where it is currently stored, and the destination you want to transfer it to\. For data transfers that are a petabyte in scale or larger, this bit of administrative housekeeping will make your life much easier when your AWS Snowball Edge appliances start to arrive\.

You can keep this data in a spreadsheet or on a whiteboard—however it works best for you to organize the large amount of content you'll be moving to the cloud\. If you're migrating data into the cloud for the first time, we recommend that you design a cloud migration model\. For more information, see the whitepaper, [A Practical Guide to Cloud Migration](https://d0.awsstatic.com/whitepapers/the-path-to-the-cloud-dec2015.pdf), on the AWS Whitepapers website\.

When you're done with this step, you'll know the total amount of data that you're going to move into the cloud\.

### Step 2: Calculate Your Target Transfer Rate<a name="calculate-rate"></a>

It's important to estimate how quickly you can transfer data to the AWS Snowball Edge appliances connected to each of your servers\. This estimated speed equals your target transfer rate\. This rate is the rate at which you can expect data to move into an AWS Snowball Edge appliance given the realities of your local network architecture\.

**Note**  
For large data transfers, we recommend using the Amazon S3 Adapter for Snowball to transfer your data\.

To calculate your target transfer rate, transfer a representative subset of your data to a Snowball Edge\. During the transfer, run the `snowballEdge status` command to track the progress of the transfer\. When the transfer is complete, compare the size of the transferred data against the time it took the transfer to complete to get an estimate of your current transfer speed\.

While determining your target transfer speed, keep in mind that you can change the speed through changes to network speed, the size of the files being transferred, and the speed at which data can be read from your local servers\. The Amazon S3 Adapter for Snowball will copy data to the AWS Snowball Edge appliance as fast as conditions allow\.

### Step 3: Determine How Many AWS Snowball Edge appliances You Need<a name="number-of-snowballs"></a>

Using the total amount of data you're going to move into the cloud, found in step 1, the transfer speed you estimated from step 2, and the number of days in which you want to move the data into AWS, determine how many AWS Snowball Edge appliances you'll need to finish your large scale data migration\. Remember that AWS Snowball Edge appliances have about 73 TB of usable space\. So if you want to move 300 TB of data into AWS in 10 days, and you have a transfer speed of 250 MB/s, you would need five AWS Snowball Edge appliances\.

### Step 4: Create Your Jobs<a name="make-jobs"></a>

Now that you know how many AWS Snowball Edge appliances you need, you can create an import job for each appliance\. Because each AWS Snowball Edge appliance import job involves a single AWS Snowball Edge appliance, you'll have to create multiple import jobs\. For more information, see [Create Your First Job](create-job.md)\.

### Step 5: Separate Your Data into Transfer Segments<a name="prepare-segments"></a>

As a best practice for large data transfers involving multiple jobs, we recommend that you separate your data into a number of smaller, manageable data transfer segments\. If you separate the data this way, you can transfer each segment one at a time, or multiple segments in parallel\. When planning your segments, make sure that all the sizes of the data for each segment combined fit on the AWS Snowball Edge appliance for this job\. When segmenting your data transfer, take care not to copy the same files or directories multiple times\. Some examples of separating your transfer into segments are as follows:

+ You can make 9 segments of 10 TB each for an AWS Snowball Edge appliance\.

+ For large files, each file can be an individual segment, keeping in mind the 5 TB size limit for objects in Amazon S3\.

+ Each segment can be a different size, and each individual segment can be made of the same kind of data—for example, small files in one segment, compressed archives in another, large files in another segment, and so on\. This approach helps you determine your average transfer rate for different types of files\.

**Note**  
Metadata operations are performed for each file transferred\. Regardless of a file's size, this overhead remains the same\. Therefore, you'll get faster performance out of compressing small files into a larger bundle, batching your files, or transferring larger individual files\.

Creating these data transfer segments makes it easier for you to quickly resolve any transfer issues, because trying to troubleshoot a large, heterogeneous transfer after the transfer has run for a day or more can be complex\.

When you've finished planning your petabyte\-scale data transfer, we recommend that you transfer a few segments onto the AWS Snowball Edge appliance from your server to calibrate your speed and total transfer time\.

## Calibrating a Large Transfer<a name="calibrating-large-transfer"></a>

You can calibrate a large transfer by transferring a representative set of your data transfer segments\. In other words, choose a number of the data segments that you defined following last section's guidelines and transfer them to an AWS Snowball Edge appliance, while making a record of the transfer speed and total transfer time for each operation\.

While the calibration is being performed, monitor the information that comes from the `snowballEdge status` command\. If the calibration's results are less than the target transfer rate, you might be able to copy multiple parts of your data transfer at the same time\. In this case, repeat the calibration with additional data transfer segment\.

Continue adding additional parallel copy operations during calibration until you see diminishing returns in the sum of the transfer speed of all instances currently transferring data\. At this point, you can end the last active instance and make a note of your new target transfer rate\.

Sometimes the fastest way to transfer data with AWS Snowball Edge appliance is to transfer data in parallel in one of the following scenarios:

+ Using multiple instances of the Amazon S3 Adapter for Snowball on a single AWS Snowball Edge appliance\.

+ Using multiple instances of the Amazon S3 Adapter for Snowball on multiple AWS Snowball Edge appliances\.

When you complete these steps, you should know how quickly you can transfer data to an AWS Snowball Edge appliance\.