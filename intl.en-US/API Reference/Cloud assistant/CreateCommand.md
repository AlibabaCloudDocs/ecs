# CreateCommand

You can call this operation to create a Cloud Assistant command.

## Description

-   You can create commands of the following types:
    -   RunBatScript: bat commands for Windows instances
    -   RunPowerShellScript: PowerShell commands for Windows instances
    -   RunShellScript: shell commands for Linux instances
-   You can specify the TimeOut parameter to set the maximum timeout period for command executions on ECS instances. When a command execution times out, the Cloud Assistant client forces the execution to stop by canceling the process ID \(PID\) of the command. For more information, see [Install the Cloud Assistant client](~~64921~~).
    -   One-time invocation: After an execution times out, the state of the execution \([InvokeRecordStatus](~~64845~~)\) on the specified ECS instance becomes Failed.
    -   Scheduled invocation:
        -   The timeout period of a scheduled invocation command is effective for every execution record.
        -   After an execution times out, the status of the execution \([InvokeRecordStatus](~~64845~~)\) becomes Failed.
        -   The timeout of previous execution does not affect the current execution.
-   You can create up to 100 Cloud Assistant commands in a region. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to increase the service quota.
-   You can use the WorkingDir parameter to specify the execution path of the command. For Linux instances, the default execution path of the command is the home directory of the root user, which is `/root`. For Windows instances, the default execution path of the command is the directory where the Cloud Assistant client process resides, such as C:\\Windows\\System32.
-   You can enable the custom parameter feature on a Cloud Assistant command by setting EnableParameter to true when you create the command. When you set the CommandContent parameter, you can use the \{\{parameter\}\} format to indicate a custom parameter. Then, when you call the [InvokeCommand](~~64841~~) operation, you can enter the key-value pair of the custom parameter. For example, assume that you create a command named `echo {{name}}`. When you call the InvokeCommand operation, you can set Parameters to `<name, Jack>`. The custom parameter automatically changes the command to a new one. Therefore, the `echo Jack` command is actually run on the instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCommand|The operation that you want to perform. Set the value to CreateCommand. |
|CommandContent|String|Yes|ZWNobyAxMjM=|The Base64-encoded content of the command.

-   The parameter value must be Base64-encoded and cannot exceed 16 KB in size after encoding.
-   The command content can be specified by using custom parameters. To enable the custom parameters feature, you must set `EnableParameter` to true.
    -   Custom parameters must be specified in the `{{}}` format. Within `{{}}`, the spaces and line feeds before and after the parameter names are ignored.
    -   The number of custom parameters cannot exceed 20.
    -   A custom parameter name can contain only letters, digits, underscores \(\_\), and hyphens \(-\). It is case-insensitive.
    -   Each custom parameter name cannot exceed 64 bytes. |
|Name|String|Yes|testName|The name of the command, which supports all character sets. It can be up to 128 characters in length. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Type|String|Yes|RunShellScript|The command type. Valid values:

-   RunBatScript: bat commands for Windows instances.
-   RunPowerShellScript: PowerShell commands for Windows instances.
-   RunShellScript: shell commands for Linux instances. |
|Description|String|No|testDescription|The description of the command, which supports all character sets. It can be up to 512 characters in length. |
|WorkingDir|String|No|/root/|The execution path of the command in the ECS instance.

Default value:

-   For Linux instances, the default value is the home directory of the root user, which is the `/root` directory.
-   For Windows instances, the default value is the directory where the Cloud Assistant client process resides, such as `C:\Windows\System32`. |
|Timeout|Long|No|60|The timeout period that is specified for the command to be run on ECS instances. Unit: seconds. When a command that you created cannot be run, the command times out. When a command execution times out, the Cloud Assistant client forces the command process to stop by canceling the PID of the command.

Default value: 60. |
|EnableParameter|Boolean|No|false|Specifies whether to use custom parameters in the command to be created.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CommandId|String|c-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the command. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateCommand
&CommandContent=ZWNobyB7e25hbWV9fSA=
&Name=testName
&RegionId=cn-hangzhou
&Type=RunShellScript
&Description=testDescription
&WorkingDir=/root/
&Timeout=60
&EnableParameter=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateCommandResponse>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d****</CommandId>
</CreateCommandResponse>
```

`JSON` format

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "CommandId": "c-7d2a745b412b4601b2d47f6a768d****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|403|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned because the specified Type parameter does not exist.|
|403|CmdName.ExceedLimit|The length of the command name exceeds the upper limit.|The error message returned because the maximum length of the command name has been reached.|
|403|CmdDesc.ExceedLimit|The length of the command description exceeds the upper limit.|The error message returned because the maximum length of the command description has been reached.|
|403|CmdCount.ExceedQuota|The total number of commands in the current region exceeds the quota.|The error message returned because the maximum number of Cloud Assistant commands in the current region has been reached.|
|403|CmdParam.EmptyKey|You must specify the parameter names.|The error message returned because some required parameters are not specified.|
|403|CmdParam.InvalidParamName|Invalid parameter name. The name can contain only lowercase letters \(a to z\), uppercase letters \(A to Z\), numbers \(0 to 9\), hyphens \(-\), and underscores \(\_\).|The error message returned because the custom parameter name is invalid. A custom parameter name can contain only letters, digits, underscores \(\_\), and hyphens \(-\).|
|403|CmdParamName.ExceedLimit|The maximum length of a parameter name is exceeded.|The error message returned because the maximum length of the custom parameter name has been reached.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

