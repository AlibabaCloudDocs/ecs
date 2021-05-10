# RunCommand

You can call this operation to run a shell, PowerShell, or batch command on one or more Elastic Compute Service \(ECS\) instances.

## Description

Different from [CreateCommand](~~64844~~) and [InvokeCommand](~~64841~~), RunCommand can be used to create and run a command within a single request.

When you call this operation, take note of the following items:

-   The ECS instance on which you want to run a command must be a VPC-type instance.
-   The instance must be in the Running \(`Running`\) state.
-   The instance must be pre-installed with the Cloud Assistant client \([InstallCloudAssistant](~~85916~~)\).
-   Before you run a PowerShell command, make sure that the Windows instance on which you want to run the command is installed with the PowerShell module.
-   The schedule on which a recurring execution of the command takes place on an ECS instance must be specified based on the system time of the instance in UTC. Make sure that the time or time zone of the ECS instance meets your business needs. For more information, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Configure the NTP service for Windows instances](~~51890~~).
-   You can specify the `TimeOut` parameter to set the timeout period for the command execution on an instance. When the execution times out, Cloud Assistant forcibly stops the process.
    -   After a one-time execution times out, the execution status \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed.
    -   For a recurring execution, the timeout period takes effect on each occurrence of the execution. The timeout of each occurrence does not affect the next occurrence. After an occurrence times out, the execution status \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed.
-   The executions of commands may fail because of the status exceptions on the ECS instances on which the commands are run, because of network exceptions, or because of the exceptions on the Cloud Assistant client. If an execution fails, no execution information is generated.
-   When `EnableParameter` is set to true, the custom parameter feature is enabled. When you specify the `CommandContent` parameter, you can specify custom parameters in the `{{parameter}}` format. Then, you can pass in these custom parameters in the key-value pair format when you run the command.
-   In a single region, you can retain a maximum of 100 to 10,000 Cloud Assistant commands and run a maximum of 2,000 to 200,000 Cloud Assistant commands every day. These numbers are determined based on your ECS usage. You can call the[DescribeAccountAttribute](~~73772~~) operation to query quotas. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to modify the maximum number of Cloud Assistant commands that you can retain and the maximum number of Cloud Assistant commands that you can run every day.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RunCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RunCommand|The operation that you want to perform. Set the value to RunCommand. |
|CommandContent|String|Yes|ZWNobyAxMjM=|The plaintext or Base64-encoded content of the command. The Base64-encoded command content cannot exceed 16 KB in size.

When `EnableParameter` is set to true, the custom parameter feature is enabled and you can configure custom parameters based on the following rules:

-   Define custom parameters in the `{{}}` format. Within `{{}}`, the spaces and line breaks before and after the parameter names are ignored.
-   The number of custom parameters cannot exceed 20.
-   A custom parameter name can contain only letters, digits, underscores \(\_\), and hyphens \(-\). The name is case-insensitive.

Each custom parameter key cannot exceed 64 bytes in length. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6neg\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 50.

If multiple instances are specified and one of them does not meet the conditions for running the command, you must re-specify the ID of the ECS instance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Type|String|Yes|RunShellScript|The language type of the command. Valid values:

-   RunBatScript: batch command, applicable to Windows instances
-   RunPowerShellScript: PowerShell command, applicable to Windows instances
-   RunShellScript: shell command, applicable to Linux instances |
|Name|String|No|testName|The name of the command. The name supports all character sets and can be up to 128 characters in length. |
|Description|String|No|testDescription|The description of the command. The description supports all character sets and can be up to 512 characters in length. |
|WorkingDir|String|No|/home/|The working directory of the command on the ECS instance.

Default value:

-   Linux instances: the home directory of the administrator, which is `/root`.
-   Windows instances: the directory where the Cloud Assistant client process resides, such as `C:\Windows\System32`. |
|Timeout|Long|No|3600|The timeout period for the execution of a command. Unit: seconds.

A timeout error occurs when a command cannot be run because the process slows down or because a specific module or the Cloud Assistant client does not exist. When the execution times out, the command process is forcibly terminated.

Default value: 60. |
|EnableParameter|Boolean|No|false|Specifies whether to include custom parameters in the command.

Default value: false. |
|RepeatMode|String|No|Once|Specifies the execution mode of the command. Valid values:

-   Once: The command is immediately run.
-   Period: The command is run on a regular basis. If you set this parameter to `Period`, you must set `Timed` to true and specify `Frequency`.
-   NextRebootOnly: The command is automatically run the next time the instance starts.
-   EveryReboot: The command is automatically run every time the instance starts.

Default value:

-   When `Timed` is not set to true and `Frequency` is not specified, the default value of RepeatMode is `Once`.
-   When `Timed` is set to true and `Frequency` is specified, `Period` is used as the value of RepeatMode regardless of whether RepeatMode is specified.

Precautions:

