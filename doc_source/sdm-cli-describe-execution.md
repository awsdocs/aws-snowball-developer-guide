# Check task status<a name="sdm-cli-describe-execution"></a>

To check the status of a remote task running on one or more target devices, use the `describe-execution` command\.

A task can have one of the following states:
+ `QUEUED`
+ `IN_PROGRESS`
+ `CANCELED`
+ `FAILED`
+ `COMPLETED`
+ `REJECTED`
+ `TIMED_OUT`

To check the status of a task, use the following command\. Replace each `user input placeholder` with your own information\.

**Command**

```
aws snow-device-management describe-execution \
--taskId st-ficthmqoc2phtlef \
--managed-device-id smd-fictqic6gcldf111
```

**Output**

```
{
    "executionId": "1",
    "lastUpdatedAt": "2021-07-22T15:29:44.110000+00:00",
    "managedDeviceId": "smd-fictqic6gcldf111",
    "startedAt": "2021-07-22T15:28:53.947000+00:00",
    "state": "SUCCEEDED",
    "taskId": "st-ficthmqoc2pht111"
}
```