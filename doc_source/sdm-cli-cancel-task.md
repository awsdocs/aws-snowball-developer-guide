# Cancel a task<a name="sdm-cli-cancel-task"></a>

To send a cancel request for a specific task, use the `cancel-task` command\. You can cancel only tasks in the `QUEUED` state that have not yet run\. Tasks that are already running can't be canceled\. 

**Note**  
A task that you're attempting to cancel might still run if it is processed from the queue before the `cancel-task` command changes the task's state\.

To cancel a task, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management cancel-task \
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
    "taskId": "st-ficthmqoc2pht111"
}
```