# DescribeInvocations

You can call this operation to query the execution list and status of Cloud Assistant commands.

## Description

-   After you run a command, it may not succeed or achieve the expected results. You can call this operation to query the actual execution results.
-   You can query the execution information within the last two weeks. A maximum of 100,000 pieces of execution information can be retained.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations&type=RPC&version=2014-05-26)

## Request Parameter

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInvocations|The operation that you want to perform. Set the value to DescribeInvocations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InvokeId|String|No|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|CommandId|String|No|c-hz0jdfwcsr\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|CommandName|String|No|CommandTestName|The name of the command. |
|CommandType|String|No|RunShellScript|The type of the command. |
|Timed|Boolean|No|true|Specifies whether to periodically run the command.

Default value: false. |
|InvokeStatus|String|No|Finished|The overall status of the execution. The value is determined by the execution status of the command on all the involved instances. Valid values:

-   Running:
    -   Recurring execution: Before you manually stop the command, the overall execution status is always Running.
    -   One-time execution: If the command is being run on one or more instances, the overall execution status is Running.
-   Finished:
    -   Recurring execution: The overall execution status can never be Finished.
    -   One-time execution: The execution is complete on all instances, or the execution is manually stopped on some instances and is complete on the other instances.
-   Failed:
    -   Recurring execution: The overall execution status can never be Failed.
    -   One-time execution: The execution fails on all instances.
-   PartialFailed:
    -   Recurring execution: The overall execution status can never be PartialFailed.
    -   One-time execution: The execution fails on some instances.
-   Stopped: The execution is stopped.

Default value: Running. |
|InstanceId|String|No|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. When you specify this parameter, the system queries all the execution records of the instance. |
|ContentEncoding|String|No|PlainText|The encoding mode of the `CommandContent` and `Output` response parameters. Valid values:

-   PlainText: returns the original command content and command output.
-   Base64: returns the Base64-encoded command content and command output.

Default value: Base64. |
|IncludeOutput|Boolean|No|false|Specifies whether to return the command outputs in the response.

-   true: returns the command outputs. When this parameter is set to true, you must specify `InvokeId`, `InstanceId`, or both of them.
-   false: does not return the command outputs.

Default value: false. |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page.

Maximum value: 50.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Invocations|Array of Invocation| |Details of execution records. |
|Invocation| | | |
|CommandContent|String|cnBtIC1xYSB8IGdyZXAgdnNm\*\*\*\*|The Base64-encoded command content. |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|The ID of the command. |
|CommandName|String|CommandTestName|The name of the command. |
|CommandType|String|RunShellScript|The type of the command. |
|CreationTime|String|2020-01-19T09:15:46Z|The time when the task was created. |
|Frequency|String|0 \*/20 \* \* \* \*|The time when recurring executions of the command take place. For more information about the value pattern, see [Cron expression](~~64769~~). |
|InvocationStatus|String|Pending|The overall execution status. This value is determined by the overall execution status on all the involved instances. Valid values:

-   Pending: The system is verifying or sending the command. When the execution status on at least one instance is Pending, the overall execution status is Pending.
-   Scheduled: The recurring command was sent and waiting to be run. When the execution status on at least one instance is Scheduled, the overall execution status is Scheduled.
-   Running: The command is being run on the instance. When the execution status on at least one instance is Running, the overall execution status is Running.
-   Success: When the execution status on all instances is Stopped or Success and the execution status on at least one instance is Success, the overall execution status is Success.
    -   One-time execution: The execution is complete and the exit code is zero.
    -   Recurring execution: The last execution succeeds, the exit code is zero, and the specified cycle ends.
-   Failed: When the execution status on all instances is Stopped or Failed, the overall execution status is Failed. When the execution status on an instance is one of the following values, Failed is returned as the overall execution status:
    -   Invalid: The command is invalid.
    -   Aborted: The command fails to be sent.
    -   Failed: The execution is complete but the exit code is a non-zero value.
    -   Timeout: The execution times out.
    -   Error: An error occurs while the execution is in progress.
-   Stopping: The execution is being stopped. When the execution status on at least one instance is Stopping, the overall execution status is Stopping.
-   Stopped: The execution is stopped. When the execution status on all instances is Stopped, the overall execution status is Stopped. When the execution status on an instance is one of the following values, Stopped is returned as the overall execution status:
    -   Cancelled: The execution is canceled.
    -   Terminated: The execution is terminated.
