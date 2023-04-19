# List remote\-manageable devices<a name="sdm-cli-list-devices"></a>

To return a list of all devices on your account that have Snow Device Management enabled in the AWS Region where the command is run, use the `list-devices` command\. `--max-results` and `--next-token` are optional\. For more information, see [Using AWS CLI pagination options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-pagination.html) in the "AWS Command Line Interface User Guide"\.

To list remote\-manageable devices, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management list-devices \
--max-results 10
```

**Exceptions**

```
ValidationException
InternalServerException
ThrottlingException
AccessDeniedException
```

**Output**

```
{
    "devices": [
        {
            "associatedWithJob": "ID2bf11d5a-ea1e-414a-b5b1-3bf7e6a6e111",
            "managedDeviceId": "smd-fictbgr3rbcjeqa5",
            "managedDeviceArn": "arn:aws:snow-device-management:us-west-2:000000000000:managed-device/smd-fictbgr3rbcje111"
            "tags": {}
        }
    ]
}
```