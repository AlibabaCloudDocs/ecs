# InvokeCommand

You can call this operation to trigger a Cloud Assistant command on one or more ECS instances.

## Description

-   You can call the InvokeCommand operation up to 5,000 times a day in a region. To adjust the maximum number of daily calls, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).
-   The following list describes requirements on the instances on which the command is run. After multiple ECS instances are selected, if one of the instances does not meet the execution conditions, you must call the InvokeCommand operation again.
    -   The network type must be VPC. For more information, see [What is a VPC?](~~34217~~)
    -   The instances must be in the Running \(`Running`\) state.
    -   The instances must be pre-installed with the Cloud Assistant client. For more information, see [Install the Cloud Assistant client](~~64921~~).
    -   Before you run PowerShell commands, make sure that the instances have the PowerShell module configured.
-   One-time invocation \(`Timed=false`\): The Cloud Assistant client runs the command only once.
-   Scheduled invocation \(`Timed=true`\):
    -   The Cloud Assistant client runs the command at the frequency specified by the `Frequency` parameter. The result of previous execution does not affect the current execution.
    -   The period of scheduled invocation is set based on UTC and the system time of the instances. If the system time of your ECS instances are not based on UTC, make sure that you have made adjustments to ensure that your commands are run at the correct time. For more information, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Configure the NTP service for Windows instances](~~51890~~).
-   Command executions may fail due to exceptions on instance status, network, or the Cloud Assistant client. If an execution fails, no execution information is generated.
-   If you enable the custom parameter feature by setting EnableParameter to true when you create a command, you must specify the value of the custom parameter \(`Parameters`\) when you run the command.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=InvokeCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|InvokeCommand|The operation that you want to perform. Set the value to InvokeCommand. |
|CommandId|String|Yes|c-e996287206324975b5fbe1d\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6n\*\*\*\*|The ID of instance N on which the command is to be run. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Timed|Boolean|No|true|Specifies whether to run the command on a scheduled basis.

Default value: false. |
|Frequency|String|No|0 \*/20 \* \* \* \*|The interval at which the command is executed on a scheduled basis. The interval between two consecutive executions cannot be less than 10 seconds. When the `Timed` parameter is set to `true`, you must specify the `Frequency` parameter.

The value of this parameter is expressed in cron. For more information, see [Cron expression](~~64769~~). |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyv\*\*\*\*\*\*aRY"\}|Specifies the values of the custom parameters when the custom parameter feature is enabled. The values are key-value pairs. Number of custom parameters: 0 to 10.

-   The key of a custom parameter cannot be an empty string. It can be up to 64 characters in length.
-   The value of a custom parameter can be an empty string.
-   After the custom parameters and the original command content are Base64 encoded, the total size cannot exceed 16 KB.
-   The set of custom parameter names must be a subset of the parameter set that is specified when you created the command. You can use empty strings to represent the parameters that are not passed in.

You can leave this parameter empty to disable the custom parameter feature. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InvokeId|String|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the execution. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=InvokeCommand
&CommandId=c-e996287206324975b5fbe1d****
&InstanceId.1=i-bp185dy2o3o6n****
&RegionId=cn-hangzhou
&Timed=true
&Frequency=0 */20 * * * *
&Parameters={"name":"Jack", "accessKey":"LTAIdyv******aRY"}
&<Common request parameters>
```

Sample success responses

`XML` format

```
<InvokeCommandResponse>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <InvokeId>t-7d2a745b412b4601b2d47f6a768d****</InvokeId>
</InvokeCommandResponse>
```

`JSON` format

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "InvokeId": "t-7d2a745b412b4601b2d47f6a768d****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified instance does not exist.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned because the Frequency parameter is not specified when you set Timed to true.|
|404|Parameter.Disabled|Parameters cannot be passed in when the command customization function is disabled.|The error message returned because you specify Parameters when you disable the custom parameter feature.|
|403|ParameterCount.ExceedLimit|The maximum number of parameters is exceeded.|The error message returned because the maximum number of custom parameters has been reached.|
|403|ParameterKey.ExceedLimit|The maximum length of a parameter name is exceeded.|The error message returned because the maximum length of the key of a custom parameter has been reached.|
|403|CmdContent.ExceedLimit|The maximum length of a command is exceeded.|The error message returned because the maximum length of the command content has been reached. Simplify your command.|
|403|ParameterKey.Duplicate|Parameter names cannot be duplicated.|The error message returned because a parameter that has the same name already exists. Parameter names must be unique.|
|403|Parameter.NotMatched|The passed-in parameters do not match the parameters defined when you created the command.|The error message returned because the custom parameters passed in do not match those specified when the command was being created.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

