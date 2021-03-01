# ModifyCommand

You can call this operation to modify the parameters and content of a Cloud Assistant command.

## Description

You can modify a command during its invocation. After the command is modified, the new command content applies to subsequent invocations.

You cannot modify the command type. For example, you cannot change a shell command \(RunShellScript\) to a batch command \(RunBatScript\).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyCommand|The operation that you want to perform. Set the value to ModifyCommand. |
|CommandId|String|Yes|c-4d34302d02424c5c8e10281e3a31\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Name|String|No|AlibabaCommand|The name of the command, which supports all character sets. The name can be up to 30 characters in length. |
|Description|String|No|UserGuide|The description of the command, which supports all character sets. The description can be up to 100 characters in length. |
|CommandContent|String|No|c2VydmljZSB0b21jYXQgc3RhcnQ=|The content of the command. |
|WorkingDir|String|No|/home/|The directory path for command invocation. |
|Timeout|Long|No|120|The timeout period. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyCommand
&CommandId=c-4d34302d02424c5c8e10281e3a31****
&RegionId=cn-hangzhou
&Name=AlibabaCommand
&Description=UserGuide
&CommandContent=c2VydmljZSB0b21jYXQgc3RhcnQ=
&WorkingDir=/home/
&Timeout=120
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyCommandResponse>
      <RequestId>0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C</RequestId>
</ModifyCommandResponse>
```

`JSON` format

```
{
    "RequestId": "0DE9B41E-EF0D-40A0-BB43-37749C5BDA9C"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidCmdType.NotFound|The specified command type does not exist.|The error message returned because the specified command type does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