-   PartialFailed: The execution succeeds on some instances and fails on the other instances. If the execution status is Success on some instances, and is Failed or Stopped on the other instances, the overall execution status is PartialFailed.

**Note:** The `InvokeStatus` parameter is similar to this parameter, but we recommend that you check this parameter. |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|InvokeInstances|Array of InvokeInstance| |Details of the instances on which the command is run. |
|InvokeInstance| | | |
|CreationTime|String|2019-12-20T06:15:54Z|The start time of the execution. |
|Dropped|Integer|0|The size of truncated and discarded text when the size of text in the Output response parameter is larger than 24 KB. |
|ErrorCode|String|InstanceNotExists|The code for the cause why a command failed to be sent or run. Valid values:

-   If this parameter is empty, the command is run normally.
-   InstanceNotExists: The instance does not exist or is released.
-   InstanceReleased: The instance is released while the command is being run.
-   InstanceNotRunning: The instance is not running when the command begins to be run.
-   CommandNotApplicable: The command is not applicable to the specified instance.
-   AccountNotExists: The specified account does not exist.
-   DirectoryNotExists: The specified directory does not exist.
-   BadCronExpression: The specified cron expression for the execution cycle is invalid.
-   ClientNotRunning: The Cloud Assistant client is not running.
-   ClientNotResponse: The Cloud Assistant client does not respond.
-   ClientIsUpgrading: The Cloud Assistant client is being upgraded.
-   ClientNeedUpgrade: The Cloud Assistant client needs to be upgraded.
-   DeliveryTimeout: The request times out.
-   ExecutionTimeout: The execution times out.
-   ExecutionException: An exception occurs when the command is being run.
-   ExecutionInterrupted: The execution is interrupted.
-   ExitCodeNonzero: The execution is complete but the exit code is a non-zero value. |
|ErrorInfo|String|the specified instance does not exists|The detailed cause why a command failed to be sent or run. Valid values:

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
|ExitCode|Long|0|The exit code of the execution.

-   For Linux instances, the exit code is the exit code of the shell process.
-   For Windows instances, the exit code is the exit code of the batch or PowerShell process. |
|FinishTime|String|2019-12-20T06:15:56Z|The end time of the execution. |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. |
|InstanceInvokeStatus|String|Finished|**Note:** We recommend that you ignore this parameter and check the returned values of the `InvocationStatus` parameter for the overall execution status. |
|InvocationStatus|String|Success|The execution status on a single instance. Valid values:

-   Pending: The system is verifying or sending the command.
-   Invalid: The specified command type or parameter is invalid.
-   Aborted: The command fails to be sent. The instance must be in the Running state and the command must be sent within 1 minute so that the command can be sent to the instance.
-   Running: The command is being run on the instance.
-   Success:
    -   One-time execution: The execution is complete and the exit code is zero.
    -   Recurring execution: The last execution succeeds, the exit code is zero, and the specified cycle ends.
-   Failed:
    -   One-time execution: The execution is complete but the exit code is a non-zero value.
    -   Recurring execution: The last execution is complete, the exit code is a non-zero value, and the specified cycle is about to end.
-   Error: The execution cannot proceed due to an exception.
-   Timeout: The execution times out.
-   Cancelled: The execution is canceled and the command is not started.
-   Stopping: The execution is being stopped.
-   Terminated: The command is terminated when it is being run.
-   Scheduled:
    -   One-time execution: not applicable.
    -   Recurring execution: The command is waiting to be run. |
|Output|String|OutPutTestmsg|The output of the command. |
|Repeats|Integer|0|The number of executions on the instance.

-   For one-time executions, the value is 0 or 1.
-   For recurring executions, the value is the number of executions that have occurred on the instance. |
|StartTime|String|2019-12-20T06:15:55Z|The time when the command started to be run on the instance. |
|StopTime|String|2020-01-19T09:15:47Z|The time when the command stopped being run on the instance. If you called the `StopInvocation` operation to manually stop the execution, the value is the time when you called the operation. |
|UpdateTime|String|2020-01-19T09:15:47Z|The time when the execution status was updated. |
|InvokeStatus|String|Finished|The overall execution status.

