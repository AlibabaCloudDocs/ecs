# DescribeInvocationResults

You can call this operation to query the execution results of one or more Cloud Assistant commands on ECS instances.

## Description

-   After you run a command, it may not succeed or achieve the expected results. You can call this operation to query the actual execution results.
-   You can query the execution information within the past two weeks. A maximum of 100,000 pieces of execution information can be retained.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInvocationResults&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInvocationResults|The operation that you want to perform. Set the value to DescribeInvocationResults. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InvokeId|String|No|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. You can call the [DescribeInvocations](~~64840~~) operation to query the execution IDs. |
|InstanceId|String|No|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. |
|CommandId|String|No|c-hz0jdfwcsr\*\*\*\*|The ID of the command. |
|InvokeRecordStatus|String|No|Running|The status of the execution. Valid values:

-   Running
-   Finished
-   Failed
-   Stopped |
|IncludeHistory|Boolean|No|false|Specifies whether to return the historical results of the recurring execution. Valid values:

-   true: returns the historical results of the recurring execution. When this parameter is set to true, the `InvokeId` parameter must be set to the ID of a recurring execution.
-   false: does not return the historical results of the recurring execution.

Default value: false. |
|ContentEncoding|String|No|PlainText|Specifies the encoding method of the `Output` response parameter. Valid values:

-   PlainText: returns the original command content and command output.
-   Base64: returns Base64-encoded command content and command output.

Default value: Base64. |
|PageNumber|Long|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|1|The number of entries to return on each page.

Maximum value: 50.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Invocation|Struct| |Details of the execution result. |
|InvocationResults|Array of InvocationResult| |The collection of execution results. |
|InvocationResult| | | |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|The ID of the command. |
|Dropped|Integer|0|The size of truncated and discarded text when the size of text in the `Output` response parameter is larger than 24 KB. |
|ErrorCode|String|InstanceNotExists|The code for the cause why a command fails to be sent or executed. Valid values:

-   If this parameter is empty, the command is run normally.
-   InstanceNotExists: The instance does not exist or is released.
-   InstanceReleased: The instance is released while the command is being run.
-   InstanceNotRunning: The instance is not running while the command is being run.
-   CommandNotApplicable: The command is not applicable to the instance.
-   AccountNotExists: The specified account does not exist.
-   DirectoryNotExists: The specified directory does not exist.
-   BadCronExpression: The specified cron expression for the execution time is invalid.
-   ClientNotRunning: The Cloud Assistant client is not running.
-   ClientNotResponse: The Cloud Assistant client does not respond.
-   ClientIsUpgrading: The Cloud Assistant client is being upgraded.
-   ClientNeedUpgrade: The Cloud Assistant client needs to be upgraded.
-   DeliveryTimeout: The request times out.
-   ExecutionTimeout: The execution times out.
-   ExecutionException: An exception occurs while the command is being run.
-   ExecutionInterrupted: The execution is interrupted.
-   ExitCodeNonzero: The execution is complete but the exit code is not zero. |
|ErrorInfo|String|the specified instance does not exists|The detailed cause why a command fails to be sent or executed. Valid values:

-   If this parameter is empty, the command is run normally.
-   the specified instance does not exists
-   the instance has released when create task
-   the instance is not running when create task
-   the command is not applicable
-   the specified account does not exists
-   the specified directory does not exists
-   the cron job expression is invalid
-   the aliyun service is not running on the instance
-   the aliyun service in the instance does not response
-   the aliyun service in the instance is upgrading now
-   the aliyun service in the instance need upgrade
-   the command delivery has been timeout
-   the command execution has been timeout
-   the command execution got an exception
-   the command execution has been interrupted
-   the command execution exit code is not zero |
|ExitCode|Long|0|The exit code of the command execution.

-   For Linux instances, the exit code is the exit code of the shell command.
-   For Windows instances, the exit code is the exit code of the batch or PowerShell command. |
|FinishedTime|String|2019-12-20T06:15:56Z|The time when the execution was complete. If an execution times out, the completion time of the execution is subject to the value of the TimedOut parameter specified in the [CreateCommand](~~64844~~) operation. |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. |
|InvocationStatus|String|Success|The command execution progress on a single instance. Valid values:

