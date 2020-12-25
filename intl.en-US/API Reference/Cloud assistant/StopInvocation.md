# StopInvocation

You can call this operation to stop a Cloud Assistant command that is running on one or more instances.

## Description

-   If you stop the process of a one-time invocation command, the executions that have started are not interrupted. The executions that have not started are canceled.
-   If you stop the process of a scheduled invocation command, the executions that have started are not interrupted. However, the execution does not start in the next period.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=StopInvocation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StopInvocation|The operation that you want to perform. Set the value to StopInvocation. |
|InvokeId|String|Yes|t-7d2a745b412b4601b2d47f6a768d\*\*\*\*|The ID of the execution. You can call the [DescribeInvocations](~~64840~~) operation to query all execution IDs. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the command. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId.N|RepeatList|No|i-bp67acfmxazb4p\*\*\*\*|The ID of instance N on which the command to be stopped is running. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=StopInvocation
&InvokeId=t-7d2a745b412b4601b2d47f6a768d****
&RegionId=cn-hangzhou
&InstanceId.1=bp67acfmxazb4p****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<StopInvocationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</StopInvocationResponse>
```

`JSON` format

```
{
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|404|InvalidInvokeId.NotFound|The specified invoke ID does not exist.|The error message returned because the specified InvokeId parameter does not exist. Check whether the ID of the execution is correct.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

