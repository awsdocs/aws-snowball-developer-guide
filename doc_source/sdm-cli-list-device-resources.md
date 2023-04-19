# List available resources<a name="sdm-cli-list-device-resources"></a>

To return a list of the AWS resources available for a device, use the `list-device-resources` command\. To filter the list by a specific type of resource, use the `--type` parameter\. Currently, Amazon EC2 instances are the only supported resource type\. `--max-results` and `--next-token` are optional\. For more information, see [Using AWS CLI pagination options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-pagination.html) in the "AWS Command Line Interface User Guide"\.

To list the available resources for a device, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management list-device-resources \
--managed-device-id smd-fictbgr3rbcje111 \
--type AWS::EC2::Instance
--next-token YAQGPwAT9l3wVKaGYjt4yS34MiQLWvzcShe9oIeDJr05AT4rXSprqcqQhhBEYRfcerAp0YYbJmRT=
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
    "resources": [
        {
            "id": "s.i-84fa8a27d3e15e111",
            "resourceType": "AWS::EC2::Instance"
        }
    ]
}
```