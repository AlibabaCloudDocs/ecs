# CreateCapacityReservation

You can call this operation to create a capacity reservation.

## Description

When you create a capacity reservation, you can specify attributes such as the zone and instance type. The system uses a private pool to reserve resources that match the specified attributes. If you select a private pool when you create a pay-as-you-go instance, this ensures that the instance is created.

-   The capacity reservation feature is in invitational preview. To use this service, submit a ticket.
-   Only capacity reservations that take effect immediately are supported. After you purchase a capacity reservation that takes effect immediately, the instance type is billed on a pay-as-you-go basis, regardless of whether you use the capacity reservation to create a pay-as-you-go instance. The billing stops until you manually release the capacity reservation or the system automatically releases the capacity reservation when it expires.
    -   You can call the [CreateInstance](~~25499~~) or [RunInstances](~~63440~~) operation to specify the private pool type when you create an instance. You can also call the [ModifyInstanceAttachmentAttributes](~~190006~~) operation to modify the private pool type. When an instance matches a private pool, you are charged based on the configurations of the instance such as the instance type, cloud disks, and public bandwidth.
    -   If no pay-as-you-go instance is created, you are charged only for the instance type.
-   Hourly bills of the instances that match a capacity reservation that takes effect immediately and the unused capacity can be offset by using savings plans or regional reserved Instances. Zonal reserved instances cannot be used to offset hourly bills. We recommend that you purchase reserved instances or savings plans before you use capacity reservations that take effect immediately. This way you can obtain an assured reservation for free.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateCapacityReservation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCapacityReservation|The operation that you want to perform. Set the value to CreateCapacityReservation. |
|InstanceType|String|Yes|ecs.g6.xlarge|The instance type. You can select only one instance type when you create a capacity reservation. |
|InstanceAmount|Integer|Yes|2|The total number of instances to be reserved for a single instance type. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId.N|RepeatList|Yes|cn-hangzhou-h|The ID of zone N in the region in which to create the capacity reservation. Capacity reservations can be created only in one zone. |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The `ClientToken` value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|PrivatePoolOptions.Name|String|No|crpTestName|The name of the capacity reservation. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|Description|String|No|This is description.|The description of the capacity reservation. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

This parameter is empty by default. |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool generated after the capacity reservation takes effect. Valid values:

-   Open: the open mode
-   Target: the private mode

Default value: Open. |
|StartTime|String|No|Now|The effective mode of the capacity reservation. You can set the capacity reservation to take effect immediately. Set the value to Now.

Default value: Now. |
|EndTimeType|String|No|Unlimited|The release mode of the capacity reservation. Valid values:

-   Limited: releases the capacity reservation at the specified time. You must also specify the `EndTime`parameter.
-   Unlimited: manually releases the capacity reservation. You can release capacity reservations at any time. |
|EndTime|String|No|2021-10-30T06:32:00Z|The expiration time of the capacity reservation. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. For more information, see [ISO 8601](~~25696~~). |
|Platform|String|No|Linux|The operating system of the instance. This parameter corresponds to the `Platform`parameter of regional reserved instances. If the operating system of a capacity reservation matches that of a regional reserved instance, the regional reserved instance can be used to offset bills of the unused capacity in the capacity reservation. Valid values:

-   Windows: Windows Server operating systems
-   Linux: Linux and Unix-like operating systems

Default value: Linux.

**Note:** This parameter is unavailable. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PrivatePoolOptionsId|String|crp-bp67acfmxazb4\*\*\*\*|The ID of the capacity reservation. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateCapacityReservation
&RegionId=cn-hangzhou
&InstanceType=ecs.g6.xlarge
&InstanceAmount=2
&ZoneId.1=cn-hangzhou-h
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateCapacityReservationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PrivatePoolOptionsId>crp-bp67acfmxazb4****</PrivatePoolOptionsId>
</CreateCapacityReservationResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PrivatePoolOptionsId": "crp-bp67acfmxazb4****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|400|InvalidStartTime.NotSupported|The specified StartTime should be within 180 calendar days from the current date, and you must specify a precision to hour.|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidStartTime.MalFormed|The specified StartTime is out of the permitted range.|The error message returned because the specified StartTime parameter exceeds the upper limit.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

