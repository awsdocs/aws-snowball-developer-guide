# Apply tags<a name="sdm-cli-tag-resource"></a>

To add or replace a tag for a device, or for a task on a device, use the `tag-resource` command\. The `--tags` parameter accepts a comma\-separated list of `Key=Value` pairs\.

To apply tags to a device, use the following command\. Replace each `user input placeholder` with your own information\. 

**Command**

```
aws snow-device-management tag-resource \
--resource-arn arn:aws:snow-device-management:us-west-2:123456789012:managed-device/smd-fictbgr3rbcjeqa5 \
--tags Project=PrototypeA
```

**Exceptions**

```
AccessDeniedException
InternalServerException
ResourceNotFoundException
ThrottlingException
```