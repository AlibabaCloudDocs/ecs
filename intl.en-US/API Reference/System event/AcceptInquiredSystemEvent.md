# AcceptInquiredSystemEvent

You can call this operation to accept the default operation for a system event in the Inquiring state and authorize the system to perform the default operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=AcceptInquiredSystemEvent&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AcceptInquiredSystemEvent|The operation that you want to perform. Set the value to AcceptInquiredSystemEvent. |
|EventId|String|Yes|e-2zeielxl1qzq8slb\*\*\*\*|The ID of the system event. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the system event. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=AcceptInquiredSystemEvent
&EventId=e-2zeielxl1qzq8slb****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<AcceptInquiredSystemEventResponse>
        <RequestId>4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D</RequestId>
</AcceptInquiredSystemEventResponse>
```

`JSON` format

```
{
    "RequestId":"4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|404|InvalidEventId.NoInquiringEventFound|%s|The error message returned because the specified EventId parameter is invalid.|
|403|OperationConflict|%s|The error message returned because this operation conflicts with another operation in progress. Try again later.|
|403|OperationFail.DiskCategoryNotSupported|%s|The error message returned because this operation is not supported while the disk is of the current category.|
|403|OperationFail.DiskStatusNotSupported|%s|The error message returned because this operation is not supported while the disk is in the current state.|
|403|OperationFail.InstanceStatusNotSupported|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|403|IncorrectInstanceStatus|%s|The error message returned because this operation is not supported while the instance is in the current state.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

