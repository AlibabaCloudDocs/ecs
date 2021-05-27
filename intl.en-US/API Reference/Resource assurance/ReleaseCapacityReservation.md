# ReleaseCapacityReservation

You can call this operation to release a capacity reservation.

## Description

When the release mode of a capacity reservation that takes effect immediately is set to manual release, you can call this operation to release the capacity reservation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ReleaseCapacityReservation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReleaseCapacityReservation|The operation that you want to perform. Set the value to ReleaseCapacityReservation. |
|PrivatePoolOptions.Id|String|Yes|crp-bp67acfmxazb4\*\*\*\*|The ID of the capacity reservation. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request. Set the value to false. The validity of the request is not checked. Capacity reservations are directly released. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ReleaseCapacityReservation
&RegionId=cn-hangzhou
&PrivatePoolOptions.Id=crp-bp67acfmxazb4****
&DryRun=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ReleaseCapacityReservationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ReleaseCapacityReservationResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

