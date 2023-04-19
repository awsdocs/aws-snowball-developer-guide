# Create a task<a name="sdm-cli-create-task"></a>

To instruct one or more target devices to perform a task, such as unlocking or rebooting, use `create-task`\. You specify target devices by providing a list of managed device IDs with the `--targets` parameter, and specify the tasks to perform with the `--command` parameter\. Only a single command can be run on a device at a time\.

Supported commands:
+ `unlock` \(no arguments\)
+ `reboot` \(no arguments\)

To create a task to be run by the target devices, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management create-task 
--targets smd-fictbgr3rbcjeqa5
--command reboot={}
```

**Exceptions**

```
ValidationException
ResourceNotFoundException
InternalServerException
ThrottlingException
AccessDeniedException
ServiceQuotaExceededException
```

**Output**

```
{
    "taskId": "st-ficthmqoc2pht111",
    "taskArn": "arn:aws:snow-device-management:us-west-2:000000000000:task/st-cjkwhmqoc2pht111"
}
```