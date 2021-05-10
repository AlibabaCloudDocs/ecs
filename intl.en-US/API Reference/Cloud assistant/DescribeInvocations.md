# DescribeInvocations

You can call this operation to query the execution list and status of Cloud Assistant commands.

## Description

-   After you run a command, the command may not succeed or achieve the expected results. You can call this operation to query the execution results.
-   You can query the execution information that is generated in the last two weeks. A maximum of 100,000 pieces of execution information can be retained.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInvocations&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInvocations|The operation that you want to perform. Set the value to DescribeInvocations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InvokeId|String|No|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|CommandId|String|No|c-hz0jdfwcsr\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|CommandName|String|No|CommandTestName|The name of the command. |
|CommandType|String|No|RunShellScript|The type of the command. |
|Timed|Boolean|No|true|Specifies whether to query the commands to be automatically run. Valid values:

-   true: queries the commands that are to be run by calling the `RunCommand` or `InvokeCommand` operation and setting the `RepeatMode` parameter to `Period`, `NextRebootOny`, or `EveryReboot`. The executions of these commands are not canceled or stopped and not complete.
-   false: queries commands that meet the following requirements:
    -   Commands that are to be run by calling the `RunCommand` or `InvokeCommand` operation and setting the `RepeatMode` parameter to `Once`.
    -   Commands whose executions are canceled, stopped, or complete.

Default value: false. |
|InvokeStatus|String|No|Finished|The overall execution status of the command. The value of this parameter depends on the execution status on all the involved instances \(InstanceInvokeStatus\). Valid values:

-   Running:
    -   Recurring execution: Before you manually stop the execution of the command, the overall execution status is always Running.
    -   One-time execution: If the execution is in progress on one or more instances, the overall execution status is Running.
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

-   PlainText: returns the original command content and command outputs.
-   Base64: returns the Base64-encoded command content and command outputs.

Default value: Base64. |
|IncludeOutput|Boolean|No|false|Specifies whether to return the command outputs in the response.

-   true: returns the command outputs. When this parameter is set to true, you must specify `InvokeId`, `InstanceId` or both.
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
|Invocations|Array of Invocation| |Details of the command executions. |
|Invocation| | | |
|CommandContent|String|cnBtIC1xYSB8IGdyZXAgdnNm\*\*\*\*|The Base64-encoded command content. |
|CommandId|String|c-hz0jdfwcsr\*\*\*\*|The ID of the command. |
|CommandName|String|CommandTestName|The name of the command. |
|CommandType|String|RunShellScript|The type of the command. |
|CreationTime|String|2020-01-19T09:15:46Z|The time when the task was created. |
|Frequency|String|0 \*/20 \* \* \* \*|The schedule on which the recurring execution of the command takes place. For more information about the value specifications, see [Cron expression](~~64769~~). |
|InvocationStatus|String|Running|The overall execution status of the command. The value of this parameter depends on the execution status on all the involved instances. Valid values:

-   Pending: The system is verifying or sending the command. When the execution status on at least one instance is Pending, the overall execution status is Pending.
-   Scheduled: The recurring command \(command that is to be run in a recurring manner\) was sent and waiting to be run. When the execution status on at least one instance is Scheduled, the overall execution status is Scheduled.
-   Running: The execution is in progress on the instances. When the execution status on at least one instance is Running, the overall execution status is Running.
-   Success: When the execution status on at least one instance is Success and the execution status on the other instances is Stopped, the overall execution status is Success.
    -   One-time execution: The execution is complete and the exit code is 0.
    -   Recurring execution: The last execution succeeds and the exit code is 0. The specified recurring period during which the command is run ends.
-   Failed: When the execution status on all instances is Stopped or Failed, the overall execution status is Failed. When the execution status on an instance is one of the following values, Failed is returned as the overall execution status:
    -   Invalid: The command is invalid.
    -   Aborted: The command fails to be sent.
    -   Failed: The execution is complete but the exit code is not 0.
    -   Timeout: The execution times out.
    -   Error: The execution is abnormal.
-   Stopping: The execution is being stopped. When the execution status on at least one instance is Stopping, the overall execution status is Stopping.
-   Stopped: The execution is stopped. When the execution status on all instances is Stopped, the overall execution status is Stopped. When the execution status on an instance is one of the following values, Stopped is returned as the overall execution status:
    -   Cancelled: The execution is canceled.
    -   Terminated: The execution is terminated.
