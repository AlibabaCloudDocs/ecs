# CreateCapacityReservation

Creates a capacity reservation.

## Description

When you create a capacity reservation, you can specify attributes such as the zone and instance type. The system uses a private pool to reserve resources that match the specified attributes. For more information, see [Overview of Immediate Capacity Reservation](~~193633~~).

-   Resource Assurance is in invitational preview. To use Resource Assurance, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).
-   Only immediate capacity reservations are supported. Immediate capacity reservations take effect immediately after they are purchased . After you purchase an immediate capacity reservation, the instance type is billed on a pay-as-you-go basis, regardless of whether you use the capacity reservation to create pay-as-you-go instances. Billing stops until you manually release the capacity reservation or until the capacity reservation is automatically released when it expires.
    -   You can call the [CreateInstance](~~25499~~) or [RunInstances](~~63440~~) operation to configure a private pool when you create instances. You can also call the [ModifyInstanceAttachmentAttributes](~~190006~~) operation to modify the attributes of a private pool. When an instance matches a private pool, you are charged based on the configurations of the instance such as the instance type, disks, and public bandwidth.
    -   If no pay-as-you-go instance is created, you are charged only for the instance type.
-   Savings plans or regional reserved instances can be applied to offset hourly bills of the unused capacity of immediate capacity reservations and hourly bills of the instances that match immediate capacity reservations. Zonal reserved instances cannot be applied to offset these bills. We recommend that you purchase reserved instances or savings plans before you use immediate capacity reservations. This way, you can obtain assured resource reservations for free.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateCapacityReservation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCapacityReservation|The operation that you want to perform. Set the value to CreateCapacityReservation. |
|InstanceType|String|Yes|ecs.g6.xlarge|Instance type N. A capacity reservation can be created to reserve capacity of a single instance type. Set N to 1. |
|InstanceAmount|Integer|Yes|2|The total number of instances for which to reserve capacity of an instance type. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the capacity reservation. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId.N|RepeatList|Yes|cn-hangzhou-h|The ID of zone N within the region in which to create the capacity reservation. A capacity reservation can reserve resources within a single zone. |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The `ClientToken` value can contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|PrivatePoolOptions.Name|String|No|crpTestName|The name of the capacity reservation. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|Description|String|No|This is description.|The description of the capacity reservation. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

This parameter is empty by default. |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool to be generated after the capacity reservation takes effect. Valid values:

-   Open: open private pool
-   Target: targeted private pool

Default value: Open. |
|StartTime|String|No|Now|The mode in which the capacity reservation takes effect. You can specify a time value for this parameter to create the capacity reservation as a scheduled capacity reservation that takes effect at the specified time. Only immediate capacity reservations are supported, and you do not need to pass in a value for this parameter.

**Note:** If this parameter is empty, the capacity reservation is created as an immediate capacity reservation. |
|EndTimeType|String|No|Unlimited|The release mode of the capacity reservation. Valid values:

-   Limited: The capacity reservation is released at the specified time. If you specify this parameter, you must also specify the `EndTime` parameter.
-   Unlimited: The capacity reservation must be manually released. You can release it at any time. |
|EndTime|String|No|2021-10-30T06:32:00Z|The expiration time of the capacity reservation. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. For more information, see [ISO 8601](~~25696~~). |
|Platform|String|No|Linux|The operating system type of the instance. This parameter corresponds to the `Platform` parameter of regional reserved instances. If the operating system of a capacity reservation matches that of a regional reserved instance, the regional reserved instance can be applied to offset bills of the unused capacity of the capacity reservation. Valid values:

-   Windows: Windows Server operating systems
-   Linux: Linux and Unix-like operating systems

Default value: Linux.

**Note:** This parameter is unavailable. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the capacity reservation. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length. It cannot start with `acs:` or `aliyun`. It cannot contain `http://` or`https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the capacity reservation. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length. It cannot start with `acs:` or contain `http://` or `https://`. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the capacity reservation. |

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
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the required RegionId parameter is not specified.|
|400|InvalidStartTime.NotSupported|The specified StartTime should be within 180 calendar days from the current date, and you must specify a precision to hour.|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidStartTime.MalFormed|The specified StartTime is out of the permitted range.|The error message returned because the specified StartTime parameter exceeds the upper limit.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|The error message returned because the specified instance type or zone is unavailable or because you are not authorized to use resources of the specified instance type or zone.|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|The error message returned because you are not authorized to purchase resources in the specified zone.|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|The error message returned because the requested resources are unavailable in the specified zone. Try other resource types, or select other regions or zones.|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is invalid.|The error message returned because the specified InstanceType parameter is invalid.|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|The error message returned because the specified ZoneId.N parameter does not exist.|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|The error message returned because the requested resources are unavailable in the specified zone. Try other instance types, or select other regions or zones.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified resource group does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

