# DescribeDemands

You can call this operation to query the delivery and usage status of filed resources.

## Description

You can call this operation to query the details of resources filed by Alibaba Cloud, including the types, delivery status, and consumption status of the resources.

By default, the filing tickets of I/O optimized VPC-type instances are queried.

For information about how to create \(CreateDemand\), modify \(ModifyDemand\), and delete \(DeleteDemand\) filing tickets on ECS resources, contact your account manager.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeDemands&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDemands|The operation that you want to perform. Set the value to DescribeDemands. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DemandId|String|No|ed-bp11n21kq00sl71p\*\*\*\*|The ID of the filing ticket. If this parameter is specified, other optional request parameters are ignored. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|ZoneId|String|No|cn-hangzhou-g|The zone ID. You can call the [DescribeZones](~~25610~~) operation to query the most recent zone list. |
|InstanceChargeType|String|No|PostPaid|The billing method of the instance. Valid values:

-   PostPaid: pay-as-you-go
-   PrePaid: subscription |
|InstanceTypeFamily|String|No|ecs.g6|The instance family of the filed instance. |
|InstanceType|String|No|ecs.g6.xlarge|The instance type of the filed instance. |
|DemandType|String|No|Custom|The source of the filed instance. Default value: System. Valid values:

-   Custom: filed on your own.
-   System: filed by Alibaba Cloud. |
|DemandStatus.N|RepeatList|No|Active|The status of the filing ticket or resource usage. Valid values:

-   Creating: The filing ticket is being created.
-   Active: The filed resources are being supplied.
-   Expired: The filing ticket expires.
-   Finished: The filed resources are consumed.
-   Refused: The filing request is denied. For reasons why the request is denied, see the `Comment` response parameter.
-   Cancelled: The filing request is canceled. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: sends a check request, without querying the status of the filing ticket. The system checks whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are set. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: sends an API request. If the request succeeds, a 2XX HTTP status code is returned and the status of the filing ticket is queried. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Demands|Array| |Details about the filing tickets whose regions meet the filter condition. |
|Demand| | | |
|AvailableAmount|Integer|10|The number of instances available for the filed resources. |
|Comment|String|test-for-comment|The feedback on the denied request for filing resources. |
|DeliveringAmount|Integer|20|The number of instances to be delivered in the filed resources. |
|DemandDescription|String|test-DemandDescription|The description of the filing ticket. |
|DemandId|String|ed-bp11n21kq00sl71p\*\*\*\*|The ID of the filing ticket. |
|DemandName|String|k8s-node-demand|The name of the filing ticket. |
|DemandStatus|String|Active|The status of the filing ticket or resource usage. Valid values:

-   Creating: The filing ticket is being created.
-   Active: The filed resources are being supplied.
-   Expired: The filing ticket expires.
-   Finished: The filed resources are consumed.
-   Refused: The filing request is denied. For reasons why the request is denied, see the `Comment` response parameter.
-   Cancelled: The filing request is canceled. After the filing request is canceled, the delivery status of the resources becomes invalid. |
|DemandTime|String|2019-02-26T12:00:00Z|The time when the filing ticket was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|EndTime|String|2019-03-03T15:00:00Z|The expected end time for the purchase of the filed resources. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|InstanceChargeType|String|Prepaid|The billing method of the filed resources. Valid values:

-   Prepaid: subscription
-   Postpaid: pay-as-you-go |
|InstanceType|String|ecs.g6.xlarge|The instance type of the filed instance. |
|InstanceTypeFamily|String|ecs.g6|The instance family of the filed instance. |
|Period|Integer|3|The usage duration of the filed resource. |
|PeriodUnit|String|Month|The unit of the usage duration of the filed resource. Valid values:

