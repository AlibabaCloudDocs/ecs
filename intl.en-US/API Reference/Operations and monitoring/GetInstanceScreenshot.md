# GetInstanceScreenshot

You can call this operation to obtain screenshots of an instance.

## Description

ECS returns an instance screenshot that is in the JPG format and encoded in Base64. You must manually decode the screenshot. We recommend that you call this operation for troubleshooting and diagnosis. When you call this operation, take note of the following items:

-   The instance must be in the Running state.
-   For instances of the retired instance types, you cannot obtain the screenshot information. For more information, see [Retired instance types](~~55263~~).
-   If you call this operation in the same instance for multiple times, the call interval must be at least 10 seconds. Otherwise, the `Throttling` error code is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=GetInstanceScreenshot&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetInstanceScreenshot|The operation that you want to perform. Set the value to GetInstanceScreenshot. |
|InstanceId|String|Yes|i-bp1gbz20g229bvu5\*\*\*\*|The ID of the instance. |
|RegionId|String|Yes|cn-shenzhen|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|WakeUp|Boolean|No|false|Specifies whether to wake up the instance that is in sleep mode.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceId|String|i-bp1gbz20g229bvu5\*\*\*\*|The ID of the instance. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|Screenshot|String|iVBORw0KGgoA...AAABJRU5ErkJggg==|The JPG-formatted instance screenshot, which is encoded in Base64. |

## Examples

Sample requests

```
http://ecs-cn-hangzhou.example.com/?Action=GetInstanceScreenshot
&InstanceId=i-bp1gbz20g229bvu5****
&RegionId=cn-shenzhen
&WakeUp=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<GetInstanceScreenshotResponse>
      <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
      <InstanceId>i-bp1gbz20g229bvu5****</InstanceId>
      <Screenshot>iVBORw0KGgoA...AAABJRU5ErkJggg==</Screenshot>
</GetInstanceScreenshotResponse>
```

`JSON` format

```
{
    "RequestId": "22A1933F-AD02-4560-A6A7-53CF2231D942",
    "InstanceId": "i-bp1gbz20g229bvu5****",
    "Screenshot": "iVBORw0KGgoA...AAABJRU5ErkJggg=="
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|404|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|405|IncorrectInstanceStatus|%s|The error message returned because this operation is not supported while the instance is in the current state.|
|405|NotSupported|%s|The error message returned because the operation is invalid.|
|429|Throttling|%s|The error message returned because the request is denied due to request throttling.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

