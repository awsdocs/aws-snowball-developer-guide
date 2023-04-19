# Check task metadata<a name="sdm-cli-describe-task"></a>

To check the metadata for a given task on a device, use the `describe-task` command\. The metadata for a task includes the following items: 
+ The target devices
+ The status of the task
+ When the task was created
+ When data was last updated on the device
+ When the task was completed
+ The description \(if any\) that was provided when the task was created

To check a task's metadata, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management describe-task \
--task-id st-ficthmqoc2pht111
```

**Exceptions**

```
ValidationException
ResourceNotFoundException
InternalServerException
ThrottlingException
AccessDeniedException
```

**Output**

```
{
    "completedAt": "2021-07-22T15:29:46.758000+00:00",
    "createdAt": "2021-07-22T15:28:42.613000+00:00",
    "lastUpdatedAt": "2021-07-22T15:29:46.758000+00:00",
    "state": "COMPLETED",
    "tags": {},
    "targets": [
        "smd-fictbgr3rbcje111"
    ],
    "taskId": "st-ficthmqoc2pht111",
    "taskArn": "arn:aws:snow-device-management:us-west-2:000000000000:task/st-ficthmqoc2pht111"
}
```