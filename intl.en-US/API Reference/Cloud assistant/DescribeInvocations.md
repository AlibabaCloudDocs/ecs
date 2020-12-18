# DescribeInvocations

You can call this operation to query the execution list and status of Cloud Assistant commands.

## Description

-   After you run a command, it may not succeed. You must call the operation to query the actual execution result.
-   You can query the execution information within the past two weeks. A maximum of 100,000 pieces of execution information can be retained.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInvocations|The operation that you want to perform. Set the value to DescribeInvocations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InvokeId|String|No|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|CommandId|String|No|c-hz0jdfwcsr\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|CommandName|String|No|CommandTestName|The name of the command. |
|CommandType|String|No|RunShellScript|The type of the command. |
|Timed|Boolean|No|true|Specifies whether to run the command on a scheduled basis.

Default value: false. |
|InvokeStatus|String|No|Finished|The overall execution status of the command. The value of this parameter depends on the overall execution status of the command on all the involved instances \(`InstanceInvokeStatus`\). Valid values:

-   Running:
    -   Scheduled invocation: Before you manually stop the command, the execution status is always Running.
    -   One-time invocation: As long as the command is being executed on one instance, the overall execution status is Running.
-   Finished:
    -   Scheduled invocation: The command execution status can never be Finished.
    -   One-time invocation: The command execution on all instances is complete, or the command execution on some instances is manually stopped and that on the other instances is complete.
-   Failed:
    -   Scheduled invocation: The command execution status can never be Failed.
    -   One-time invocation: The command execution fails on all instances.
-   PartialFailed:
    -   Scheduled invocation: The command execution status can never be PartialFailed.
    -   One-time invocation: The command execution fails on some instances.
-   Stopped: The command is stopped.

Default value: Running. |
|InstanceId|String|No|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. When you specify this parameter, the system queries all the command execution records of the instance. |
|ContentEncoding|String|No|PlainText|The encoding method of the `CommandContent` and `Output` response parameters. Valid values:

-   PlainText: returns the original command content and command output.
-   Base64: returns Base64-encoded command content and command output.

Default value: Base64. |
|IncludeOutput|Boolean|No|false|Specifies whether to return the execution output information in the result.

-   true: The execution output information is returned in the result. When this parameter is set to true, you must specify at least one of the following parameters: `InvokeId` and `InstanceId`.
-   false: The execution output information is not returned in the result.

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
|Invocations|Array| |Details about the command execution records. |
|Invocation| | | |
|CommandContent|String|cnBtIC1xYSB8IGdyZXAgdnNm\*\*\*\*|The Base64-encoded command content. |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|The ID of the command. |
|CommandName|String|CommandTestName|The name of the command. |
|CommandType|String|RunShellScript|The type of the command. |
|CreationTime|String|2020-01-19T09:15:46Z|The time when the task was created. |
|Frequency|String|0 \*/20 \* \* \* \*|The execution cycle of the scheduled invocation. For more information about the value specifications, see [Cron expression](~~64769~~). |
|InvocationStatus|String|Pending|The overall execution status of the command. The value of this parameter depends on the overall execution status on all the involved instances. Valid values:

-   Pending: The system is verifying or sending the command. When the execution status on at least one instance is Pending, the overall execution status is Pending.
-   Scheduled: The scheduled command is sent and waiting to be executed. When the execution status on at least one instance is Scheduled, the overall execution status is Scheduled.
-   Running: The command is running on the instances. When the execution status on at least one instance is Running, the overall execution status is Running.
-   Success: When the execution status on all instances is Stopped or Success and the execution status on at least one instance is Success, the overall execution status is Success.
    -   One-time invocation: The execution is complete and the exit code is 0.
    -   Scheduled invocation: The last execution succeeds, the exit code is 0, and the specified cycle has ended.
-   Failed: When the execution status on all instances is Stopped or Failed and the execution status on at least one instance is Failed, the overall execution status is Failed. When the execution status on the instances is one of the following values, Failed is returned:
    -   Invalid: The command is invalid.
    -   Aborted: The command fails to be sent.
    -   Failed: The execution is complete but the exit code is not 0.
    -   Timeout: The execution times out.
    -   Error: An error occurs when the command is being executed.
-   Stopping: The task is being stopped. When the execution status on at least one instance is Stopping, the overall execution status is Stopping.
-   Stopped: The task is stopped. When the execution status on all instances is Stopped, the overall execution status is Stopped. When the execution status on the instances is one of the following values, Stopped is returned:
    -   Cancelled: The task is canceled.
    -   Terminated: The task is terminated.
-   PartialFailed: The execution succeeds on some instances and fails on some other instances. If the execution status on all instances is Success, Failed, or Stopped, the overall execution status is PartialFailed.

