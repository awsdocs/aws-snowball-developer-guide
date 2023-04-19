# List tasks by status<a name="sdm-cli-list-tasks"></a>

Use the `list-tasks` command to return a list of tasks from the devices in the AWS Region where the command is run\. To filter the results by `IN_PROGRESS`, `COMPLETED`, or `CANCELED` status, use the `--state` parameter\. `--max-results` and `--next-token` are optional\. For more information, see [Using AWS CLI pagination options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-pagination.html) in the "AWS Command Line Interface User Guide"\.

To list tasks by status, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management list-tasks \
--state IN_PROGRESS \
--next-token K8VAMqKiP2Cf4xGkmH8GMyZrgOF8FUb+d1OKTP9+P4pUb+8PhW+6MiXh4= \
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
    "tasks": [
        {
            "state": "IN_PROGRESS",
            "tags": {},
            "taskId": "st-ficthmqoc2phtlef",
            "taskArn": "arn:aws:snow-device-management:us-west-2:000000000000:task/st-ficthmqoc2phtlef"
          
        }
    ]
}
```