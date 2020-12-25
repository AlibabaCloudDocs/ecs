# CancelSimulatedSystemEvents

You can call this operation to cancel one or more simulated system events that are in the Scheduled or Executing state. After you cancel a simulated system event, the simulated event enters the Canceled state.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CancelSimulatedSystemEvents&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CancelSimulatedSystemEvents|The operation that you want to perform. Set the value to CancelSimulatedSystemEvents. |
|EventId.N|RepeatList|Yes|e-xhskHun1256\*\*\*\*|The ID of system event N. Valid values of N: 1 to 100. Specify multiple values in the repeated list format. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the system event. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CancelSimulatedSystemEvents
&EventId.1=e-xhskHun1256****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CancelSimulatedSystemEventsResponse>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CancelSimulatedSystemEventsResponse>
```

`JSON` format

```
{
    "RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|CannotCancelSystemEvent.NotSimulated|%s|The error message returned because you cannot cancel a non-simulated system event.|
|403|InvalidEventId.NotFound|%s|The error message returned because the specified EventId parameter is invalid.|
|400|EventIdLimitExceeded|%s|The error message returned because more than 100 system event IDs are specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