**Note:** We recommend that you ignore this parameter and check the returned values of the `InvocationStatus` parameter for the overall execution status. |
|Parameters|String|\{\}|The custom parameters in the command. |
|Timed|Boolean|false|Indicates whether the execution is a recurring execution. |
|Username|String|root|The username that was used to run the command on the ECS instance. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Long|2|The total number of commands. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInvocations
&RegionId=cn-hangzhou
&InvokeId=t-hz0jdfwd9f****
&CommandId=c-hz0jdfwcsr****
&CommandName=CommandTestName
&CommandType=RunShellScrip
&Timed=true
&InvokeStatus=Finished
&InstanceId=i-bp1i7gg30r52z2em****
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInvocationsResponse>
      <TotalCount>5</TotalCount>
      <RequestId>634562E9-F291-4289-B60B-FC511A43CD34</RequestId>
      <PageSize>1</PageSize>
      <PageNumber>1</PageNumber>
      <Invocations>
            <Invocation>
                  <CommandContent>cnBtIC1xYSB8IGdyZXAgdnNm****</CommandContent>
                  <InvocationStatus>Failed</InvocationStatus>
                  <InvokeStatus>Finished</InvokeStatus>
                  <Parameters>{}</Parameters>
                  <CommandType>RunShellScript</CommandType>
                  <Timed>false</Timed>
                  <CreationTime>2020-05-11T09:01:39Z</CreationTime>
                  <Frequency></Frequency>
                  <CommandId>c-hz0jdfwcsr****</CommandId>
                  <CommandName>AutoTest</CommandName>
                  <InvokeId>t-hz0jdfwd9f****</InvokeId>
                  <InvokeInstances>
                        <InvokeInstance>
                              <Dropped>0</Dropped>
                              <InvocationStatus>Failed</InvocationStatus>
                              <InstanceId>i-bp1i7gg30r52z2em****</InstanceId>
                              <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
                              <ExitCode>1</ExitCode>
                              <ErrorInfo>the command execution exit code is not zero.</ErrorInfo>
                              <StartTime>2020-05-11T09:01:40Z</StartTime>
                              <Repeats>1</Repeats>
                              <FinishTime>2020-05-11T09:01:41Z</FinishTime>
                              <Output></Output>
                              <CreationTime>2020-05-11T09:01:39Z</CreationTime>
                              <UpdateTime>2020-05-11T09:01:41Z</UpdateTime>
                              <ErrorCode>ExitCodeNonzero</ErrorCode>
                              <StopTime></StopTime>
                        </InvokeInstance>
                  </InvokeInstances>
            </Invocation>
      </Invocations>
</DescribeInvocationsResponse>
```

`JSON` format

```
{
    "TotalCount": 5,
    "RequestId": "634562E9-F291-4289-B60B-FC511A43CD34",
    "PageSize": 1,
    "PageNumber": 1,
    "Invocations": {
        "Invocation": [
            {
                "CommandContent": "cnBtIC1xYSB8IGdyZXAgdnNm****",
                "InvocationStatus": "Failed",
                "InvokeStatus": "Finished",
                "Parameters": "{}",
                "CommandType": "RunShellScript",
                "Timed": false,
                "CreationTime": "2020-05-11T09:01:39Z",
                "Frequency": "",
                "CommandId": "c-hz0jdfwcsr****",
                "CommandName": "AutoTest",
                "InvokeId": "t-hz0jdfwd9f****",
                "InvokeInstances": {
                    "InvokeInstance": [
                        {
                            "Dropped": 0,
                            "InvocationStatus": "Failed",
                            "InstanceId": "i-bp1i7gg30r52z2em****",
                            "InstanceInvokeStatus": "Finished",
                            "ExitCode": 1,
                            "ErrorInfo": "the command execution exit code is not zero.",
                            "StartTime": "2020-05-11T09:01:40Z",
                            "Repeats": 1,
                            "FinishTime": "2020-05-11T09:01:41Z",
                            "Output": "",
                            "CreationTime": "2020-05-11T09:01:39Z",
                            "UpdateTime": "2020-05-11T09:01:41Z",
                            "ErrorCode": "ExitCodeNonzero",
                            "StopTime": ""
                        }
                    ]
                }
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because this API operation cannot be called in the specified region. Check whether the RegionId parameter is valid.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

