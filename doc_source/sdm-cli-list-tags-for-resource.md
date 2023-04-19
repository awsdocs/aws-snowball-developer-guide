# List device or task tags<a name="sdm-cli-list-tags-for-resource"></a>

To return a list of tags for a managed device or task, use the `list-tags-for-resource` command\.

To list the tags for a device, use the following command\. Replace the example Amazon Resource Name \(ARN\) with the ARN for your device\. 

**Command**

```
aws snow-device-management list-tags-for-resource
--resource-arn arn:aws:snow-device-management:us-west-2:123456789012:managed-device/smd-fictbgr3rbcjeqa5
```

**Exceptions**

```
AccessDeniedException
InternalServerException
ResourceNotFoundException
ThrottlingException
```

**Output**

```
{
    "tags": {
        "Project": "PrototypeA"
    }
}
```