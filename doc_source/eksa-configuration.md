# Configuring and running Amazon EKS Anywhere on Snowball Edge devices<a name="eksa-configuration"></a>

Follow these procedures to configure and start Amazon EKS Anywhere on your Snowball Edge devices\. Then, to configure Amazon EKS Anywhere to operate on disconnected devices, complete additional procedures before disconnecting those devices from the external network\. For more information, see [Configuring Amazon EKS Anywhere on AWS Snow for disconnected operation](configure-disconnected.md)\.

**Topics**
+ [Initial setup](#initial-setup)
+ [Configuring and running Amazon EKS Anywhere on Snowball Edge devices automatically](#auto-eksa-configuration)
+ [Configuring and running Amazon EKS Anywhere on Snowball Edge devices manually](#manual-eksa-configuration)

## Initial setup<a name="initial-setup"></a>

Perform the initial setup on each Snowball Edge device by connecting the device to your local network, downloading the Snowball Edge client, getting credentials, and unlocking the device\.

**Perform initial setup**

1. Download and install the Snowball Edge client\. For more information, see [Downloading and Installing the Snowball Edge client](download-the-client.md)\.

1. Connect the device to your local network\. For more information, see [Connecting to Your Local Network](getting-started-connect.md)\.

1. Get credentials to unlock your device\. For more information, see [Getting Your Credentials and Tools](get-credentials.md)\.

1. Unlock the device\. For more information, see [Unlocking the Snowball Edge](unlockdevice.md)\. You can also use a script tool instead of unlocking devices manually\. See [Unlock devices](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/setup-tools#Unlock-devices)\.

## Configuring and running Amazon EKS Anywhere on Snowball Edge devices automatically<a name="auto-eksa-configuration"></a>

You can use sample script tools to set up the environment and run an Amazon EKS Anywhere admin instance or you can do so manually\. To use the script tools, see [Unlock devices and setup environment for Amazon EKS Anywhere](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/setup-tools#Unlock-devices-and-setup-envorinment-for-EKS-Anywhere)\. After the environment is set up and the Amazon EKS Anywhere admin instance is running, if you need to configure Amazon EKS Anywhere to operate on the Snowball Edge device while disconnected from a network, see [Configuring Amazon EKS Anywhere on AWS Snow for disconnected operation](configure-disconnected.md)\. Otherwise, see [Create, upgrade, and delete Amazon EKS Anywhere clusters on Snowball Edge devices](CrUD-clusters.md)\.

To manually set up the environment and run an Amazon EKS Anywhere admin instance, see [Configuring and running Amazon EKS Anywhere on Snowball Edge devices manually](#manual-eksa-configuration)\.

## Configuring and running Amazon EKS Anywhere on Snowball Edge devices manually<a name="manual-eksa-configuration"></a>

**Topics**
+ [Create an AWS CLI profile](#create-cli-profile)
+ [Create an Amazon EKS Anywhere IAM local user](#create-role)
+ [\(Optional\) Create and import a Secure Shell key](#create-ssh-key)
+ [Run an Amazon EKS Anywhere admin instance and transfer credential and certificate files to it](#start-config-eksa-admin-instance)

### Create an AWS CLI profile<a name="create-cli-profile"></a>

Create an AWS CLI profile to store credentials for use throughout the process of configuring Snowball Edge devices and the Amazon EKS Anywhere admin instance\. For more information about AWS CLI profiles, see [Named profiles for the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html) in the AWS Command Line Interface User Guide\.

You can use a sample script tool to automatically create the AWS CLI profile and the Amazon EKS Anywhere local IAM user\. See [Create credentials and certificates file](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/setup-tools#Create-credentials-and-certificates-file)\. After using the script, resume with [\(Optional\) Create and import a Secure Shell key](#create-ssh-key)\. Otherwise, follow this procedure and then the procedures in [Create an Amazon EKS Anywhere IAM local user](#create-role)\.

**Note**  
Do this for each Snowball Edge device that you configure\.

```
PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge list-access-keys --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code
{
 "AccessKeyIds" : [ "xxxx" ]
}
```

Use the value of `AccessKeyIds` as the value of the `access-key-id` parameter of the `get-secret-access-key` command\.

```
PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge get-secret-access-key --access-key-id ACCESS_KEY_ID --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code
[snowballEdge]
aws_access_key_id = xxx
aws_secret_access_key = xxx
```

Use the value of `aws_access_key_id` and `aws_secret_access_key` as the values of `AWS Access Key ID` and `AWS Secret Access Key` of the AWS CLI profile\.

```
aws configure --profile profile-name
AWS Access Key ID [None]: aws_access_key_id
AWS Secret Access Key [None]: aws_secret_access_key
Default region name [None]: snow
```

### Create an Amazon EKS Anywhere IAM local user<a name="create-role"></a>

For best security practices, create a local IAM user for Amazon EKS Anywhere on the Snowball Edge device\. You can do this by manually using the following procedures\.

**Note**  
Do this for each Snowball Edge device that you use\.

#### Create a local user<a name="create-eksa-iam-user"></a>

Use the `create-user` command to create the Amazon EKS Anywhere IAM user\.

```
aws iam create-user --user-name user-name --endpoint http://snowball-ip:6078 --profile profile-name
    {
        "User": {
            "Path": "/",
            "UserName": "eks-a-user",
            "UserId": "AIDACKCEVSQ6C2EXAMPLE",
            "Arn": "arn:aws:iam::123456789012:user/eks-a-user",
            "CreateDate": "2022-04-06T00:13:35.665000+00:00"
        }
    }
```

#### Create a policy for the local user<a name="create-eksa-iam-user-policy"></a>

Create a policy document, use it to create an IAM policy, and attach that policy to the Amazon EKS Anywhere local user\.

**To create a policy document and attach it to the Amazon EKS Anywhere local user**

1. Create a policy document and save it to your computer\. Copy the policy below to the document\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "snowballdevice:DescribeDevice",
           "snowballdevice:CreateDirectNetworkInterface",
           "snowballdevice:DeleteDirectNetworkInterface",
           "snowballdevice:DescribeDirectNetworkInterfaces",
           "snowballdevice:DescribeDeviceSoftware"
         ],
         "Resource": ["*"]
       },
       {
         "Effect": "Allow",
         "Action": [
           "ec2:RunInstances",
           "ec2:DescribeInstances",
           "ec2:TerminateInstances",
           "ec2:ImportKeyPair",
           "ec2:DescribeKeyPairs",
           "ec2:DescribeInstanceTypes",
           "ec2:DescribeImages",
           "ec2:DeleteTags"
         ],
         "Resource": ["*"]
       }
     ]
   }
   ```

1. Use the `create-policy` command to create an IAM policy based on the policy document\. The value of the `--policy-document` parameter should use the absolute path to the policy file\. For example, `file:///home/user/policy-name.json`

   ```
   aws iam create-policy --policy-name policy-name --policy-document file:///home/user/policy-name.json --endpoint http://snowball-ip:6078 --profile profile-name
   {
       "Policy": {
           "PolicyName": "policy-name",
           "PolicyId": "ANPACEMGEZDGNBVGY3TQOJQGEZAAAABP76TE5MKAAAABCCOTR2IJ43NBTJRZBU",
           "Arn": "arn:aws:iam::123456789012:policy/policy-name",
           "Path": "/",
           "DefaultVersionId": "v1",
           "AttachmentCount": 0,
           "IsAttachable": true,
           "CreateDate": "2022-04-06T04:46:56.907000+00:00",
           "UpdateDate": "2022-04-06T04:46:56.907000+00:00"
       }
   }
   ```

1. Use the `attach-user-policy` command to attach the IAM policy to the Amazon EKS Anywhere local user\.

   ```
   aws iam attach-user-policy --policy-arn policy-arn --user-name user-name --endpoint http://snowball-ip:6078 --profile profile-name     
   ```

#### Create an access key and a credential file<a name="create-eksa-iam-user-access-key"></a>

Create an access key for the Amazon EKS Anywhere IAM local user\. Then, create a credential file and include in it the values of `AccessKeyId` and `SecretAccessKey` generated for the local user\. The credential file will be used by the Amazon EKS Anywhere admin instance later\.

1. Use the `create-access-key` command to create an access key for the Amazon EKS Anywhere local user\.

   ```
   aws iam create-access-key --user-name user-name --endpoint http://snowball-ip:6078 --profile profile-name
       {
           "AccessKey": {
               "UserName": "eks-a-user",
               "AccessKeyId": "AKIAIOSFODNN7EXAMPLE",
               "Status": "Active",
               "SecretAccessKey": "RTT/wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
               "CreateDate": "2022-04-06T04:23:46.139000+00:00"
           }
       }
   ```

1. Create a credential file\. In it, save the `AccessKeyId` and `SecretAccessKey` values in the following format\.

   ```
   [snowball-ip] 
   aws_access_key_id = ABCDEFGHIJKLMNOPQR2T
   aws_secret_access_key = AfSD7sYz/TBZtzkReBl6PuuISzJ2WtNkeePw+nNzJ
   region = snow
   ```
**Note**  
If you're working with multiple Snowball Edge devices, the order of the credentials in the file doesn’t matter, but the credentials for all devices do need to be in one file\.

#### Create a certificates file for the admin instance<a name="create-credentials-for-admin-instance"></a>

The Amazon EKS Anywhere admin instance needs the certificates of the Snowball Edge devices in order to run on them\. Create a certificates file holding the certificate to access Snowball Edge devices for use later by the Amazon EKS Anywhere admin instance\.

**To create a certificates file**

1. Use the `list-certificates` command to get certificates for each Snowball Edge device that you plan to use\.

   ```
   PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge list-certificates --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code
   {
     "Certificates" : [ {
       "CertificateArn" : "arn:aws:snowball-device:::certificate/xxx",
       "SubjectAlternativeNames" : [ "ID:JID-xxx" ]
     } ]
   }
   ```

1. Use the value of `CertificateArn` as the value for the `--certificate-arn` parameter of the `get-certificate` command\. 

   ```
   PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge get-certificate --certificate-arn ARN --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code            
   ```

1. Create a device certificate file\. Put the output of `get-certificate` into the certificate file\. Following is an example of how to save the output\.
**Note**  
If you're working with multiple Snowball Edge devices, the order of the credentials in the file doesn’t matter, but the credentials for all devices do need to be in one file\.

   ```
   -----BEGIN CERTIFICATE-----
   ZWtzYSBzbm93IHRlc3QgY2VydGlmaWNhdGUgZWtzYSBzbm93IHRlc3QgY2VydGlm  
   aWNhdGVla3NhIHNub3cgdGVzdCBjZXJ0aWZpY2F0ZWVrc2Egc25vdyB0ZXN0IGNl  
   cnRpZmljYXRlZWtzYSBzbm93IHRlc3QgY2VydGlmaWNhdGVla3NhIHNub3cgdGVz  
   dCBjZXJ0aWZpY2F0ZQMIIDXDCCAkSgAwIBAgIJAISM0nTVmbj+MA0GCSqGSIb3DQ  
   ...                                                               
   -----END CERTIFICATE-----
   ```

1. Repeat [Create an Amazon EKS Anywhere IAM local user](#create-role) to create an IAM local user for Amazon EKS Anywhere on all Snowball Edge devices\.

### \(Optional\) Create and import a Secure Shell key<a name="create-ssh-key"></a>

Use this optional procedure to create a Secure Shell \(SSH\) key to access all Amazon EKS Anywhere node instances and to import the public key to all Snowball Edge devices\. Keep and secure this key file\.

If you skip this procedure, Amazon EKS Anywhere will create and import an SSH key automatically when necessary\. This key will be stored on the admin instance in `${PWD}/${CLUSTER_NAME}/eks-a-id_rsa`\.

**Create an SSH key and import it to the Amazon EKS Anywhere instance**

1. Use the `ssh-keygen` command to generate a SSH key\.

   ```
   ssh-keygen -t rsa -C "key-name" -f path-to-key-file
   ```

1. Use the `import-key-pair` command to import the key from your computer to the Snowball Edge device\.
**Note**  
The value of the `key-name` parameter must be the same when you import the key to all devices\.

   ```
   aws ec2 import-key-pair --key-name key-name --public-key-material fileb:///path/to/key-file --endpoint http://snowball-ip:8008 --profile profile-name 
   {
       "KeyFingerprint": "5b:0c:fd:e1:a0:69:05:4c:aa:43:f3:3b:3e:04:7f:51",
       "KeyName": "default",
       "KeyPairId": "s.key-85edb5d820c92a6f8"
   }
   ```

### Run an Amazon EKS Anywhere admin instance and transfer credential and certificate files to it<a name="start-config-eksa-admin-instance"></a>

#### Run an Amazon EKS Anywhere admin instance<a name="start-admin-instance"></a>

Follow this procedure to manually run an Amazon EKS Anywhere admin instance, configure a Virtual Network Interface \(VNI\) for the admin instance, check the status of the instance, create an SSH key, and connect to the admin instance with it\. You can use a sample script tool to automate creating an Amazon EKS Anywhere admin instance and transferring credential and certificate files to this instance\. See [Create Amazon EKS Anywhere admin instance](https://github.com/aws-samples/aws-snow-tools-for-eks-anywhere/tree/main/setup-tools#Create-EKS-Anywhere-admin-instance)\. After the script tool completes, you can ssh into the instance and create clusters by referring to [Create, upgrade, and delete Amazon EKS Anywhere clusters on Snowball Edge devices](CrUD-clusters.md)\. If you want to set up the Amazon EKS Anywhere instance manually, use the following steps\.\.

**Note**  
If you're using more than one Snowball Edge devices to provision the cluster, you can launch an Amazon EKS Anywhere admin instance on any of the Snowball Edge devices\.

**To run an Amazon EKS Anywhere admin instance**

1. Use the `create-key-pair` command to create a SSH key for the Amazon EKS Anywhere admin instance\. The command saves the key to `$PWD/key-file-name`\.

   ```
   aws ec2 create-key-pair --key-name key-name --query 'KeyMaterial' --output text --endpoint http://snowball ip:8008 --profile profile-name > key-file-name
   ```

1. Use the `describe-images` command to find the image name that begins with `eks-anywhere-admin` from the output\.

   ```
   aws ec2 describe-images --endpoint http://snowball-ip:8008 --profile profile-name
   ```

1. Use the `run-instance` command to start an eks\-a admin instance with the Amazon EKS Anywhere admin image\. 

   ```
   aws ec2 run-instances --image-id eks-a-admin-image-id --key-name key-name --instance-type sbe-c.xlarge --endpoint http://snowball-ip:8008 --profile profile-name
   ```

1. Use the `describe-instances` command to check the status of the Amazon EKS Anywhere instance\. Wait until the command indicates the instances state is `running` before continuing\.

   ```
   aws ec2 describe-instances --instance-id instance-id --endpoint http://snowball-ip:8008 --profile profile-name
   ```

1. From the output of the `describe-device` command, note the value of `PhysicalNetworkInterfaceId` for the physical network interface that is connected to your network\. You will use this to create a VNI\.

   ```
    
   PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge describe-device --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code
   ```

1. Create a VNI for the Amazon EKS Anywhere admin instance\. Use the value of `PhysicalNetworkInterfaceId` as the value of the `physical-network-interface-id` parameter\.

   ```
   PATH_TO_Snowball_Edge_CLIENT/bin/snowballEdge create-virtual-network-interface --ip-address-assignment dhcp --physical-network-interface-id PNI --endpoint https://snowball-ip --manifest-file path-to-manifest-file --unlock-code unlock-code
   ```

1. Use the value of `IpAddress` as the value of the `public-ip` parameter of the `associate-address` command to associate the public address to the Amazon EKS Anywhere admin instance\.

   ```
   aws ec2 associate-address --instance-id instance-id --public-ip VNI-IP --endpoint http://snowball-ip:8008 --profile profile-name 
   ```

1. Connect to the Amazon EKS Anywhere admin instance by SSH\.

   ```
   ssh -i path-to-key ec2-user@VNI-IP      
   ```

#### Transfer certificate and credential files to the admin instance<a name="transfer-cred-cert-files"></a>

After the Amazon EKS Anywhere admin instance is running, transfer the credentials and certificates of your Snowball Edge devices to the admin instance\. Run the following command from the same directory where you saved the credentials and certificates files in [Create an access key and a credential file](#create-eksa-iam-user-access-key) and [Create a certificates file for the admin instance](#create-credentials-for-admin-instance)\.

```
scp -i path-to-key path-to-credentials-file path-to-certificates-file ec2-user@eks-admin-instance-ip:~        
```

Verify the contents of the files on the Amazon EKS Anywhere admin instance\. Following are examples of the credential and certificate files\.

```
[192.168.1.1] 
aws_access_key_id = EMGEZDGNBVGY3TQOJQGEZB5ULEAAIWHWUJDXEXAMPLE 
aws_secret_access_key = AUHpqjO0GZQHEYXDbN0neLNlfR0gEXAMPLE 
region = snow 

[192.168.1.2] 
aws_access_key_id = EMGEZDGNBVGY3TQOJQGEZG5O7F3FJUCMYRMI4KPIEXAMPLE 
aws_secret_access_key = kY4Cl8+RJAwq/bu28Y8fUJepwqhDEXAMPLE 
region = snow
```

```
-----BEGIN CERTIFICATE-----                                      
ZWtzYSBzbm93IHRlc3QgY2VydGlmaWNhdGUgZWtzYSBzbm93IHRlc3QgY2VydGlm  
aWNhdGVla3NhIHNub3cgdGVzdCBjZXJ0aWZpY2F0ZWVrc2Egc25vdyB0ZXN0IGNl  
cnRpZmljYXRlZWtzYSBzbm93IHRlc3QgY2VydGlmaWNhdGVla3NhIHNub3cgdGVz  
dCBjZXJ0aWZpY2F0ZQMIIDXDCCAkSgAwIBAgIJAISM0nTVmbj+MA0GCSqGSIb3DQ  
...                                                               
-----END CERTIFICATE-----                                         

-----BEGIN CERTIFICATE-----                                       
KJ0FPl2PAYPEjxr81/PoCXfZeARBzN9WLUH5yz1ta+sYUJouzhzWuLJYA1xqcCPY  
mhVlkRsN4hVdlBNRnCCpRF766yjdJeibKVzXQxoXoZBjrOkuGwqRy3d3ndjK77h4  
OR5Fv9mjGf7CjcaSjk/4iwmZvRSaQacb0YG5GVeb4mfUAuVtuFoMeYfnAgMBAAGj  
azBpMAwGA1UdEwQFMAMBAf8wHQYDVR0OBBYEFL/bRcnBRuSM5+FcYFa8HfIBomdF  
...                                                              
-----END CERTIFICATE-----
```