-   PartialFailed: The execution succeeds on some instances and fails on some other instances. When the execution status is Success on some instances and is Failed or Stopped on the other instances, the overall execution status is PartialFailed.

**Note:** The `InvokeStatus` response parameter is similar to this parameter, but we recommend that you check the return value of this parameter. |
|InvokeId|String|t-hz0jdfwd9f\*\*\*\*|The ID of the execution. |
|InvokeInstances|Array of InvokeInstance| |Details of the instances on which the command is run. |
|InvokeInstance| | | |
|CreationTime|String|2019-12-20T06:15:54Z|The start time of the execution. |
|Dropped|Integer|0|The size of truncated and discarded text when the size of text in the Output response parameter is larger than 24 KB. |
|ErrorCode|String|InstanceNotExists|The code for the cause why a command failed to be sent or run. Valid values:

-   If this parameter is empty, the command is run normally.
-   InstanceNotExists: The instance does not exist or is released.
-   InstanceReleased: The instance is released while the command is being run.
-   InstanceNotRunning: The instance is not running when the command starts to be run.
-   CommandNotApplicable: The command is not applicable to the specified instance.
-   AccountNotExists: The specified account does not exist.
-   DirectoryNotExists: The specified directory does not exist.
-   BadCronExpression: The specified cron expression for the execution schedule is invalid.
-   ClientNotRunning: The Cloud Assistant client is not running.
-   ClientNotResponse: The Cloud Assistant client does not respond.
-   ClientIsUpgrading: The Cloud Assistant client is being upgraded.
-   ClientNeedUpgrade: The Cloud Assistant client needs to be upgraded.
-   DeliveryTimeout: The request times out.
-   ExecutionTimeout: The execution times out.
-   ExecutionException: An exception occurs when the command is being run.
-   ExecutionInterrupted: The execution is interrupted.
-   ExitCodeNonzero: The execution is complete but the exit code is not 0. |
|ErrorInfo|String|the specified instance does not exists|The details of the cause why the command failed to be sent or run. Valid values:

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
|ExitCode|Long|0|The exit code of the execution. Valid values:

-   For Linux instances, the exit code is the exit code of the shell process.
-   For Windows instances, the exit code is the exit code of the batch or PowerShell process. |
|FinishTime|String|2019-12-20T06:15:56Z|The end time of the execution. |
|InstanceId|String|i-bp1i7gg30r52z2em\*\*\*\*|The ID of the instance. |
|InstanceInvokeStatus|String|Finished|**Note:** We recommend that you ignore this parameter and check the return value of the `InvocationStatus` parameter for the overall execution status. |
|InvocationStatus|String|Success|The execution status on a single instance. Valid values:

-   Pending: The system is verifying or sending the command.
-   Invalid: The specified command type or parameter is invalid.
-   Aborted: The command fails to be sent. To send a command to an instance, make sure that the instance must be in the Running state and that the command can be sent within 1 minute.
-   Running: The command is running on the instance.
-   Success:
    -   One-time execution: The execution is complete and the exit code is 0.
    -   Recurring execution: The previous occurrence of the execution succeeds and the exit code is 0. The specified recurring period during which the command is run ends.
-   Failed:
    -   One-time execution: The execution is complete but the exit code is not 0.
    -   Recurring execution: The previous occurrence of the execution is complete and the exit code is not 0. The specified recurring period during which the command is run is about to end.
-   Error: The execution cannot proceed due to an exception.
-   Timeout: The execution times out.
-   Cancelled: The execution has been canceled and the command has not been started.
-   Stopping: The execution is being stopped.
-   Terminated: The command is terminated when it is being run.
-   Scheduled:
    -   One-time execution: not applicable.
    -   Recurring execution: The command is waiting to be run. |
|Output|String|OutPutTestmsg|The output of the command. |
|Repeats|Integer|0|The number of times that the command is run on the instance.

-   If the execution is a one-time execution, the value is 0 or 1.
-   If the execution is a recurring execution, the value is the number of times that the command is run. |
|StartTime|String|2019-12-20T06:15:55Z|The time when the command started to be run on the instance. |
|StopTime|String|2020-01-19T09:15:47Z|The time when the command stopped being run on the instance. If you called the `StopInvocation` operation to manually stop the execution, the value is the time when you call the operation. |
|Timed|Boolean|false|Indicates whether the command is to be automatically run. |
|UpdateTime|String|2020-01-19T09:15:47Z|The time when the execution status was updated. |
|InvokeStatus|String|Finished|The overall execution status of the command.

