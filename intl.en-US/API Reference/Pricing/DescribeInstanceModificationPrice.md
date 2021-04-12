# DescribeInstanceModificationPrice

You can call this operation to query the pricing information about the new instance types or newly attached subscription data disks when you upgrade the configurations of subscription ECS instances that have not expired.

## Description

-   The pricing information can be queried for subscription ECS instances that have expired only when their configurations are upgraded. The pricing information cannot be queried when their configurations are downgraded.
-   The pricing information cannot be queried for pay-as-you-go ECS instances when their configurations are changed. Prices of pay-as-you-go ECS instances whose configurations are changed are the same as those of newly purchased pay-as-you-go instances. You can call the [DescribePrice](~~107829~~) operation to query the latest prices of ECS instances.
-   Before you upgrade the configurations of an instance, we recommend that you call the [DescribeResourcesModification](~~66187~~) operation to query the instance types that can be used for upgrade in the specified zone.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceModificationPrice&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeInstanceModificationPrice|The operation that you want to perform. Set the value to DescribeInstanceModificationPrice. |
|InstanceId|String|Yes|i-bp1f2o4ldh8l\*\*\*\*|The ID of the instance for which you want to query the prices of its new configurations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. |
|InstanceType|String|No|ecs.g6e.large|The new instance type. We recommend that you call the [DescribeResourcesModification](~~66187~~) operation to query the instance types that are available for use in the specified zone.

**Note:** When you call the DescribeInstanceModificationPrice operation, you must specify at least one of the following parameters: `InstanceType` and `DataDisk.N.*`. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. This parameter is required only when you upgrade a retired instance type to an available one and upgrade a non-I/O optimized instance type to an I/O optimized one. For more information about instance types, see [Instance families](~~25378~~) and [Retired instance types](~~55263~~).

Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD

This parameter is empty by default. |
|DataDisk.N.Category|String|No|cloud\_essd|The category of data disk N. You can specify this parameter if you want to query the prices of newly attached subscription data disks. Valid values of N: 1 to 16. Valid values:

-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud: basic disk

This parameter is empty by default.

**Note:** When you call the DescribeInstanceModificationPrice operation, you must specify at least one of the following parameters: `InstanceType` and `DataDisk.N.*`. |
|DataDisk.N.Size|Integer|No|100|The capacity of data disk N. Valid values of N: 1 to 16. Unit: GiB. Valid values:

-   Valid values when DataDisk.N.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.N.Category is set to cloud: 5 to 2000

The default value is the minimum capacity value that corresponds to the specified data disk category. |
|DataDisk.N.PerformanceLevel|String|No|PL1|Specifies the performance level of the data disk that is an ESSD. The N value must be the same as that in DataDisk.N.Category when `DataDisk.N.Category` is set to cloud\_essd. Valid values:

-   PL0: A single ESSD can deliver up to 10,000 random read/write IOPS.
-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

Default value: PL1.

For more information about ESSD performance levels, see [Enhanced SSDs](~~122389~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PriceInfo|Struct| |Details about the PriceInfo data, including the price and discount rules. |
|Price|Struct| |The price. |
|Currency|String|CNY|The currency unit. Valid values:

-   CNY
-   USD |
|DiscountPrice|Float|61.320|The discount. |
|OriginalPrice|Float|175.200|The original price. |
|TradePrice|Float|113.880|The transaction price, which is equal to the original price minus the discount. |
|Rules|Array of Rule| |The promotion rules. |
|Rule| | | |
|Description|String|Upgrade offers|The description of the promotion rule. |
|RuleId|Long|1234567890|The ID of the rule. |
|RequestId|String|A3DC3196-379B-4F32-A2C5-B937134FAD8A|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceModificationPrice
&RegionId=cn-hangzhou
&InstanceId=i-bp1f2o4ldh8l****
&InstanceType=ecs.g6e.large
&DataDisk.1.Category=cloud_essd
&DataDisk.1.Size=100
&DataDisk.1.PerformanceLevel=PL1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceModificationPriceResponse>
      <RequestId>A3DC3196-379B-4F32-A2C5-B937134FAD8A</RequestId>
      <PriceInfo>
            <Rules>
                  <Rule>
                        <Description>Upgrade offers</Description>
                        <RuleId>1234567890</RuleId>
                  </Rule>
            </Rules>
            <Price>
                  <OriginalPrice>175.200</OriginalPrice>
                  <Currency>CNY</Currency>
                  <DiscountPrice>61.320</DiscountPrice>
                  <TradePrice>113.880</TradePrice>
            </Price>
      </PriceInfo>
</DescribeInstanceModificationPriceResponse>
```

`JSON` format

```
{
    "RequestId": "A3DC3196-379B-4F32-A2C5-B937134FAD8A", 
    "PriceInfo": {
        "Rules": {
            "Rule": [
                {
                    "Description": "Upgrade offers", 
                    "RuleId": "1234567890"
                }
            ]
        }, 
        "Price": {
            "OriginalPrice": "175.200", 
            "Currency": "CNY", 
            "DiscountPrice": "61.320", 
            "TradePrice": "113.880"
        }
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|The error message returned because the specified ResourceOwnerAccount parameter is invalid.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified ResourceGroupId parameter does not exist.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidDiskCategory.Missing|The DataDisk.1.Category parameter that is mandatory for processing the request is not provided.|The error message returned because the DataDisk.N.Category parameter is not specified.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or because you are not authorized to manage instances of the specified instance type.|
|400|InstanceType.Offline|%s|The error message returned because the operation is not supported while the instance type is retired or resources of the instance type are insufficient.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to perform the operation in the specified region.|
|500|InternalError|%s|The error message returned because an internal error has occurred.|
|400|PriceNotFound|The price of your queried resource is not available now, please try other resources.|The error message returned because the price of the resource cannot be queried. Try again later.|
|403|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