-   Pending: The system is verifying or sending the command.
-   Invalid: The specified command type or parameter is invalid.
-   Aborted: The command fails to be sent. To send a command to an instance, the instance must be in the Running state and the command must be sent within one minute.
-   Running: The command is being run on the instance.
-   Success:
    -   One-time execution: The execution is complete and the exit code is zero.
    -   Recurring execution: The last execution succeeds, the exit code is zero, and the specified cycle ends.
-   Failed:
    -   One-time execution: The execution is complete but the exit code is not zero.
    -   Recurring execution: The last execution is complete, the exit code is not 0, and the specified cycle is about to end.
-   Error: The execution cannot proceed due to an exception.
-   Timeout: The execution times out.
-   Cancelled: The execution has been canceled and the command has not been started.
-   Stopping: The running command is being stopped.
-   Terminated: The command is terminated when it is being run.
-   Scheduled:
    -   One-time execution: not applicable.
    -   Recurring execution: The command is waiting to be run. |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|InvokeRecordStatus|String|Running|The status of the execution. |
|Output|String|MTU6MzA6MDEK|The output of the execution. |
|Repeats|Integer|0|The number of executions on the instance.

-   If the execution mode is one-time execution, the value is 0 or 1.
-   If the execution mode is recurring execution, the value is the number of executions that have occurred. |
|StartTime|String|2019-12-20T06:15:55Z|The time when the command started to be run on the instance. |
|StopTime|String|2020-01-19T09:15:47Z|The time when the command stopped being run on the instance. If you called the `StopInvocation` operation to manually stop the execution, the value is the time when you call the operation. |
|Username|String|root|The username that was used to run the command on the ECS instance. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|1|The number of entries return per page. |
|TotalCount|Long|1|The total number of commands. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInvocationResults
&RegionId=cn-hangzhou
&InstanceId=i-bp1i7gg30r52z2em****
&PageNumber=1
&PageSize=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInvocationResultsResponse>
      <RequestId>F416C43A-6581-4138-9503-4FBBC4EA1BB7</RequestId>
      <Invocation>
            <InvocationResults>
                  <InvocationResult>
                        <Dropped>0</Dropped>
                        <InvocationStatus>Failed</InvocationStatus>
                        <InstanceId>i-bp1i7gg30r52z2em****</InstanceId>
                        <ExitCode>1</ExitCode>
                        <ErrorInfo>the command execution exit code is not zero.</ErrorInfo>
                        <StartTime>2020-05-11T09:01:40Z</StartTime>
                        <Repeats>1</Repeats>
                        <InvokeRecordStatus>Finished</InvokeRecordStatus>
                        <FinishedTime>2020-05-11T09:01:41Z</FinishedTime>
                        <Output></Output>
                        <CommandId>c-hz0jdfwcsr****</CommandId>
                        <ErrorCode>ExitCodeNonzero</ErrorCode>
                        <InvokeId>t-hz0jdfwd9f****</InvokeId>
                        <StopTime></StopTime>
                  </InvocationResult>
            </InvocationResults>
            <TotalCount>5</TotalCount>
            <PageSize>1</PageSize>
            <PageNumber>1</PageNumber>
      </Invocation>
</DescribeInvocationResultsResponse>
```

`JSON` format

```
{
    "RequestId": "F416C43A-6581-4138-9503-4FBBC4EA1BB7",
    "Invocation": {
        "InvocationResults": {
            "InvocationResult": [
                {
                    "Dropped": 0,
                    "InvocationStatus": "Failed",
                    "InstanceId": "i-bp1i7gg30r52z2em****",
                    "ExitCode": 1,
                    "ErrorInfo": "the command execution exit code is not zero.",
                    "StartTime": "2020-05-11T09:01:40Z",
                    "Repeats": 1,
                    "InvokeRecordStatus": "Finished",
                    "FinishedTime": "2020-05-11T09:01:41Z",
                    "Output": "",
                    "CommandId": "c-hz0jdfwcsr****",
                    "ErrorCode": "ExitCodeNonzero",
                    "InvokeId": "t-hz0jdfwd9f****",
                    "StopTime": ""
                }
            ]
        },
        "TotalCount": 5,
        "PageSize": 1,
        "PageNumber": 1
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because this API operation cannot be called in the specified region. Check whether the RegionId parameter is correct.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