**Note:** We recommend that you ignore this parameter and check the return value of the `InvocationStatus` parameter for the overall execution status. |
|Parameters|String|\{\}|The custom parameters in the command. |
|RepeatMode|String|Once|Indicates the execution mode of the command. Valid values:

-   Once: The command is immediately run.
-   Period: The command is run on a regular basis.
-   NextRebootOnly: The command is automatically run the next time the instance starts.
-   EveryReboot: The command is automatically run every time the instance starts. |
|Timed|Boolean|false|Indicates whether the command is to be automatically run. |
|Username|String|root|The username that was used to run the command on the instance. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Long|1|The total number of commands. |

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
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <Invocations>
            <Invocation>
                  <InvocationStatus>Running</InvocationStatus>
                  <Parameters>{}</Parameters>
                  <Timed>false</Timed>
                  <InvokeInstances>
                        <InvokeInstance>
                              <Dropped>0</Dropped>
                              <InvocationStatus>Success</InvocationStatus>
                              <InstanceId>i-bp1i7gg30r52z2em****</InstanceId>
                              <Timed>false</Timed>
                              <InstanceInvokeStatus>Finished</InstanceInvokeStatus>
                              <ExitCode>0</ExitCode>
                              <ErrorInfo></ErrorInfo>
                              <StartTime>2019-12-20T06:15:55Z</StartTime>
                              <Repeats>0</Repeats>
                              <FinishTime>2019-12-20T06:15:56Z</FinishTime>
                              <Output>OutPutTestmsg</Output>
                              <CreationTime>2019-12-20T06:15:54Z</CreationTime>
                              <UpdateTime>2020-01-19T09:15:47Z</UpdateTime>
                              <ErrorCode></ErrorCode>
                              <StopTime>2020-01-19T09:15:47Z</StopTime>
                        </InvokeInstance>
                  </InvokeInstances>
                  <CommandContent>cnBtIC1xYSB8IGdyZXAgdnNm****</CommandContent>
                  <RepeatMode>Once</RepeatMode>
                  <InvokeStatus>Finished</InvokeStatus>
                  <CommandType>RunShellScript</CommandType>
                  <Username>root</Username>
                  <CreationTime>2020-01-19T09:15:46Z</CreationTime>
                  <Frequency></Frequency>
                  <CommandId>c-hz0jdfwcsr****</CommandId>
                  <CommandName>CommandTestName</CommandName>
                  <InvokeId>t-hz0jdfwd9f****</InvokeId>
            </Invocation>
      </Invocations>
</DescribeInvocationsResponse>
```

`JSON` format

```
{
  "TotalCount": 1,
  "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "PageSize": 10,
  "PageNumber": 1,
  "Invocations": {
    "Invocation": [
      {
        "InvocationStatus": "Running",
        "Parameters": "{}",
        "Timed": false,
        "InvokeInstances": {
          "InvokeInstance": [
            {
              "Dropped": 0,
              "InvocationStatus": "Success",
              "InstanceId": "i-bp1i7gg30r52z2em****",
              "Timed": false,
              "InstanceInvokeStatus": "Finished",
              "ExitCode": 0,
              "ErrorInfo": "",
              "StartTime": "2019-12-20T06:15:55Z",
              "Repeats": 0,
              "FinishTime": "2019-12-20T06:15:56Z",
              "Output": "OutPutTestmsg",
              "CreationTime": "2019-12-20T06:15:54Z",
              "UpdateTime": "2020-01-19T09:15:47Z",
              "ErrorCode": "",
              "StopTime": "2020-01-19T09:15:47Z"
            }
          ]
        },
        "CommandContent": "cnBtIC1xYSB8IGdyZXAgdnNm****",
        "RepeatMode": "Once",
        "InvokeStatus": "Finished",
        "CommandType": "RunShellScript",
        "Username": "root",
        "CreationTime": "2020-01-19T09:15:46Z",
        "Frequency": "",
        "CommandId": "c-hz0jdfwcsr****",
        "CommandName": "CommandTestName",
        "InvokeId": "t-hz0jdfwd9f****"
      }
    ]
  }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because this API operation cannot be called in the specified region. Check whether the specified RegionId parameter is valid.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

