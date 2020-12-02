# DescribeSpotPriceHistory

You can call this operation to query the price history of a preemptible instance that was generated in the last 30 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeSpotPriceHistory&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSpotPriceHistory|The operation that you want to perform. Set the value to DescribeSpotPriceHistory. |
|InstanceType|String|Yes|ecs.t1.xsmall|The instance type of the instance. |
|NetworkType|String|Yes|vpc|The network type of the preemptible instance. Valid values:

-   classic
-   vpc |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID of the instance. |
|SpotDuration|Integer|No|1|The retention period of the preemptible instance. Unit: hours. Valid values: 0, 1, 2, 3, 4, 5, and 6.

-   Protection periods of 2, 3, 4, 5, and 6 hours are in invitational preview. If you want to set the protection period value to one of these values, submit a ticket.
-   If this parameter is set to 0, no protection period is configured for the preemptible instance.

Default value: 1. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   optimized
-   none

For generation I instance families, the default value is none.

For other instance families, the default value is optimized. |
|StartTime|String|No|2017-08-22T08:45:08Z|The start time of the query. Specify the time in the [ISO 8601](~~25696~~) standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.

This parameter is empty by default. If this parameter is empty, the start time is defined as three hours earlier than the specified EndTime. You can specify a StartTime value of up to 30 days earlier than the specified EndTime. |
|EndTime|String|No|2017-08-22T08:45:08Z|The end time of the query. Specify the time in the [ISO 8601](~~25696~~) standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC.

This parameter is empty by default. If this parameter is empty, the current time is used. |
|OSType|String|No|linux|The type of the operating system platform. Valid values:

-   linux
-   windows |
|Offset|Integer|No|0|The start row of the query.

Default value: 0. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Currency|String|CNY|The currency unit of the price. |
|NextOffset|Integer|1000|The start row of the next page. It is the value of the `Offset` parameter. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|SpotPrices|Array of SpotPriceType| |Details about the spot prices. |
|SpotPriceType| | | |
|InstanceType|String|ecs.g5.large|The instance type of the preemptible instance. |
|IoOptimized|String|optimized|Indicates whether the preemptible instance is I/O optimized. |
|NetworkType|String|vpc|The network type of the preemptible instance. |
|OriginPrice|Float|0.354|The price for a pay-as-you-go instance that has the same configuration as the specified preemptible instance. |
|SpotPrice|Float|0.036|The spot price of the preemptible instance. |
|Timestamp|String|2019-11-19T06:00:00Z|The time that corresponds to the queried spot price. The time is in the `yyyy-MM-ddTHH:mm:ssZ` format. |
|ZoneId|String|cn-hangzhou-c|The zone ID of the preemptible instance. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeSpotPriceHistory
&NetworkType=vpc
&RegionId=cn-hangzhou
&InstanceType=ecs.g5.large
&StartTime=2019-11-19T00:00:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSpotPriceHistoryResponse>
      <RequestId>5E2D59BA-4EB0-45C4-A0D7-D98C1A4B320B</RequestId>
      <SpotPrices>
            <SpotPriceType>
                  <IoOptimized>optimized</IoOptimized>
                  <OriginPrice>0.354</OriginPrice>
                  <NetworkType>vpc</NetworkType>
                  <ZoneId>cn-hangzhou-g</ZoneId>
                  <Timestamp>2019-11-19T06:00:00Z</Timestamp>
                  <SpotPrice>0.036</SpotPrice>
                  <InstanceType>ecs.g5.large</InstanceType>
            </SpotPriceType>
            <SpotPriceType>
                  <IoOptimized>optimized</IoOptimized>
                  <OriginPrice>0.354</OriginPrice>
                  <NetworkType>vpc</NetworkType>
                  <ZoneId>cn-hangzhou-g</ZoneId>
                  <Timestamp>2019-11-19T07:00:00Z</Timestamp>
                  <SpotPrice>0.036</SpotPrice>
                  <InstanceType>ecs.g5.large</InstanceType>
            </SpotPriceType>
      </SpotPrices>
      <Currency>CNY</Currency>
</DescribeSpotPriceHistoryResponse>
```

`JSON` format

```
{
    "RequestId": "5E2D59BA-4EB0-45C4-A0D7-D98C1A4B320B",
    "SpotPrices": {
        "SpotPriceType": [
            {
                "IoOptimized": "optimized",
                "OriginPrice": 0.354,
                "NetworkType": "vpc",
                "ZoneId": "cn-hangzhou-g",
                "Timestamp": "2019-11-19T06:00:00Z",
                "SpotPrice": 0.036,
                "InstanceType": "ecs.g5.large"
            },
            {
                "IoOptimized": "optimized",
                "OriginPrice": 0.354,
                "NetworkType": "vpc",
                "ZoneId": "cn-hangzhou-g",
                "Timestamp": "2019-11-19T07:00:00Z",
                "SpotPrice": 0.036,
                "InstanceType": "ecs.g5.large"
            }
        ]
    },
    "Currency": "CNY"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidUserType.NotSupported|%s|The error message returned because your account does not support this operation.|
|403|Abs.InvalidAccount.NotFound|%s|The error message returned because your Alibaba Cloud account does not exist or your AccessKey pair has expired.|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|Forbedden.NotSupportRAM|%s|The error message returned because RAM users are not authorized to perform this operation.|
|400|UnsupportedParameter|%s|The error message returned because a specific parameter is not supported.|
|403|Forbbiden.SubUser|%s|The error message returned because you are not authorized to manage this resource. Contact the owner of the Alibaba Cloud account for authorization.|
|400|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|400|InvalidInstanceID.Malformed|%s|The error message returned because the specified InstanceId parameter is invalid.|
|400|InvalidParams.StartTime|%s|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidParams.EndTime|%s|The error message returned because the specified EndTime parameter is invalid.|
|400|Abs.Abs.InvalidSpotInstanceUID|%s|The error message returned because the format of the preemptible instance ID is invalid.|
|400|InvalidParams.NetworkType|%s|The error message returned because the specified NetworkType parameter is invalid.|
|400|InvalidParams.IoOptimized|%s|The error message returned because the specified IoOptimized parameter is invalid.|
|400|InvalidParams.OSType|%s|The error message returned because the specified OSType parameter is invalid.|
|400|Abs.IoOptimized.ValueNotSupported|%s|The error message returned because the I/O optimization attribute of the instance is invalid. Check whether the specified IoOptimized parameter is valid.|
|400|InvalidZoneId.NotFound|The specified zone does not exist.|The error message returned because the specified ZoneId parameter does not exist.|
|400|InvalidParams.ZoneId|%s|The error message returned because the specified ZoneId parameter is invalid.|
|400|InvalidParams.RegionId|%s|The error message returned because the specified RegionId parameter is invalid.|
|400|InvalidParams.InstanceType|%s|The error message returned because the specified InstanceType parameter is invalid.|
|400|InvalidParams.PageSize|%s|The error message returned because the specified PageSize parameter is invalid.|
|400|InvalidParams.Offset|%s|The error message returned because the specified Offset parameter is invalid.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned because this operation cannot be performed on instances of the specified instance type.|
|400|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|The error message returned because the specified instance type is not I/O optimized.|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|The error message returned because the specified SpotDuration parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

