# InvokeCommand

You can call this operation to trigger a Cloud Assistant command on one or more ECS instances.

## Description

-   You can call the InvokeCommand operation up to 5,000 times per day in a region. To adjust the maximum number of daily calls, [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).
-   The instances on which the command is to run must meet the following requirements. If multiple ECS instances are specified and one of the instances does not meet the execution conditions of the command, you must call the InvokeCommand operation again.
    -   The network type of the instances must be VPC. For more information, see [What is a VPC?](~~34217~~)
    -   The instances must be in the Running \(`Running`\) state.
    -   The instances must be pre-installed with the Cloud Assistant client. For more information, see [Install the Cloud Assistant client](~~64921~~).
    -   Before you run a PowerShell command, make sure that the instances on which you want to run the command are installed with the PowerShell module.
-   One-time execution \(`Timed` set to false\): The command is run only once.
-   Recurring execution \(`Timed` set to true\):
    -   The command is periodically run based on the value of `Frequency`. The result of each recurring execution does not affect the next execution.
    -   The time when recurring executions of the command take place on an ECS instance must be specified based on the system time of the instance in UTC. Make sure that the time or time zone of the ECS instance meets your business needs. For more information, see [Time setting: Synchronize NTP servers and change time zone for Linux instances](~~92803~~) or [Configure the NTP service for Windows instances](~~51890~~).
-   Commands may fail to be run because of the status exceptions of the ECS instances on which the commands are run, because of network exceptions, or because of the exceptions of the Cloud Assistant client. If an execution fails, no execution information is generated.
-   If you enable the custom parameter feature by setting EnableParameter to true when you create a command, you must specify custom parameters \(`Parameters`\) when you run the command.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=InvokeCommand&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|InvokeCommand|The operation that you want to perform. Set the value to InvokeCommand. |
|CommandId|String|Yes|c-e996287206324975b5fbe1d\*\*\*\*|The ID of the command. You can call the [DescribeCommands](~~64843~~) operation to query all available command IDs. |
|InstanceId.N|RepeatList|Yes|i-bp185dy2o3o6n\*\*\*\*|The ID of instance N on which to run the command. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Timed|Boolean|No|true|Specifies whether to periodically run the command.

 Default value: false. |
|Frequency|String|No|0 \*/20 \* \* \* \*|The time when recurring executions of the command take place. The interval between two consecutive recurring executions cannot be less than 10 seconds. When the `Timed` parameter is set to `true`, you must specify the `Frequency` parameter.

 Set the value of this parameter to a cron expression. For more information, see [Cron expression](~~64769~~). |
|Parameters|Json|No|\{"name":"Jack", "accessKey":"LTAIdyv\*\*\*\*\*\*aRY"\}|The key-value pairs of custom parameters to be passed in when the custom parameter feature is enabled. Number of custom parameters: 0 to 10.

 -   The key of a custom parameter cannot be an empty string. It can be up to 64 characters in length.
-   The value of a custom parameter can be an empty string.
-   After the custom parameters and the original command content are encoded in Base64, their total size cannot exceed 16 KB.
-   The set of custom parameter names must be a subset of the parameter set that is specified when you created the command. You can use empty strings to represent the parameters that are not passed in.

 You can leave this parameter empty to disable the custom parameter feature. |
|Username|String|No|root|The username that is used to run the command on the ECS instance.

 -   For Linux instances, the root username is used by default.
-   For Windows instances, the System username is used by default.

 You can also specify other usernames that already exist in the ECS instance to run the command. It is safer for you to run Cloud Assistant commands as a regular user. For more information, see [Configure a regular user to run Cloud Assistant commands](~~203771~~). |
|WindowsPasswordName|String|No|axtSecretPassword|The name of the password used to run the command on a Windows instance.

 If you want to use a username other than the default System username to run the command on the Windows instance, you must specify both this parameter and the `Username` parameter. The password is hosted in plaintext in the parameter repository of Operation Orchestration Service \(OOS\) to reduce the risk of password leaks. Only the name of the password is passed in by using this parameter. For more information, see [Encrypt parameters](~~186828~~) and [Configure a regular user to run Cloud Assistant commands](~~203771~~).

 **Note:** When you use the root username for Linux instances or the System username for Windows instances to run the command, you do not need to specify this parameter. |

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
&Username=root
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
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because the API operation cannot be called in the specified region. Check whether the RegionId parameter is correct.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred while the request was being sent. Try again later.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified instance does not exist.|
|403|InvalidInstance.NotMatch|The specified instance type does not match the command.|The error message returned because the specified command cannot be run on the specified ECS instance. Check whether the status of the instance meets the execution conditions of the command.|
|404|InvalidCmdId.NotFound|The specified command ID does not exist.|The error message returned because the specified CommandId parameter is invalid. You can call the DescribeCommands operation to query all available command IDs.|
|403|MissingParam.Frequency|The frequency must be specified when you create a timed task.|The error message returned because the Frequency parameter is not specified when you set Timed to true.|
|403|InvalidParam.Frequency|The specified frequency is invalid.|The error message returned because the specified Frequency parameter is invalid.|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|The error message returned because more than 50 ECS instance IDs are specified.|
|404|Parameter.Disabled|Parameters cannot be passed in when the command customization function is disabled.|The error message returned because you specify Parameters when the custom parameter feature is disabled.|
|403|ParameterCount.ExceedLimit|The maximum number of parameters is exceeded.|The error message returned because the number of specified custom parameters exceeds the upper limit.|
|403|ParameterKey.ExceedLimit|The maximum length of a parameter name is exceeded.|The error message returned because the key of a custom parameter exceeds 64 characters in length.|
|403|CmdContent.ExceedLimit|The maximum length of a command is exceeded.|The error message returned because the length of the command content exceeds the upper limit. Shorten your command.|
|403|ParameterKey.Duplicate|Parameter names cannot be duplicated.|The error message returned because a parameter that has the same name already exists. Parameter names must be unique.|
|403|Parameter.NotMatched|The passed-in parameters do not match the parameters defined when you created the command.|The error message returned because the custom parameters passed in do not match those specified when the command was created.|
|403|Username.ExceedLimit|The length of the username exceeds the upper limit.|The error message returned because the length of the username exceeds the upper limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

