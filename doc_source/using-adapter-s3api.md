--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Supported REST API Actions for Amazon S3<a name="using-adapter-s3api"></a>

Following, you can find the list of Amazon S3 REST API actions that are supported for using the Amazon S3 Adapter for Snowball, with links to information about how the API actions work with Amazon S3\. The list also covers any differences in behavior between the Amazon S3 API action and the AWS Snowball Edge appliance counterpart\. All responses coming back from an AWS Snowball Edge appliance declare `Server` as `AWSSnowball`, as in the following example\.

```
HTTP/1.1 200 OK
x-amz-id-2: JuKZqmXuiwFeDQxhD7M8KtsKobSzWA1QEjLbTMTagkKdBX2z7Il/jGhDeJ3j6s80
x-amz-request-id: 32FE2CEB32F5EE25
Date: Fri, 08 2016 21:34:56 GMT
Server: AWSSnowball
```

+ [GET Bucket \(List Objects\) Version 1](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGET.html)  – Supported, however the only supported delimiter is a forward slash\. Note that this is for version 1 only\. GET Bucket \(List Objects\) Version 2 is not supported\.

+ [GET Service](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTServiceGET.html) 

+ [HEAD Bucket](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketHEAD.html) 

+ [HEAD Object](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectHEAD.html)  

+ [GET Object](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGET.html) – When an object is uploaded to an AWS Snowball Edge appliance using `GET Object`, an entity tag \(ETag\) is not generated unless the object was uploaded using multipart upload\. The ETag is a hash of the object\. The ETag reflects changes only to the contents of an object, not its metadata\. The ETag might or might not be an MD5 digest of the object data\. For more information on ETags, see [Common Response Headers](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTCommonResponseHeaders.html) in the Amazon Simple Storage Service API Reference\.

+ [PUT Object](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUT.html) – When an object is uploaded to an AWS Snowball Edge appliance using `PUT Object`, an ETag is not generated unless the object was uploaded using multipart upload\.

+ [DELETE Object](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectDELETE.html) 

+ [Initiate Multipart Upload](http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadInitiate.html) – In this implementation, initiating a multipart upload request for an object already on the AWS Snowball Edge appliance first deletes that object and then copies it in parts to the AWS Snowball Edge appliance\. 

+ [List Multipart Uploads](http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadListMPUpload.html)  

+ [Upload Part](http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadUploadPart.html)  

+ [Complete Multipart Upload](http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadComplete.html)  

+ [Abort Multipart Upload](http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadAbort.html)  

**Note**  
Any Amazon S3 REST API actions not listed here are not supported\. Using any unsupported REST API actions with your Snowball Edge will return an error message saying that the action is not supported\.