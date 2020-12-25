# InstallCloudAssistant

You can call this operation to install the Cloud Assistant client on one or more instances. You must restart the instances for the installed Cloud Assistant client to take effect.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=InstallCloudAssistant&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|InstallCloudAssistant|The operation that you want to perform. Set the value to InstallCloudAssistant.

**Note:** After you call the InstallCloudAssistant and [RebootInstance](~~25502~~) operations in sequence, the Cloud Assistant client takes effect. |
|InstanceId.N|RepeatList|Yes|i-bp1iudwa5b1tqa\*\*\*\*|The ID of instance N. Valid values of N: 1 to 50. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=InstallCloudAssistant
&InstanceId.1=i-bp11f7trr4hbi1****
&InstanceId.2=i-bp1iudwa5b1tqa****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<InstallCloudAssistantResponse>
      <RequestId>928E2273-5715-46B9-A730-238DC996A533</RequestId>
</InstallCloudAssistantResponse>
```

`JSON` format

```
{
    "RequestId": "928E2273-5715-46B9-A730-238DC996A533"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified instance does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

