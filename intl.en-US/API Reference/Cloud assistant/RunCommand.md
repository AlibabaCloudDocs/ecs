# RunCommand

You can call this operation to run a shell, PowerShell, or batch command on one or more ECS instances.

## Description

Different from [CreateCommand](~~64844~~) and [InvokeCommand](~~64841~~), RunCommand can be used to create and run a command within a single request.

When you call this operation, take note of the following items:

-   The ECS instances for which you want to call this operation must be VPC-type instances.
-   The ECS instances must be in the Running \(`Running`\) state.
-   The ECS instances must be pre-installed with the Cloud Assistant client \([InstallCloudAssistant](~~85916~~)\).
-   Before you run a PowerShell command, make sure that the Windows instances on which you want to run the command are installed with the PowerShell module.
-   The time when recurring executions of the command take place on an ECS instance must be specified based on the system time of the instance in UTC. The time or time zone of the ECS instance must meet your business needs. For more information about time zones, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Configure the NTP service for Windows instances](~~51890~~).
-   You can specify the `Timeout` parameter to set the timeout period for executions of the command on an ECS instance. When an execution times out, Cloud Assistant forcibly stops the command process.
    -   If the command is configured to run on the specified instances only once, the execution state \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed after the one-time execution times out.
    -   If the command is configured to periodically run on the specified instances, the specified timeout period takes effect for each recurring execution of the command. The timeout of each recurring execution does not affect the next execution. After a recurring execution times out, the execution state \([InvokeRecordStatus](~~64845~~)\) of the command becomes Failed.
-   Commands may fail to be run because of the status exceptions of the ECS instances on which the commands are run, because of network exceptions, or because of the exceptions of the Cloud Assistant client. If an execution fails, no execution information is generated.
-   When `EnableParameter` is set to true, the custom parameter feature is enabled. When you set the `CommandContent` parameter, you can specify custom parameters in the `{{parameter}}` format. Then, you can pass in these custom parameters in the key-value pair format when you run the command.
-   In a single region, you can retain a maximum of 100 to 10,000 Cloud Assistant commands and run a maximum of 2,000 to 200,000 Cloud Assistant commands every day based on your ECS usage. You can call the [DescribeAccountAttribute](~~73772~~) operation to query quotas. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to modify the maximum number of Cloud Assistant commands that you can retain and the maximum number of Cloud Assistant commands that you can run every day.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RunCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RunCommand|The operation that you want to perform. Set the value to RunCommand. |
|CommandContent|String|Yes|ZWNobyAxMjM=|The plaintext or Base64-encoded content of the command. The Base64-encoded command content cannot exceed 16 KB in size.

When `EnableParameter` is set to true, the custom parameter feature is enabled. You can configure custom parameters based on the following rules:

-   Define custom parameters in the `{{}}` format. Within `{{}}`, the spaces and line breaks before and after the parameter names are ignored.
-   The number of custom parameters cannot exceed 20.
-   A custom parameter name can contain letters, digits, underscores \(\_\), and hyphens \(-\). The name is case-insensitive.

Each custom parameter key cannot exceed 64 bytes in size. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6neg\*\*\*\*|The ID of ECS instance N. Valid values of N: 1 to 50.

If multiple ECS instances are specified and one of them does not meet the execution conditions of the command, you must re-specify the ID of the ECS instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the ECS instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
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
|Timeout|Long|No|3600|The timeout period for command executions. Unit: seconds.

A timeout error occurs when a command cannot be run because the process slows down or because a specific module or the Cloud Assistant client does not exist. When an execution times out, the command process is forcibly terminated.

Default value: 60. |
|EnableParameter|Boolean|No|false|Specifies whether to include custom parameters in the command.

Default value: false. |
|Timed|Boolean|No|true|Specifies whether to periodically run the command. Valid values:

-   true: periodically runs the command based on the value of `Frequency`. The result of each execution does not affect the next execution.
-   false: runs the command only once.

Default value: false. |
|Frequency|String|No|0 \*/20 \* \* \* \*|The time when recurring executions of the command take place. When the Timed parameter is set to true, you must specify the Frequency parameter. The interval between two consecutive recurring executions cannot be less than 10 seconds.

Set the value of this parameter to a cron expression. For more information, see [Cron expression](~~64769~~). |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyvdIqaRY\*\*\*\*"\}|The key-value pairs of custom parameters to be passed in when the command contains custom parameters. For example, if the command content is `echo {{name}}`, the `Parameters` parameter can be used to pass in the `{"name":"Jack"}` key-value pair. The `name` value of the custom parameter is automatically replaced to generate a new command. Therefore, the `echo Jack` command is actually run.

Number of custom parameters: 0 to 10.

-   The key cannot be an empty string. It can be up to 64 characters in length.
-   The value can be an empty string.
-   After the custom parameters and the original command content are encoded in Base64, their total size cannot exceed 16 KB.
-   The set of custom parameter names must be a subset of the parameter set that is specified when you created the command. You can use empty strings to represent the parameters that are not passed in.

This parameter is empty by default. This indicates that this parameter is canceled and the custom parameter feature is disabled. |
|KeepCommand|Boolean|No|false|Specifies whether to retain the command after it is run. Valid values:

-   true: retains the command. You can call the InvokeCommand operation to run the command again. The retained command counts against the quota of Cloud Assistant commands.
-   false: does not retain the command. The command is automatically deleted after it is run, and does not count against the quota of Cloud Assistant commands.

Default value: false. |
|ContentEncoding|String|No|Base64|The encoding mode of command content \(`CommandContent`\). Valid values \(case-insensitive\):

-   PlainText: does not encode the command content and transmits it in plaintext.
-   Base64: encodes the command in Base64.

Default value: PlainText. If the specified value of this parameter is invalid, PlainText is used by default. |
|Username|String|No|root|The username that is used to run the command on the ECS instance.

-   For Linux instances, the root username is used by default.
-   For Windows instances, the System username is used by default.

You can also specify other usernames that already exist in the ECS instance to run the command. It is safer for you to run Cloud Assistant commands as a regular user. |
|WindowsPasswordName|String|No|axtSecretPassword|The name of the password used to run the command on a Windows instance.

If you want to use a username other than the default System username to run the command on the Windows instance, you must specify both this parameter and the `Username` parameter. The password is hosted in plaintext in the parameter repository of Operation Orchestration Service \(OOS\) to reduce the risk of password leaks. Only the name of the password is passed in by using this parameter.

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
http(s)://ecs.aliyuncs.com/? Action=RunCommand
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
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because the API operation cannot be called in the specified region. Check whether the RegionId parameter is correct.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned because the specified Type parameter does not exist.|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|The error message returned because the command name exceeds 128 characters in length.|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|The error message returned because the command description exceeds 512 characters in length.|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|The error message returned because the maximum number of Cloud Assistant commands in the current region has been reached.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified ECS instance does not exist.|
|403|InvalidInstance.NotMatch|The specified instance type does not match the command.|The error message returned because the specified command cannot be run on the specified ECS instance. Check whether the status of the instance meets the execution conditions of the command.|
|404|InvalidCmdId.NotFound|The specified command ID does not exist.|The error message returned because the specified CommandId parameter is invalid. You can call the DescribeCommands operation to query all available command IDs.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned because the Frequency parameter is not specified when you set Timed to true.|
|403|InvalidParam.Frequency|The specified frequency is invalid.|The error message returned because the specified Frequency parameter is invalid.|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|The error message returned because more than 50 ECS instance IDs are specified.|
|403|Username.ExceedLimit|The length of the username exceeds the upper limit.|The error message returned because the length of the username exceeds the upper limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

