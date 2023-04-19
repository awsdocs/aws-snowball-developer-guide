# Performance<a name="performance"></a>

Following, you can find recommendations and information about AWS Snowball Edge device performance\. This section describes performance in general terms, because on\-premises environments have a different way of doing things—different network technologies, different hardware, different operating systems, different procedures, and so on\.

The following table outlines how your network's transfer rate impacts how long it takes to fill a Snowball Edge device with data\. Transferring smaller files reduces your transfer speed due to increased overhead\. If you have many small files, we recommend that you zip them up into larger archives before transferring them onto a Snowball Edge device\.


| Rate \(MB/s\) | 82 TB transfer time | 
| --- | --- | 
| 800 | 1\.22 days | 
| 450 | 2\.11 days | 
| 400 | 2\.37 days | 
| 300 | 3\.16 days | 
| 277 | 3\.42 days | 
| 200 | 4\.75 days | 
| 100 | 9\.49 days | 
| 60 | 15\.53 days | 
| 30 | 31\.06 days | 
| 10 | 85\.42 days | 

To provide meaningful guidance about performance, the following sections describe how to determine when to use the AWS Snowball Edge device and how to get the most out of the service\.

**Topics**
+ [Performance Recommendations](#perf-recommendations)
+ [Speeding Up Data Transfer](#transferspeed)

## Performance Recommendations<a name="perf-recommendations"></a>

The following practices are highly recommended, because they have the largest impact on improving the performance of your data transfer:
+ We recommend that you have no more than 500,000 files or directories within each directory\.
+ We recommend that all files transferred to a Snowball Edge device be no smaller than 1 MB in size\.
+ If you have many files smaller than 1 MB in size, we recommend that you zip them up into larger archives before transferring them onto a Snowball Edge device\.

## Speeding Up Data Transfer<a name="transferspeed"></a>

**Note**  
If you are using a Snowball Edge with the S3 data transfer mechanism, the data transfer rate using the file interface is typically between 25 MB/s and 40 MB/s\. If you need to transfer data faster than this, use the Amazon S3 interface\. The S3 interface has a data transfer rate typically between 250 MB/s and 400 MB/s\. For more information about using the Amazon S3 interface, see [Transferring Files Using the Amazon S3 Interface](using-adapter.md)  
If you are using a Snowball Edge with the NFS data transfer mechanism, the data transfer rate using the file interface is typically between 250 MB/s and 400 MB/s\. For more information about using the file interface, see [Transferring Files to Snowball Edge devices using the File Interface](using-fileinterface.md)\.

One of the best ways that you can improve the performance of an AWS Snowball Edge device is to speed up the transfer of data going to and from a device\. In general, you can improve the transfer speed from your data source to the device in the following ways\. This following list is ordered from largest to smallest positive impact on performance:

1. **Perform multiple write operations at one time** – To do this, run each command from multiple terminal windows on a computer with a network connection to a single AWS Snowball Edge device\.

1. **Transfer small files in batches ** – Each copy operation has some overhead because of encryption\. To speed up the process, batch files together in a single archive\. When you batch files together, they can be auto\-extracted when they are imported into Amazon S3\. For more information, see [Batching Small Files](batching-small-files.md)\.

1. **Don't perform other operations on files during transfer** – Renaming files during transfer, changing their metadata, or writing data to the files during a copy operation has a negative impact on transfer performance\. We recommend that your files remain in a static state while you transfer them\. 

1. **Reduce local network use** – Your AWS Snowball Edge device communicates across your local network\. So you can improve data transfer speeds by reducing other local network traffic between the AWS Snowball Edge device, the switch it's connected to, and the computer that hosts your data source\.

1. **Eliminate unnecessary hops** – We recommend that you set up your AWS Snowball Edge device, your data source, and the computer running the terminal connection between them so that they're the only machines communicating across a single switch\. Doing so can improve data transfer speeds\.