# Shipping considerations for Snow Family devices<a name="shipping"></a>

When you create a job, you specify a shipping address and shipping speed\. Note that the shipping speed doesn’t indicate how soon you can expect to receive the AWS Snowball Edge device from the day you created the job\. Rather, it indicates the time that the device is in transit between AWS and your shipping address\. Before the device ships, AWS processes your job\. The amount of time that's required to process your job depends on factors like job type and size\. Also, carriers generally only pick up outgoing Snowball Edge devices once a day and carriers don't pick up outgoing devices on weekends\. Thus, processing before shipping can take a day or more\.

**Note**  
The shipping speed that you choose applies when AWS sends the device to you and when you return the device to AWS\.  
Snowball Edge devices can only be used to import or export data within the AWS Region where the devices are ordered\.

 For information about shipping charges, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\.

## Region\-based shipping restrictions<a name="shipwithinregion"></a>

Before you create a job, you should sign in to the console from the same AWS Region as your Amazon S3 data\. AWS does not ship Snow Family devices between countries within the same AWS Region—for example, from Asia Pacific \(India\) to Asia Pacific \(Australia\)\.

An exception to shipping between countries is among European Union \(EU\) member countries\. For data transfers in the European AWS Regions, we only ship devices to the EU member countries listed:

Austria, Belgium, Bulgaria, Croatia, Republic of Cyprus, Czech Republic, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Italy, Ireland, Latvia, Lithuania, Luxembourg, Malta, Netherlands, Poland, Portugal, Romania, Slovakia, Slovenia, Spain and Sweden\.

Snow Family devices can only be returned to the same AWS Region where the devices were ordered\.

Shipments domestically within the same country are permitted\. Examples:
+ For data transfers in the United Kingdom Region, we ship devices domestically within the UK\.
+ For data transfers in Asia Pacific \(Mumbai\), we ship devices within India\. 

**Note**  
AWS doesn't ship Snow Family devices to post office boxes\.