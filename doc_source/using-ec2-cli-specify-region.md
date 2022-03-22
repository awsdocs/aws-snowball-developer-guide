# Using the AWS CLI and API Operations on Snowball Edge<a name="using-ec2-cli-specify-region"></a>

When using the AWS Command Line Interface \(AWS CLI\) or API operations to issue IAM, Amazon S3 and Amazon EC2 commands on Snowball Edge, you must specify the `region` as "`snow`\." You can do this using `AWS configure` or within the command itself, as in the following examples\.

```
aws configure --profile ProfileName
AWS Access Key ID [None]: defgh
AWS Secret Access Key [None]: 1234567
Default region name [None]: snow
Default output format [None]: json
```

Or

```
aws s3 ls --profile ProfileName --endpoint http://192.0.2.0:8080 --region snow 
```