**Note:** The `InvokeStatus` parameter is similar to this parameter, but we recommend that you check this parameter. |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|InvokeInstances|Array| |Details about the instances on which the command is executed. |
|InvokeInstance| | | |
|CreationTime|String|2019-12-20T06:15:54Z|The time when the command execution was created. |
|Dropped|Integer|0|The size of truncated and discarded text when the size of text in the Output field is larger than 24 KB. |
|ErrorCode|String|InstanceNotExists|The code for the cause why a command fails to be sent or executed. Valid values:

-   Null: The command runs normally.
-   InstanceNotExists: The instance does not exist or is released.
-   InstanceReleased: The instance is released while the task is being executed.
-   InstanceNotRunning: The instance is not running when the task is being created.
-   CommandNotApplicable: The command is not applicable to the specified instance.
-   AccountNotExists: The specified account does not exist.
-   DirectoryNotExists: The specified directory does not exist.
-   BadCronExpression: The specified cron expression for the execution cycle is invalid.
-   ClientNotRunning: The Cloud Assistant client is not running.
-   ClientNotResponse: The Cloud Assistant client is not responding.
-   ClientIsUpgrading: The Cloud Assistant client is being upgraded.
-   ClientNeedUpgrade: The Cloud Assistant client needs to be upgraded.
-   DeliveryTimeout: The request times out.
-   ExecutionTimeout: The execution times out.
-   ExecutionException: An exception occurs when the command is running.
-   ExecutionInterrupted: The task is interrupted.
-   ExitCodeNonzero: The execution is complete but the exit code is not 0. |
|ErrorInfo|String|the specified instance does not exists|The detailed cause why a command fails to be sent or executed. Valid values:

-   Null: The command runs normally
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
|ExitCode|Long|0|The exit code of the command execution. Valid values:

-   For Linux instances, the exit code is the exit code of the shell process.
-   For Windows instances, the exit code is the exit code of the batch or PowerShell process. |
|FinishTime|String|2019-12-20T06:15:56Z|The end time of the command execution. |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. |
|InstanceInvokeStatus|String|Finished|The command execution status on a single instance. Valid values:

-   Running:
    -   Scheduled invocation: Before you manually stop the command, the command execution status is always Running.
    -   One-time invocation: The command is running.
-   Finished:
    -   Scheduled invocation: The command execution status cannot be Finished.
    -   One-time invocation: The command is executed.
-   Failed:
    -   Scheduled invocation: The command execution status cannot be Failed.
    -   One-time invocation: The command execution fails.
-   Stopped: The command execution is stopped.
-   PartialFailed:
    -   Scheduled invocation: The command execution status cannot be PartialFailed.
    -   One-time invocation: The command execution fails on some instances. |
|InvocationStatus|String|Success|The command execution progress on a single instance. Valid values:

-   Pending: The system is verifying or sending the command.
-   Invalid: The specified command type or parameter is invalid.
-   Aborted: The command fails to be sent. The instance must be in the Running state and the command can be sent within one minute.
-   Running: The command is running on the instance.
-   Success:
    -   One-time invocation: The execution is complete and the exit code is 0.
    -   Scheduled invocation: The last execution succeeds, the exit code is 0, and the specified cycle has ended.
-   Failed:
    -   One-time invocation: The execution is complete but the exit code is not 0.
    -   Scheduled invocation: The last execution is complete, the exit code is not 0, and the specified cycle is about to end.
-   Error: The execution cannot proceed due to an exception.
-   Timeout: The execution times out.
-   Cancelled: The task has been canceled and the command has not been started.
-   Stopping: The task is being stopped.
-   Terminated: The command is terminated when it is running.
-   Scheduled:
    -   One-time invocation: not applicable.
    -   Scheduled invocation: The command is waiting to be run. |
|Output|String|OutPutTestmsg|The output of the command execution. |
|Repeats|Integer|0|The number of executions on the instance.

-   If the execution mode is one-time invocation, the value is 0 or 1.
-   If the execution mode is scheduled invocation, the value is the number of executions that have occurred. |
|StartTime|String|2019-12-20T06:15:55Z|The time when the command started to be executed on the instance. |
|StopTime|String|2020-01-19T09:15:47Z|The time when you called the `StopInvocation` operation to manually stop the command execution. |
|UpdateTime|String|2020-01-19T09:15:47Z|The time when the task status was updated. |
|InvokeStatus|String|Finished|The overall execution status of the command.

**Note:** We recommend that you ignore this parameter and check the returned values of the `InvocationStatus` parameter. |
|Parameters|String|\{\}|The custom parameters in the command. |
|Timed|Boolean|false|Indicates whether the command is run on a scheduled basis. |
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
                              <ErrorInfo>the command execution exit code is not zero. </ErrorInfo>
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
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

