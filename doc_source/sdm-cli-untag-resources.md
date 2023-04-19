# Remove tags<a name="sdm-cli-untag-resources"></a>

To remove a tag from a device, or from a task on a device, use the `untag-resources` command\.

To remove tags from a device, use the following command\. Replace each `user input placeholder` with your own information\. 

**Command**

```
aws snow-device-management untag-resources \
--resource-arn arn:aws:snow-device-management:us-west-2:123456789012:managed-device/smd-fictbgr3rbcjeqa5 \
--tag-keys Project
```

**Exceptions**

```
AccessDeniedException
InternalServerException
ResourceNotFoundException
ThrottlingException
```