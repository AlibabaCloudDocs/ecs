# RunCommand

You can call this operation to run a shell, PowerShell, or bat command on one or more instances.

## Description

Different from [CreateCommand](~~64844~~) and [InvokeCommand](~~64841~~), RunCommand can be used to create and run a command within a single request.

When you call this operation, take note of the following items:

-   The instance on which you want to run a command must be a VPC-type instance.
-   The instance must be in the Running \(`Running`\) state.
-   The instance must be pre-installed with the Cloud Assistant client \([InstallCloudAssistant](~~85916~~)\).
-   Before you run a PowerShell command, make sure that the Windows instance on which you want to run the command is installed with the PowerShell module.
-   The period of recurring tasks is set based on UTC and the system time of the instance. The time or time zone of the ECS instance must meet your business needs. For more information about time zones, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Configure the NTP service for Windows instances](~~51890~~).
-   You can specify the `TimeOut` parameter to set the maximum timeout period of a command execution on an instance. After a command execution times out, Cloud Assistant forcibly stops the process.
    -   After a single command execution times out, the execution state \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed.
    -   Each record of timeout period of recurring tasks is valid. The timeout of the previous task does not affect the next task. After an execution task times out, the execution state \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed.
-   Commands may fail to be run because of the status exceptions of the instances on which commands are run, network exceptions, or the exceptions of the Cloud Assistant client. If an execution task fails, no execution information is generated.
-   When `EnableParameter` is set to true, the custom parameter feature is enabled. When you set the `CommandContent` parameter, you can specify custom parameters in the `{{parameter}}` format. Then, you can pass in these custom parameters in the key-value pair format when you run the command.
-   In a region, you can retain a maximum of 100 to 10,000 Cloud Assistant commands and run a maximum of 2,000 to 200,000 Cloud Assistant commands every day based on your ECS usage. You can call the [DescribeAccountAttribute](~~73772~~) operation to query quotas. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to modify the maximum number of Cloud Assistant commands that you can retain and the maximum number of calls every day.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RunCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RunCommand|The operation that you want to perform. Set the value to RunCommand. |
|CommandContent|String|Yes|ZWNobyAxMjM=|The plaintext or Base64-encoded content of the command. The Base64-encoded command content cannot exceed 16 KB in size.

When `EnableParameter` is set to true, the custom parameter feature is enabled:

-   Define custom parameters in the `{{}}` format. Within `{{}}`, the spaces and line breaks before and after the parameter names are ignored.
-   The number of custom parameters cannot exceed 20.
-   A custom parameter name can contain only letters, digits, underscores \(\_\), and hyphens \(-\). The name is case-insensitive.

Each custom parameter key cannot exceed 64 bytes. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6neg\*\*\*\*|The ID of instance N. Valid values of N: 1 to 50.

If multiple instances are specified and one of them does not meet the execution conditions, you must re-specify the IDs of all the instances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Type|String|Yes|RunShellScript|The language type of the O&M command. Valid values:

-   RunBatScript: batch commands for Windows instances
-   RunPowerShellScript: PowerShell commands for Windows instances
-   RunShellScript: shell commands for Linux instances |
|Name|String|No|testName|The name of the command. The name supports all character sets. It cannot exceed 128 characters in length. |
|Description|String|No|testDescription|The description of the command. The description supports all character sets. It cannot exceed 512 characters in length. |
|WorkingDir|String|No|/home/|The working directory of the command in the ECS instance.

Default value:

-   Linux instances: the home directory of the administrator, which is `/root`.
-   Windows instances: the directory where the Cloud Assistant client process resides, such as `C:\Windows\System32\`. |
|Timeout|Long|No|3600|The timeout period for command execution. Unit: seconds.

A timeout error occurs when a command cannot be run because the process slows down, a specific module or the Cloud Assistant client does not exist. When the command times out, the command process is forcibly terminated.

Default value: 60. |
|EnableParameter|Boolean|No|false|Specifies whether to contain custom parameters in the command.

Default value: false. |
|Timed|Boolean|No|true|Specifies whether to periodically run the command. Valid values:

-   true: runs the command on a regular basis based on the value set for the `Frequency` parameter. The result of the previous execution task does not affect the next execution task.
-   false: runs once only.

Default value: false. |
|Frequency|String|No|0 \*/20 \* \* \* \*|The execution period of recurring tasks. If the Timed parameter is set to true, you must specify the Frequency parameter. The interval between two recurring tasks cannot be less than 10 seconds.

The parameter value follows the cron expression. For more information, see [Cron expression](~~64769~~). |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyvdIqaRY\*\*\*\*"\}|The key-value pairs of custom parameters that are passed in when the command contains custom parameters. For example, if the command content is `echo {{name}}`, the `Parameters` parameter can be used to pass in the `{"name":"Jack"}` key-value pair. The `name` variable value of the custom parameter is automatically replaced to generate a new command. Therefore, the `echo Jack` command is actually run.

Number of custom parameters: 0 to 10.

-   The key cannot be an empty string. It can be up to 64 characters in length.
-   The value can be an empty string.
-   After the custom parameters and the original command content are Base64 encoded, the total size cannot exceed 16 KB.
-   The set of custom parameter names must be a subset of the parameter set that is defined when you created the command. You can use an empty string to represent the parameters that are not passed in.

This parameter is empty by default. This indicates that this parameter is canceled and customer parameters are disabled. |
|KeepCommand|Boolean|No|false|Specifies whether to retain the command after it is run. Valid values:

-   true: The command is retained. You can call the InvokeCommand operation to run the command again. The retained command takes up the quota of Cloud Assistant commands.
-   false: The command is not retained. The command is automatically deleted after it is run and it does not take up the quota of Cloud Assistant commands.

Default value: false. |
|ContentEncoding|String|No|Base64|The encoding mode of command content \(`CommandContent`\). Valid values \(case-insensitive\):

-   PlainText: The command content is not encoded, and is transmitted in plaintext.
-   Base64: The command content is Base64-encoded.

Default value: PlainText. If the specified value of this parameter is invalid, PlainText is used by default. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the command. |
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of command execution. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
http(s)://ecs.aliyuncs.com/? Action=RunCommand
&CommandContent='echo hello'
&InstanceId.1=i-bp185dy2o3o6neg****
&Name=test
&RegionId=cn-hangzhou
&Type=RunShellScript
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RunCommandResponse>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
        <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
        <InvokeId>t-7d2a745b412b4601b2d47f6a768d****</InvokeId>
</RunCommandResponse>
```

`JSON` format

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "CommandId": "c-7d2a745b412b4601b2d47f6a768d****",
    "InvokeId": "t-7d2a745b412b4601b2d47f6a768d****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned because the specified Type parameter does not exist.|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|The error message returned because the maximum length of the command name has been reached.|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|The error message returned because the maximum length of the command description has been reached.|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|The error message returned because the maximum number of Cloud Assistant commands in the current region has been reached.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified instance does not exist.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned because the Frequency parameter is not specified when you create a scheduled task.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

