# Working with S3 buckets on a Snowball Edge device<a name="working-s3-snow-buckets"></a>

You can create Amazon S3 buckets on your Snowball Edge devices to store and retrieve objects on premises for applications that require local data access, local data processing, and data residency\. Amazon S3 compatible storage on Snow Family devices provides a new storage class, `SNOW`, which uses the Amazon S3 APIs, and is designed to store data durably and redundantly across multiple Snowball Edge devices\. You can use the same APIs and features on Snowball Edge buckets that you do on Amazon S3, including bucket lifecycle policies, encryption, and tagging\.

## Using the AWS CLI<a name="working-s3-snow-buckets-cli-setup"></a>

**Note**  
You must use the latest AWS CLI to work with Amazon S3 compatible storage on Snow Family devices\. Install or upgrade to the latest version\. For more information, see [Installing, updating, and uninstalling the AWS CLI](https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-install.html)\.

Follow these instructions to work with Amazon S3 buckets on your device using the AWS CLI\.

**To set up the AWS CLI**

1. Create a profile for object endpoints in `~/.aws/config`\.

   ```
   [profile your-profile]
   aws_access_key_id = your-access-id
   aws_secret_access_key = your-access-key
   region = snow
   ca_bundle = dev/apps/ca-certs/your-ca_bundle
   ```

