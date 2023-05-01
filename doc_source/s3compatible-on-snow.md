# Using Amazon S3 compatible storage on Snow Family devices<a name="s3compatible-on-snow"></a>

Amazon S3 compatible storage on Snow Family devices delivers secure object storage with increased resiliency, scale, and an expanded Amazon S3 API feature\-set to rugged, mobile edge, and disconnected environments\. Using Amazon S3 compatible storage on Snow Family devices, you can store data and run highly available applications on Snow Family devices for edge computing\.

You can deploy Amazon S3 compatible storage on Snow Family devices in standalone configuration or in cluster configuration\. In standalone configuration, you can provision S3 capacity on the device and the balance is available as block storage\. In cluster configuration, all data disk capacity is used for S3 storage\. A cluster may consist of a minimum of 3 devices up to a maximum of 16 devices\. Depending on the size of cluster, S3 service is designed to sustain device fault tolerance of 1 or 2 devices\. 

Following is the fault tolerance and storage capacity for a standalone device using Amazon S3 compatible storage on Snow Family devices\. For fault tollerence and storage capacity for clusters, see [this table](ClusterOverview.md#cluster-table)\.


**Amazon S3 compatible storage on Snow Family devices standalone fault tolerance and storage capacity**  

| Fault tolerance | Storage capacity of Snowball Edge Compute Optimized \(with AMD EPYC Gen1\) with up to 52 vCPUs in TB | Storage capacity of Snowball Edge Compute Optimized \(with AMD EPYC Gen2\) with up to 104 vCPU in TB | 
| --- | --- | --- | 
|  Loss of up to 1 disk in device  |  31  |  16\.5  | 

Amazon S3 compatible storage on Snow Family devices specifications:
+ The maximum Snow Family device bucket size is 50 TB\.
+ The maximum number of Snow Family device buckets is 100 per device or per cluster\.
+ The S3 on Snow Family device bucket owner account owns all objects in the bucket\.
+ Only the S3 on Snow Family device bucket owner account can perform operations on the bucket\.
+ Object size limitations are consistent with those in Amazon S3\.
+ All objects stored on S3 on Snow Family devices have SNOW as the storage class\.
+ By default, all objects stored in the SNOW storage class are stored using server\-side encryption with Amazon S3 managed encryption keys \(SSE\-S3\)\. You can also explicitly choose to store objects by using server\-side encryption with customer\-provided encryption keys \(SSE\-C\)\.
+ If there is not enough space to store an object on your Snow Family device, the API returns an insufficient capacity exception \(ICE\)\.

**Topics**
+ [Order Amazon S3 compatible storage on Snow Family devices](s3-edge-snow-order-device.md)
+ [Setting up using the Snowball Edge client CLI](s3-edge-snow-setting-up.md)
+ [Setting up your Snowball Edge device](s3-edge-snow-setup.md)
+ [Working with S3 buckets on a Snowball Edge device](working-s3-snow-buckets.md)
+ [Clustering overview](ClusterOverview.md)