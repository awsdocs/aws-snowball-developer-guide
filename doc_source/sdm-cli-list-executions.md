# List task status across devices<a name="sdm-cli-list-executions"></a>

To return the status of tasks for one or more target devices, use the `list-executions` command\. To filter the return list to show tasks that are currently in a single specific state, use the `--state` parameter\. `--max-results` and `--next-token` are optional\. For more information, see [Using AWS CLI pagination options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-pagination.html) in the "AWS Command Line Interface User Guide"\.

A task can have one of the following states:
+ `QUEUED`
+ `IN_PROGRESS`
+ `CANCELED`
+ `FAILED`
+ `COMPLETED`
+ `REJECTED`
+ `TIMED_OUT`

To list task status across devices, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management list-executions \
--taskId st-ficthmqoc2phtlef \
--state SUCCEEDED \
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
    "executions": [
        {
            "executionId": "1",
            "managedDeviceId": "smd-fictbgr3rbcje111",
            "state": "SUCCEEDED",
            "taskId": "st-ficthmqoc2pht111"
        }
    ]
}
```