1. Obtain a certificate from your device\. For information, see the *[Snowball Edge Developer Guide](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#snowball-edge-certificates-cli)*\.

1. If you installed the SDK in a virtual environment, activate it using the following command:

   ```
   source your-virtual-environment-name/bin/activate
   ```

After you set up your operations, you can access them using API calls with the AWS CLI\. In the following examples, `cert` is the device certificate you just obtained using IAM\.

**Accessing object operations**  
`aws s3api --profile your-profile list-objects-v2 --endpoint s3api-endpoint-ip`

**Accessing bucket operations**  
`aws s3control --profile your-profile list-regional-buckets --account-id bucket-owner --endpoint s3ctrlapi-endpoint-ip`

## Using the Java SDK<a name="working-s3-snow-buckets-python-setup"></a>

Use the following example to work with Amazon S3 objects using the Java SDK\.

```
import software.amazon.awssdk.services.s3.S3Client;
import software.amazon.awssdk.auth.credentials.AwsBasicCredentials;
import software.amazon.awssdk.auth.credentials.StaticCredentialsProvider;
import software.amazon.awssdk.http.SdkHttpClient;
import software.amazon.awssdk.http.apache.ApacheHttpClient;
import software.amazon.awssdk.regions.Region;

import java.net.URI;

AwsBasicCredentials creds = AwsBasicCredentials.create(accessKey, secretKey); // set creds by getting Access Key and Secret Key from snowball edge
SdkHttpClient httpClient = ApacheHttpClient.builder().tlsTrustManagersProvider(trustManagersProvider).build(); // set trust managers provider with client certificate from snowball edge
String s3SnowEndpoint = "10.0.0.0"; // set s3-snow object api endpoint from describe service

S3Client s3Client = S3Client.builder().httpClient(httpClient).region(Region.of("snow")).endpointOverride(new URI(s3SnowEndpoint)).credentialsProvider(StaticCredentialsProvider.create(creds)).build();
```

## Bucket ARN format<a name="working-s3-snow-buckets-format"></a>

You can use the Amazon Resource Name \(ARN\) format listed here to identify an Amazon S3 bucket on a Snowball Edge device:

```
arn:partition:s3:snow:account-id:device/device-id/bucket/bucket-name
```

Where *partition* is the Region where you ordered your Snowball Edge device\. *device\-id* is the job\_id if the device is a standalone Snowball Edge device, or the *cluster\_id* if you have a Snowball Edge cluster\.

## Creating an S3 bucket on a Snowball Edge device<a name="creating-s3-snow-bucket"></a>

You can create Amazon S3 buckets on your Snowball Edge device to store and retrieve objects at the edge for applications that require local data access, local data processing, and data residency\. Amazon S3 compatible storage on Snow Family devices provides a new storage class, `SNOW`, which uses Amazon S3 and is designed to store data durably and redundantly across multiple devices \. You can use the same APIs and features as you do on Amazon S3 buckets, including bucket lifecycle policies, encryption, and tagging\.

The following example creates an Amazon S3 bucket for a Snowball Edge device using the AWS CLI\. To run this command, replace the user input placeholders with your own information\.

```
aws s3control --profile your-profile create-bucket --bucket your-snow-bucket
```

## Creating and managing an object lifecycle configuration using the AWS CLI<a name="lifecycle-s3-snow"></a>

You can use Amazon S3 Lifecycle to optimize storage capacity for Amazon S3 compatible storage on Snow Family devices\. You can create lifecycle rules to expire objects as they age or are replaced by newer versions\. You can create, enable, disable, or delete a lifecycle rule\. For more information about Amazon S3 Lifecycle, see [Managing your storage lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)\.

**Note**  
The AWS account that creates the bucket owns it and is the only one that can create, enable, disable, or delete a lifecycle rule\.

To create and manage a lifecycle configuration for an Amazon S3 compatible storage on Snow Family devices bucket using the AWS Command Line Interface \(AWS CLI\), see the following examples\.

### PUT a lifecycle configuration on a Snowball Edge bucket<a name="put-s3-snow-example"></a>

The following AWS CLI example puts a lifecycle configuration policy on a Snowball Edge bucket\. This policy specifies that all objects that have the flagged prefix \(*myprefix*\) and tags expire after 10 days\. To use this example, replace each user input placeholder with your own information\. 

First, save the lifecycle configuration policy to a JSON file\. For this example, the file is named **lifecycle\-example\.json**\.

```
{
    "Rules": [{
        "ID": "id-1",
        "Filter": {
            "And": {
                "Prefix": "myprefix",
                "Tags": [{
                        "Value": "mytagvalue1",
                        "Key": "mytagkey1"
                    },
                    {
                        "Value": "mytagvalue2",
                        "Key": "mytagkey2"
                    }
                ],
            }
        },
        "Status": "Enabled",
        "Expiration": {
            "Days": 10
        }
    }]
}
```

After you save the file, submit the JSON file as part of the `put-bucket-lifecycle-configuration` command\. To use this command, replace each user input placeholder with your own information\.

```
aws s3control put-bucket-lifecycle-configuration --bucket 
                example-snow-bucket --profile your-profile 
                --lifecycle-configuration file://lifecycle-example.json --endpoint s3ctrlapi-endpoint-ip
```

For more information about this command, see [put\-bucket\-lifecycle\-configuration](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/put-bucket-lifecycle-configuration.html) in the *AWS CLI Command Reference*\. 

## Working with Amazon S3 compatible storage on Snow Family devices buckets<a name="buckets-s3-snow"></a>

With Amazon S3 compatible storage on Snow Family devices, you can create Amazon S3 buckets on your Snowball Edge devices to store and retrieve objects on premises for applications that require local data access, local data processing, and data residency\. Amazon S3 compatible storage on Snow Family devices provides a new storage class, `SNOW`, which uses the Amazon S3 APIs, and is designed to store data durably and redundantly across multiple Snowball Edge devices\. You can use the same APIs and features on Snowball Edge buckets that you do on Amazon S3, including bucket lifecycle policies, encryption, and tagging\. You can use Amazon S3 compatible storage on Snow Family devices using the AWS Command Line Interface \(AWS CLI\) or AWS SDKs\.

**Determine whether you can access an Amazon S3 compatible storage on Snow Family devices bucket**

The following example uses the `head-bucket` command to determine if an Amazon S3 bucket exists and you have permissions to access it using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3api head-bucket --bucket sample-bucket --profile your-profile --endpoint-url s3api-endpoint-ip
```

 **Retrieve a list of buckets** 

The following example lists Amazon S3 compatible storage on Snow Family devices buckets using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3control list-regional-buckets --account-id 123456789012 --profile your-profile --endpoint s3ctrlapi-endpoint-ip
```

For more information about this command, see [list\-regional\-buckets](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/list-regional-buckets.html) in the *AWS CLI Command Reference*\.

The following SDK for Java example gets a list of buckets on Snowball Edge devices\. For more information, see [ListRegionalBuckets](https://docs.aws.amazon.com/AmazonS3/latest/API/API_control_ListRegionalBuckets.html) in the [Amazon Simple Storage Service API Reference](https://docs.aws.amazon.com/AmazonS3/latest/API/)\.

```
import com.amazonaws.services.s3control.model.*;

public void listRegionalBuckets() {

    ListRegionalBucketsRequest reqListBuckets = new ListRegionalBucketsRequest()
            .withAccountId(AccountId)

    ListRegionalBucketsResult respListBuckets = s3ControlClient.listRegionalBuckets(reqListBuckets);
    System.out.printf("ListRegionalBuckets Response: %s%n", respListBuckets.toString());

}
```

 **Get a bucket** 

The following example gets an Amazon S3 compatible storage on Snow Family devices bucket using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3control get-bucket --account-id 123456789012 --bucket DOC-EXAMPLE-BUCKET --profile your-profile --endpoint s3ctrlapi-endpoint-ip
```

For more information about this command, see [get\-bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/get-bucket.html) in the *AWS CLI Command Reference*\.

The following Amazon S3 compatible storage on Snow Family devices example gets a bucket using the SDK for Java\. For more information, see [GetBucket](https://docs.aws.amazon.com/AmazonS3/latest/API/API_control_GetBucket.html) in the [Amazon Simple Storage Service API Reference](https://docs.aws.amazon.com/AmazonS3/latest/API/)\.

```
import com.amazonaws.services.s3control.model.*;

public void getBucket(String bucketName) {

    GetBucketRequest reqGetBucket = new GetBucketRequest()
            .withBucket(bucketName)
            .withAccountId(AccountId);

    GetBucketResult respGetBucket = s3ControlClient.getBucket(reqGetBucket);
    System.out.printf("GetBucket Response: %s%n", respGetBucket.toString());
}
```

 **Delete a bucket** 

**Important**  
The AWS account that creates the bucket owns it and is the only one that can delete it\.
Snow Family devices buckets must be empty before they can be deleted\. 
 You cannot recover a bucket after it has been deleted\.

The following example deletes an Amazon S3 compatible storage on Snow Family devices bucket using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3control delete-bucket --account-id 123456789012 --bucket DOC-EXAMPLE-BUCKET --profile your-profile --endpoint s3ctrlapi-endpoint-ip
```

For more information about this command, see [delete\-bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/delete-bucket.html) in the *AWS CLI Command Reference*\.

## Working with Amazon S3 compatible storage on Snow Family devices objects<a name="objects-s3-snow"></a>

This section describes various operations you can perform with objects on Amazon S3 compatible storage on Snow Family devices devices\.

**Copy an object to an Amazon S3 compatible storage on Snow Family devices bucket**

The following example uploads a file named *sample\-object\.xml* to an Amazon S3 compatible storage on Snow Family devices bucket that you have write permissions for using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3api get-object --bucket sample-bucket --key sample-object.xml --profile your-profile --endpoint-url s3api-endpoint-ip
```

The following Amazon S3 compatible storage on Snow Family devices example copies an object into a new object in the same bucket using the SDK for Java\. To use this command, replace each user input placeholder with your own information\.

```
import com.amazonaws.AmazonServiceException;
import com.amazonaws.SdkClientException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.CopyObjectRequest;
add : import java.io.IOException;

public class CopyObject {
    public static void main(String[] args) {
        String bucketName = "*** Bucket name ***";
        String sourceKey = "*** Source object key ***";
        String destinationKey = "*** Destination object key ***";

        try {
            // This code expects that you have AWS credentials set up per:
            // https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html
            AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
                    .enableUseArnRegion()
                    .build();

            // Copy the object into a new object in the same bucket.
            CopyObjectRequest copyObjectRequest = new CopyObjectRequest(sourceKey, destinationKey);
            s3Client.copyObject(copyObjectRequest);
            CopyObjectRequest copyObjectRequest = CopyObjectRequest.builder()
                    .sourceKey(sourceKey)
                    .destinationKey(destKey)
                    .build();
        } catch (AmazonServiceException e) {
            // The call was transmitted successfully, but Amazon S3 couldn't process
            // it, so it returned an error response.
            e.printStackTrace();
        } catch (SdkClientException e) {
            // Amazon S3 couldn't be contacted for a response, or the client
            // couldn't parse the response from Amazon S3.
            e.printStackTrace();
        }
    }
}
```

 **Get an object from a bucket** 

The following example gets an object named *sample\-object\.xml* from an Amazon S3 compatible storage on Snow Family devices bucket using the AWS CLI\. The SDK command is `s3-snow:GetObject`\. To use this command, replace each user input placeholder with your own information\.

```
aws s3api get-object --bucket sample-bucket --key sample-object.xml --profile your-profile --endpoint-url s3api-endpoint-ip
```

For more information about this command, see [get\-object](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/get-object.html) in the *AWS CLI Command Reference*\.

The following Amazon S3 compatible storage on Snow Family devices example gets an object using the SDK for Java\. To use this command, replace each user input placeholder with your own information\. For more information, see [GetObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetObject.html) in the [Amazon Simple Storage Service API Reference](https://docs.aws.amazon.com/AmazonS3/latest/API/)\.

```
import com.amazonaws.AmazonServiceException;
import com.amazonaws.SdkClientException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.GetObjectRequest;
import com.amazonaws.services.s3.model.ResponseHeaderOverrides;
import com.amazonaws.services.s3.model.S3Object;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

public class GetObject {
    public static void main(String[] args) throws IOException {
        String bucketName = "*** Bucket name ***";
        String key = "*** Object key ***";

        S3Object fullObject = null, objectPortion = null, headerOverrideObject = null;
        try {
            // This code expects that you have AWS credentials set up per:
            // https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html
            AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
                    .enableUseArnRegion()
                    .build();
            GetObjectRequest getObjectRequest = GetObjectRequest.builder()
                    .bucket(bucketName)
                    .key(key)
                    .build());

s3Client.getObject(getObjectRequest);
        } catch (AmazonServiceException e) {
            // The call was transmitted successfully, but Amazon S3 couldn't process
            // it, so it returned an error response.
            e.printStackTrace();
        } catch (SdkClientException e) {
            // Amazon S3 couldn't be contacted for a response, or the client
            // couldn't parse the response from Amazon S3.
            e.printStackTrace();
        } finally {
            // To ensure that the network connection doesn't remain open, close any open input streams.
            if (fullObject != null) {
                fullObject.close();
            }
            if (objectPortion != null) {
                objectPortion.close();
            }
            if (headerOverrideObject != null) {
                headerOverrideObject.close();
            }
        }
    }

    private static void displayTextInputStream(InputStream input) throws IOException {
        // Read the text input stream one line at a time and display each line.
        BufferedReader reader = new BufferedReader(new InputStreamReader(input));
        String line = null;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        System.out.println();
    }
}
```

 **List objects in a bucket** 

The following example lists objects in an Amazon S3 compatible storage on Snow Family devices bucket using the AWS CLI\. The SDK command is `s3-snow:ListObjectsV2`\. To use this command, replace each user input placeholder with your own information\.

```
aws s3api list-objects-v2 --bucket sample-bucket --profile your-profile --endpoint-url s3api-endpoint-ip
```

For more information about this command, see [list\-objects\-v2](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/list-objects-v2.html) in the *AWS CLI Command Reference*\.

The following Amazon S3 compatible storage on Snow Family devices example lists objects in a bucket using the SDK for Java\. To use this command, replace each user input placeholder with your own information\.

This example uses [ListObjectsV2](https://docs.aws.amazon.com/AmazonS3/latest/API/API_ListObjectsV2.html), which is the latest revision of the ListObjects API operation\. We recommend that you use this revised API operation for application development\. For backward compatibility, Amazon S3 continues to support the prior version of this API operation\.

```
import com.amazonaws.AmazonServiceException;
import com.amazonaws.SdkClientException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.ListObjectsV2Request;
import com.amazonaws.services.s3.model.ListObjectsV2Result;
import com.amazonaws.services.s3.model.S3ObjectSummary;

public class ListObjectsV2 {

    public static void main(String[] args) {
        String bucketName = "*** Bucket name ***";

        try {
            // This code expects that you have AWS credentials set up per:
            // https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html
            AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
                    .enableUseArnRegion()
                    .build();

            System.out.println("Listing objects");

            // maxKeys is set to 2 to demonstrate the use of
            // ListObjectsV2Result.getNextContinuationToken()
            ListObjectsV2Request req = new ListObjectsV2Request().withBucketName(bucketName).withMaxKeys(2);
            ListObjectsV2Result result;

            do {
                result = s3Client.listObjectsV2(req);

                for (S3ObjectSummary objectSummary : result.getObjectSummaries()) {
                    System.out.printf(" - %s (size: %d)\n", objectSummary.getKey(), objectSummary.getSize());
                }
                // If there are more than maxKeys keys in the bucket, get a continuation token
                // and list the next objects.
                String token = result.getNextContinuationToken();
                System.out.println("Next Continuation Token: " + token);
                req.setContinuationToken(token);
            } while (result.isTruncated());
        } catch (AmazonServiceException e) {
            // The call was transmitted successfully, but Amazon S3 couldn't process
            // it, so it returned an error response.
            e.printStackTrace();
        } catch (SdkClientException e) {
            // Amazon S3 couldn't be contacted for a response, or the client
            // couldn't parse the response from Amazon S3.
            e.printStackTrace();
        }
    }
}
```

 **Delete objects in a bucket** 

You can delete one or more objects from an Amazon S3 compatible storage on Snow Family devices bucket\. The following example deletes an object named *sample\-object\.xml* using the AWS CLI\. To use this command, replace each user input placeholder with your own information\.

```
aws s3api delete-object --bucket sample-bucket --key key --profile your-profile --endpoint-url s3api-endpoint-ip
```

For more information about this command, see [delete\-object](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/delete-object.html) in the *AWS CLI Command Reference*\.

The following Amazon S3 compatible storage on Snow Family devices example deletes an object in a bucket using the SDK for Java\. To use this example, specify the key name for the object that you want to delete\. For more information, see [DeleteObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_DeleteObject.html) in the Amazon Simple Storage Service API Reference\.

```
import com.amazonaws.AmazonServiceException;
import com.amazonaws.SdkClientException;
import com.amazonaws.services.s3.AmazonS3;
import com.amazonaws.services.s3.AmazonS3ClientBuilder;
import com.amazonaws.services.s3.model.DeleteObjectRequest;

public class DeleteObject {
    public static void main(String[] args) {
        String bucketName = "*** Bucket name ***";
        String keyName = "*** key name ****";

        try {
            // This code expects that you have AWS credentials set up per:
            // https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html
            AmazonS3 s3Client = AmazonS3ClientBuilder.standard()
                    .enableUseArnRegion()
                    .build();

            DeleteObjectRequest deleteObjectRequest = DeleteObjectRequest.builder()
                    .bucket(bucketName)
                    .key(keyName)
                    .build()));
            s3Client.deleteObject(deleteObjectRequest);
        } catch (AmazonServiceException e) {
            // The call was transmitted successfully, but Amazon S3 couldn't process
            // it, so it returned an error response.
            e.printStackTrace();
        } catch (SdkClientException e) {
            // Amazon S3 couldn't be contacted for a response, or the client
            // couldn't parse the response from Amazon S3.
            e.printStackTrace();
        }
    }
}
```

## Configuring Amazon S3 compatible storage on Snow Family devices event notifications<a name="s3-snow-event-notifications"></a>

Amazon S3 compatible storage on Snow Family devices supports Amazon S3 event notifications for object API calls based on the MQTT protocol\.

You can use Amazon S3 compatible storage on Snow Family devices to receive notifications when certain events happen in your S3 bucket\. To enable notifications, add a notification configuration that identifies the events that you want the service to publish\.

Amazon S3 compatible storage on Snow Family devices supports the following notification types:
+ New object created events
+ Object removal events
+ Object tagging events

**Configure Amazon S3 event notifications**

1. Before you begin, you must have MQTT infrastructure in your network\.

1. In your Snowball Edge client, run the `snowballEdge configure` command to set up the Snowball Edge device\.

   When prompted, enter the following information:
   + The path to your manifest file\.
   + The device's unlock code\.
   + The device's endpoint \(for example, **https://10\.0\.0\.1**\)\.

1. Run the following `put-notification-configuration` command to send notifications to an external broker\.

   ```
   snowballEdge put-notification-configuration --broker-endpoint ssl://mqtt-broker-ip-address:8883 --enabled true --service-id s3-snow --ca-certificate file:path-to-mqtt-broker-ca-cert
   ```

1. Run the following `get-notification-configuration` command to verify that everything is set up correctly:

   ```
   snowballEdge get-notification-configuration --service-id s3-snow
   ```

   This returns the broker endpoint and enabled field\.

After you configure the entire cluster to send notifications to the MQTT broker in the network, every object API call will result in an event notification\.

**Note**  
You need to subscribe to the topic s3SnowEvents/*Device ID* \(or *Cluster Id* if it is a cluster\)/bucketName\. You can also use wildcards, for example topic name can be *\#* or *s3SnowEvents/\#*\.

The following is an example Amazon S3 compatible storage on Snow Family devices event log:

```
{
  "eventDetails": {
    "additionalEventData": {
      "AuthenticationMethod": "AuthHeader",
      "CipherSuite": "ECDHE-RSA-AES128-GCM-SHA256",
      "SignatureVersion": "SigV4",
      "bytesTransferredIn": 3,
      "bytesTransferredOut": 0,
      "x-amz-id-2": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
    },
    "eventName": "PutObject",
    "eventTime": "2022-10-04T20:24:57.645Z",
    "requestAuthLatencyMillis": 12,
    "requestID": "1234567890abcdef0",
    "requestLatencyMillis": 215,
    "requestLockLatencyNanos": 2325270,
    "requestParameters": {
      "Content-Length": "3",
      "Content-MD5": "dk76iD3aHhHbR2ccSju9ng==",
      "Host": "10.0.2.114",
      "bucketName": "bucketa",
      "key": "hi"
    },
    "requestTTFBLatencyMillis": 215,
    "responseElements": {
      "ETag": "\"764efa883dda1e11db47671c4a3bbd9e\"",
      "Server": "AmazonS3",
      "x-amz-id-2": "1JeMSMd3ai6K4NHAcEeh9kHpy7t2WVrsw2dY2125DoRfIrKHpHVqlg==",
      "x-amz-request-id": "1234567890abcdef0"
    },
    "responseStatusCode": 200,
    "sourceIPAddress": "172.31.37.21",
    "userAgent": "aws-cli/1.16.14 Python/2.7.18 Linux/4.14.291-218.527.amzn2.x86_64 botocore/1.12.4",
    "userIdentity": "{\n  \"identityType\" : \"IAMUser\",\n  \"principalId\" : \"444455556666\",\n  \"arn\" : \"arn:aws:iam::444455556666:root\",\n  \"accountId\" : null,\n  \"accessKeyId\" : null,\n  \"userName\" : \"root\",\n  \"identityProvider\" : null,\n  \"sessionContext\" : null,\n  \"invokedByService\" : null\n}"
  },
```

For more information about Amazon S3 event notifications, see [Amazon S3 Event Notifications](AmazonS3/latest/userguide/NotificationHowTo.html)\.

## Configuring local SMTP notifications<a name="s3-snow-smtp-notifications"></a>

You can set up local notifications for your Snowball Edge devices with Simple Mail Transfer Protocol \(SMTP\)\. The local notifications send emails to configured servers when the service state \(Active, Degraded, Inactive\) changes, or if you cross capacity utilization thresholds of 80%, 90%, or 100%\.

### Prerequisites<a name="s3-snow-smtp-notifications-prerequisites"></a>

Before you begin, confirm that:
+ You have access to the latest Snowball Edge client\.
+ Your device is unlocked and ready to use\.
+ Your device can connect to the internet \(if using Amazon Simple Email Service or external SMTP server\) or to a local SMTP server\.

### Configuring the device<a name="s3-snow-smtp-notifications-configure"></a>

Set up your device to send you email notifications\.

**To configure the device for SMTP notifications**

1. Run the following command to add an SMTP configuration to your device:

   ```
   # If you don't specify a port, port 587 is the default.
   SMTP_ENDPOINT=your-local-smtp-server-endpoint:port
   
   # For multiple email recepients, separate with commas
   RECIPIENTS_LIST=your-email-address
   
   snowballEdge put-notification-configuration \
     --service-id local-monitoring \
     --enabled true \
     --type smtp \
     --broker-endpoint "$SMTP_ENDPOINT" \
     --sender example-sender@domain.com \
     --recipients "$RECIPIENTS_LIST"
   ```

   You receive a test email from **example\-sender@domain\.com** if you're successful\.

1. Test the configuration by running the following `get-notification-configuration` command:

   ```
   snowballEdge get-notification-configuration \
     --service-id local-monitoring
   ```

   The response doesn't include a password or certificate, even if you provide them\.

## Set up remote monitoring<a name="s3-edge-snow-remote-monitoring"></a>

Remote monitoring allows AWS to monitor Amazon S3 compatible storage on Snow Family devices that are connected to an AWS Region\. Enabling this feature triggers periodic service log uploads to the AWS Region and allows AWS to proactively notify customers when we detect issues with the service\.

**Note**  
Remote monitoring only enables monitoring for Amazon S3 compatible storage on Snow Family devicesat this time\.

You can enable remote monitoring by using the `set-features` command in the Snowball Edge CLI\. When the feature is enabled, you can start and stop the feature by toggling the state between INSTALLED\_AUTOSTART and INSTALLED\_ONLY states, respectively\. Use the same command to start remote monitoring\. 

The `describe-features` command shows the status of remote monitoring on Snow Family devices\.

```
./snowballEdge describe-features 
  --manifest-file ./manifest.bin
  --unlock-code unlock-code 
  --endpoint https://device-local-ip
```

Devices that have remote management return the following:

```
{
    "RemoteManagementState" : INSTALLED_ONLY
}
```

Activate remote monitoring by changing the state to auto\-start\.

```
snowballEdge set-features
  --remote-monitoring-state INSTALLED_AUTOSTART
  --manifest-file ./manifest.bin
  --unlock-code unlock-code
  --endpoint https://device-local-ip
```

After you change the state, you receive the following output:

```
{
    "RemoteMonitoringState" : "INSTALLED_AUTOSTART"
}
```

After remote monitoring is enabled you receive the following output\.

```
{
    "RemoteManagementState" : INSTALLED_ONLY,
    "RemoteMonitoringState" : INSTALLED_AUTOSTART
}
```

If remote monitoring isn't available on the device or isn't enabled, there's no change in the output of `describe-features` command\. It only returns the status of remote management\.

**Note**  
The behavior of the device when remote monitoring is stopped is similar to that of an incompatible device—it will not attempt to publish internal device or service telemetry to the cloud\. An incompatible device is one that's not allow\-listed \(the configuration isn't published\), or one that's running an older version of the software that doesn't support remote monitoring\.

```
{
    "RemoteManagementState" : INSTALLED_ONLY
}
```

You can stop remote monitoring by setting the state to `INSTALLED_ONLY`\.

```
snowballEdge set-features
  --remote-monitoring-state INSTALLED_ONLY
  --manifest-file ./manifest.bin
  --unlock-code unlock-code
  --endpoint https://device-local-ip
```

Example output:

```
{
    "RemoteMonitoringState" : "INSTALLED_ONLY"
}
```