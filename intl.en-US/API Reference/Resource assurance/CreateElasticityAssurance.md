# CreateElasticityAssurance

Creates an elasticity assurance.

## Description

Elasticity Assurance provides a new method to purchase and use resources with flexibility and assurance. It offers assured resource reservations for pay-as-you-go Elastic Compute Service \(ECS\) instances. For more information, see [Overview of Elasticity Assurance](~~193630~~).

-   Resource Assurance is in invitational preview. To use Resource Assurance, [submit a ticket](https://workorder-intl.console.aliyun.com/console.htm).
-   Elasticity assurances are not refundable after purchase.
-   Elasticity assurances are applicable only to pay-as-you-go ECS instances.
-   Only elasticity assurances in unlimited mode are supported. You can set `AssuranceTimes` only to `Unlimited`. Elasticity assurances in unlimited mode can be applied for an unlimited number of times within their effective duration. Elasticity assurances in unlimited mode takes effect immediately after they are purchased.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateElasticityAssurance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateElasticityAssurance|The operation that you want to perform. Set the value to CreateElasticityAssurance. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region in which to create the elasticity assurance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId.N|RepeatList|Yes|cn-hangzhou-h|The ID of zone N within the region in which to create the elasticity assurance. An elasticity assurance can reserve resources within a single zone. |
|InstanceType.N|RepeatList|Yes|ecs.c6.xlarge|Instance type N. An elasticity assurance can be created to reserve capacity of a single instance type. Set N to 1. |
|Period|Integer|No|1|The effective duration of the elasticity assurance. The unit of the duration is determined by the `PeriodUnit` value. Valid values:

 -   When the `PeriodUnit` parameter is set to `Month`, the valid values of the Period parameter are 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   When the `PeriodUnit` parameter is set to `Year`, the valid values of the Period parameter are 1, 2, 3, 4, and 5.

 Default value: 1. |
|PeriodUnit|String|No|Year|The unit of the effective duration for the elasticity assurance. Valid values:

 -   Month
-   Year

 Default value: Year. |
|ClientToken|String|No|0c593ea1-3bea-11e9-b96b-88e9fe637760|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The `ClientToken` value can contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|PrivatePoolOptions.Name|String|No|eapTestName|The name of the elasticity assurance. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|Description|String|No|This is description.|The description of the elasticity assurance. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.

 This parameter is empty by default. |
|PrivatePoolOptions.MatchCriteria|String|No|Open|The type of the private pool to be associated with the elasticity assurance. Valid values:

 -   Open: open private pool
-   Target: targeted private pool

 Default value: Open. |
|AssuranceTimes|String|No|Unlimited|The total number of times that the elasticity assurance can be applied. Set the value to Unlimited. This value indicates that the elasticity assurance can be applied for an unlimited number of times within its effective duration.

 Default value: Unlimited. |
|InstanceAmount|Integer|No|2|The total number of instances for which to reserve capacity of an instance type. |
|StartTime|String|No|2020-10-30T06:32:00Z|The time when the elasticity assurance takes effect. The default value is the time when the CreateElasticityAssurance operation is called to create the elasticity assurance. Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. For more information, see [ISO 8601](~~25696~~). |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which to assign the elasticity assurance. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the elasticity assurance. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length. It cannot start with `acs:` or `aliyun`. It cannot contain `http://` or`https://`. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the elasticity assurance. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length. It cannot start with `acs:` or contain `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|1234567890|The ID of the order. |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|The ID of the elasticity assurance. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateElasticityAssurance
&RegionId=cn-hangzhou
&InstanceType.1=ecs.c6.xlarge
&ZoneId.1=cn-hangzhou-h
&InstanceAmount=2
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateElasticityAssuranceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PrivatePoolOptionsId>eap-bp67acfmxazb4****</PrivatePoolOptionsId>
      <OrderId>1234567890</OrderId>
</CreateElasticityAssuranceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PrivatePoolOptionsId": "eap-bp67acfmxazb4****",
    "OrderId": "1234567890"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|The error message returned because the required RegionId parameter is not specified.|
|400|InvalidStartTime.NotSupported|The specified StartTime should be within 180 calendar days from the current date, and you must specify a precision to hour.|The error message returned because the specified StartTime parameter is invalid.|
|400|InvalidStartTime.MalFormed|The specified StartTime is out of the permitted range.|The error message returned because the specified StartTime parameter exceeds the upper limit.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|The error message returned because the specified instance type or zone is unavailable or because you are not authorized to use resources of the specified instance type or zone.|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|The error message returned because you are not authorized to purchase resources in the specified zone.|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|The error message returned because the requested resources are unavailable in the specified zone. Try other resource types, or select other regions or zones.|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is invalid.|The error message returned because the specified InstanceType.N parameter is invalid.|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|The error message returned because the specified ZoneId.N parameter does not exist.|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|The error message returned because the requested resources are unavailable in the specified zone. Try other instance types, or select other regions or zones.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified resource group does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