-   When this parameter is set to `Period`, `NextRebootOnly`, or `EveryReboot`, you can call the [StopInvocation](~~64838~~) operation to stop the pending or recurring execution of the command.
-   When this parameter is set to `Period` or `EveryReboot`, you can call the [DescribeInvocationResults](~~64845~~) operation and set `IncludeHistory` to true to view the historical results of the recurring execution. |
|Timed|Boolean|No|true|Specifies whether to periodically run the command. Valid values:

-   true: periodically runs the command on the schedule specified by `Frequency`. The results of each occurrence of the command execution do not affect the next occurrence.
-   false: runs the command only once.

Default value: false. |
|Frequency|String|No|0 \*/20 \* \* \* \*|The schedule on which the recurring execution of the command takes place. You must specify this parameter when you set `Timed` to `true`. The interval between two consecutive occurrences of the recurring execution must not be less than 10 seconds.

Set the value of this parameter to a cron expression. For more information, see [Cron expression](~~64769~~). |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyvdIqaRY\*\*\*\*"\}|The key-value pairs of custom parameters to be passed in when the command contains custom parameters. For example, if the command content is `echo {{name}}`, the `Parameters` parameter can be used to pass in the `{"name":"Jack"}` key-value pair. The custom parameter automatically replaces the `name` value in the command to generate a new command. Therefore, the `echo Jack` command is run.

Number of custom parameters: 0 to 10.

-   The key cannot be an empty string. It can be up to 64 characters in length.
-   The value can be an empty string.
-   After the custom parameters and the original command content are encoded in Base64, their total size cannot exceed 16 KB.
-   The custom parameter names specified in the value of Parameters must all be included in the custom parameters specified when you created the command. You can use empty strings to represent the parameters that are not passed in.

This parameter is empty by default. This indicates that this parameter is canceled and the custom parameter feature is disabled. |
|KeepCommand|Boolean|No|false|Specifies whether to retain the command after it is run. Valid values:

-   true: retains the command. You can call the InvokeCommand operation to run the command again. The retained command counts against the quota of Cloud Assistant commands.
-   false: does not retain the command. The command is automatically deleted after it is run, and does not count against the quota of Cloud Assistant commands.

Default value: false. |
|ContentEncoding|String|No|Base64|The encoding mode of command content \(`CommandContent`\). The valid values are case-insensitive. Valid values:

-   PlainText: does not encode the command content.
-   Base64: encodes the command content in Base64.

Default value: PlainText. If the specified value of this parameter is invalid, PlainText is used by default. |
|Username|String|No|root|The username that is used to run the command on the ECS instance.

-   For Linux instances, the root username is used by default.
-   For Windows instances, the System username is used by default.

You can also specify other usernames that already exist in the ECS instance to run the command. It is safer for you to run Cloud Assistant commands as a regular user. For more information, see [Configure a regular user to run Cloud Assistant commands](~~203771~~). |
|WindowsPasswordName|String|No|axtSecretPassword|The name of the password used to run the command on a Windows instance.

If you want to use a username other than the default System username to run the command on the Windows instance, you must specify both the WindowsPasswordName and `Username` parameters. The password is hosted in plaintext in the parameter repository of Operation Orchestration Service \(OOS\) to reduce the risk of password leaks. Only the name of the password is passed in by using the WindowsPasswordName parameter.

**Note:** When you use the root username for Linux instances or the System username for Windows instances to run the command, you do not need to specify this parameter. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the command. |
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the execution. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
http(s)://ecs.aliyuncs.com/?Action=RunCommand
&CommandContent='echo hello'
&InstanceId.1=i-bp185dy2o3o6neg****
&Name=Test
&RegionId=cn-hangzhou
&Type=RunShellScript
&Username=root
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
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because this API operation cannot be called in the specified region. Check whether the specified RegionId parameter is valid.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned because the specified Type parameter does not exist.|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|The error message returned because the command name exceeds 128 characters in length.|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|The error message returned because the command description exceeds 512 characters in length.|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|The error message returned because the maximum number of Cloud Assistant commands in the current region has been reached.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified ECS instance does not exist.|
|403|InvalidInstance.NotMatch|The specified instance type does not match the command.|The error message returned because the specified command cannot be run on the specified ECS instance. Check whether the status of the instance meets the conditions for running the command.|
|404|InvalidCmdId.NotFound|The specified command ID does not exist.|The error message returned because the specified CommandId parameter is invalid. You can call the DescribeCommands operation to query all available command IDs.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned because the Frequency parameter is not specified when you set Timed to true.|
|403|InvalidParam.Frequency|The specified frequency is invalid.|The error message returned because the specified Frequency parameter is invalid.|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|The error message returned because more than 50 ECS instance IDs are specified.|
|403|Username.ExceedLimit|The length of the username exceeds the upper limit.|The error message returned because the length of the username exceeds the upper limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