-   Hour
-   Day
-   Month |
|StartTime|String|2019-02-27T12:00:00Z|The expected start time for the purchase of the filed resources. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|SupplyInfos|Array| |Details about the delivery status of the filed resources. |
|SupplyInfo| | | |
|Amount|Integer|30|The number of delivered instances. |
|SupplyEndTime|String|2019-03-03T15:00:00Z|The end time when the filed resources are delivered and available. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|SupplyStartTime|String|2019-03-01T14:00:00Z|The start time when the filed resources are delivered and available. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|SupplyStatus|String|Delivering|The delivery status of the filed resource. Valid values:

-   Delivered: The filed resource is delivered.
-   Delivering: The filed resource is being delivered. |
|TotalAmount|Integer|50|The number of filed instances. |
|UsedAmount|Integer|20|The number of consumed instances. |
|ZoneId|String|cn-hangzhou-g|The ID of the zone where the filed resource resides. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RegionId|String|cn-hangzhou|The region ID. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|6|The number of queried filing tickets. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeDemands
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDemandsResponse>
      <Demands>
            <AvailableAmount>0</AvailableAmount>
            <DeliveringAmount>50</DeliveringAmount>
            <DemandStatus>Expired</DemandStatus>
            <DemandTime>2019-02-26T12:00:00Z</DemandTime>
            <EndTime>2019-03-03T15:00:00Z</EndTime>
            <InstanceChargeType>PrePaid</InstanceChargeType>
            <DemandName>testnames</DemandName>
            <DemandDescription>testDesc</DemandDescription>
            <InstanceType>ecs.g6.xlarge</InstanceType>
            <DemandId>ed-bp16iilptf1tnc0y2***</DemandId>
            <Comment>zone closed</Comment>
            <InstanceTypeFamily>ecs.g6</InstanceTypeFamily>
            <Period>3</Period>
            <PeriodUnit>Month</PeriodUnit>
            <StartTime>2019-02-27T12:00:00Z</StartTime>
            <SupplyInfos>
                  <Amount>50</Amount>
                  <SupplyEndTime>2019-03-03T15:00:00Z</SupplyEndTime>
                  <SupplyStartTime>2019-03-01T14:00:00Z</SupplyStartTime>
                  <SupplyStatus>Delivering</SupplyStatus>
            </SupplyInfos>
            <TotalAmount>50</TotalAmount>
            <UsedAmount>0</UsedAmount>
            <ZoneId>cn-hangzhou-g</ZoneId>
      </Demands>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <RegionId>cn-hangzhou</RegionId>
      <RequestId>04066112-BF3A-4FCD-ABBD-B4B5EDAE9DXX</RequestId>
      <TotalCount>1</TotalCount>
</DescribeDemandsResponse>
```

`JSON` format

```
{
    "Demands": [
        {
            "AvailableAmount": 0,
            "DeliveringAmount": 50,
            "DemandStatus": "Expired",
            "DemandTime": "2019-02-26T12:00:00Z",
            "EndTime": "2019-03-03T15:00:00Z",
            "InstanceChargeType": "PrePaid",
            "DemandName": "testnames",
            "DemandDescription": "testDesc",
            "InstanceType": "ecs.g6.xlarge",
            "DemandId": "ed-bp16iilptf1tnc0y2***",
             "Comment": "zone closed",                       
            "InstanceTypeFamily": "ecs.g6",
            "Period": 3,
            "PeriodUnit": "Month",
            "StartTime": "2019-02-27T12:00:00Z",
            "SupplyInfos": [
                {
                    "Amount": "50",
                    "SupplyEndTime": "2019-03-03T15:00:00Z",
                    "SupplyStartTime": "2019-03-01T14:00:00Z",
                    "SupplyStatus": "Delivering"
                }
            ],
            "TotalAmount": 50,
            "UsedAmount": 0,
            "ZoneId": "cn-hangzhou-g"
        }
    ],
    "PageNumber": 1,
    "PageSize": 10,
    "RegionId": "cn-hangzhou",
    "RequestId": "04066112-BF3A-4FCD-ABBD-B4B5EDAE9DXX",
    "TotalCount": 1
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParamter.RegionId|The regionId should not be null.|The error message returned because the RegionId parameter is not specified.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because you are not authorized to manage this resource, or this API operation does not support RAM roles.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

