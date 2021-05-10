# DescribePrice

You can call this operation to query the most recent prices of Elastic Compute Resource \(ECS\) resources.

## Description

-   The required parameters vary based on the types of resources whose prices you are querying.
    -   When the `ResourceType` parameter is set to instance, you must specify the `InstanceType` parameter.
    -   When the `ResourceType` parameter is set to disk, you must specify the `DataDisk.1.Category` and `DataDisk.1.Size` parameters. When the ResourceType parameter is set to `disk`, only the pay-as-you-go disk prices are returned. In this scenario, the `PriceUnit` parameter can be set only to `Hour`.
    -   When the `ResourceType` parameter is set to ddh, you must specify the `DedicatedHostType` parameter.
-   When the `ResourceType` is set to bandwidth, only the pay-by-traffic \(`PayByTraffic`\) price for network usage is returned.
-   When the `ResourceType` parameter is set to instance, the prices of up to four data disks can be queried.
-   By default, the `ChargeType` parameter is set to `PostPaid`. You can specify the `PriceUnit` parameter to query prices of ECS resources that have different billing cycles.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribePrice&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribePrice|The operation that you want to perform. Set the value to DescribePrice. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the ECS resource. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceType|String|No|instance|The type of resources whose most recent prices to query. Valid values:

-   instance: queries the most recent prices of ECS instances. When this parameter is set to `instance`, you must specify the `InstanceType` parameter.
-   disk: queries the most recent prices of disks. When this parameter is set to `disk`, you must specify the `DataDisk.1.Category` and `DataDisk.1.Size` parameters.
-   bandwidth: queries the most recent prices for network usage.
-   ddh: queries the most recent prices of dedicated hosts.

Default value: instance. |
|ImageId|String|No|centos\_7\_05\_64\_20G\_alibase\_20181212.vhd|The ID of the image, which indicates the runtime environment to load when the instance starts. You can call the [DescribeImages](~~25534~~) operation to query the available images. If you do not specify this parameter, the system queries the prices of Linux images. |
|InstanceType|String|No|ecs.g6.large|The instance type. When the `ResourceType` parameter is set to `instance`, you must specify the InstanceType parameter. For more information, see [Instance families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent list of instance types. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

If the instance type specified by the InstanceType parameter belongs to [Generation I instance families](~~55263~~), the default value is none.

If the instance type specified by the InstanceType parameter does not belong to [Generation I instance families](~~55263~~), the default value is optimized. |
|InstanceNetworkType|String|No|vpc|The network type of the instance. Valid values:

-   classic: classic network
-   vpc: Virtual Private Cloud \(VPC\)

Default value: vpc. |
|InternetChargeType|String|No|PayByTraffic|The billing method for network usage. Valid values:

-   PayByBandwidth: pay-by-bandwidth
-   PayByTraffic: pay-by-traffic

Default value: PayByTraffic. |
|InternetMaxBandwidthOut|Integer|No|5|The maximum outbound public bandwidth. Unit: Mbit/s. Valid values: 0 to 100.

Default value: 0. |
|SystemDisk.Category|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: enhanced SSD \(ESSD\)

Description of the default values:

-   When the InstanceType parameter is set to a retired instance type and the `IoOptimized` parameter is set to `none`, the default value is `cloud`.
-   In other cases, the default value is `cloud_efficiency`. |
|SystemDisk.Size|Integer|No|80|The size of the system disk. Unit: GiB. Valid values: 20 to 500.

The default value is 40 or the size of the image, depending on whichever is greater.

**Note:** The value of this parameter must be at least 20 and greater than or equal to the image size. |
|SystemDisk.PerformanceLevel|String|No|PL1|The performance level of the system disk when it is an ESSD. This parameter is valid only when the `SystemDiskCategory` parameter is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0
-   PL1
-   PL2
-   PL3 |
|DataDisk.1.Size|Integer|No|2000|The size of the first data disk. Unit: GiB. Valid values:

-   Valid values when DataDisk.1.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.1.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.1.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.1.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.1.Category is set to ephemeral\_ssd: 5 to 800 |
|DataDisk.1.Category|String|No|cloud\_ssd|The category of the first data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD |
|DataDisk.1.PerformanceLevel|String|No|PL1|The performance level of the first data disk when it is an ESSD. This parameter is valid only when the `DataDisk.1.Category` parameter is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0
-   PL1
-   PL2
-   PL3 |
|DataDisk.2.Size|Integer|No|200|The size of the second data disk. Unit: GiB.

-   Valid values when DataDisk.2.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.2.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.2.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.2.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.2.Category is set to ephemeral\_ssd: 5 to 800 |
|DataDisk.2.Category|String|No|cloud\_ssd|The category of the second data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD |
|DataDisk.2.PerformanceLevel|String|No|PL1|The performance level of the second data disk when it is an ESSD. This parameter is valid only when the `DataDisk.2.Category` parameter is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0
-   PL1
-   PL2
-   PL3 |
|DataDisk.3.Size|Integer|No|2000|The size of the third data disk. Unit: GiB.

-   Valid values when DataDisk.3.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.3.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.3.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.3.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.3.Category is set to ephemeral\_ssd: 5 to 800 |
|DataDisk.3.Category|String|No|cloud\_ssd|The category of the third data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD |
|DataDisk.3.PerformanceLevel|String|No|PL1|The performance level of the third data disk when it is an ESSD. This parameter is valid only when the `DataDisk.3.Category` parameter is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0
-   PL1
-   PL2
-   PL3 |
|DataDisk.4.Size|Integer|No|2000|The size of the fourth data disk. Unit: GiB.

-   Valid values when DataDisk.4.Category is set to cloud: 5 to 2000
-   Valid values when DataDisk.4.Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when DataDisk.4.Category is set to cloud\_ssd: 20 to 32768
-   Valid values when DataDisk.4.Category is set to cloud\_essd: 20 to 32768
-   Valid values when DataDisk.4.Category is set to ephemeral\_ssd: 5 to 800 |
|DataDisk.4.Category|String|No|cloud\_ssd|The category of the fourth data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD |
|DataDisk.4.PerformanceLevel|String|No|PL1|The performance level of the fourth data disk when it is an ESSD. This parameter is valid only when the `DataDisk.4.Category` parameter is set to cloud\_essd. Default value: PL1. Valid values:

-   PL0
-   PL1
-   PL2
-   PL3 |
|Period|Integer|No|1|The billing duration of the ECS instance. Valid values:

-   Valid values when PriceUnit is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   Valid values when PriceUnit is set to Year: 1, 2, 3, 4, and 5.
-   Set the value to 1 when PriceUnit is set to Hour.

Default value: 1. |
|PriceUnit|String|No|Year|The pricing unit of the ECS resource. Default value: Hour. Valid values:

-   Month
-   Year
-   Hour |
|Amount|Integer|No|1|The number of ECS instances that you want to purchase. You can specify this parameter when you want to query the prices of multiple instances that have specific specifications. Valid values: 1 to 1000.

Default value: 1. |
|AssuranceTimes|String|No|Unlimited|The total number of times that the elasticity assurance can be applied. Set the value to Unlimited. This value indicates that the elasticity assurance can be applied for an unlimited number of times within its effective duration.

Default value: Unlimited. |
|InstanceTypeList.N|RepeatList|No|ecs.g6.xlarge|Instance type N. You can select only a single instance type when you configure an elasticity assurance in unlimited mode. |
|DedicatedHostType|String|No|ddh.c5|The dedicated host type. You can call the [DescribeDedicatedHostTypes](~~134240~~) operation to query the most recent list of dedicated host types. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PriceInfo|Struct| |Details about the prices and discount rules. |
|Price|Struct| |The price. |
|Currency|String|CNY|The currency unit. |
|DetailInfos|Array of ResourcePriceModel| |Details about the price. |
|ResourcePriceModel| | | |
|DiscountPrice|Float|655.2|The discount. |
|OriginalPrice|Float|4368|The original price. |
|Resource|String|instance|The name of the resource. |
|SubRules|Array of Rule| |Details about the pricing rules. |
|Rule| | | |
|Description|String|Receive a 15% discount on a 1-year subscription|The description of the pricing rule. |
|RuleId|Long|587|The ID of the rule. |
|TradePrice|Float|3712.8|The transaction price. |
|DiscountPrice|Float|655.2|The discount. |
|OriginalPrice|Float|4368|The original price. |
|ReservedInstanceHourPrice|Float|1|The hourly price of the reserved instance for which the no-upfront or partial-upfront payment option is used. |
|TradePrice|Float|3712.8|The final transaction price after discounts are applied. |
|Rules|Array of Rule| |Details about the promotion rules. |
|Rule| | | |
|Description|String|Receive a 15% discount on a 1-year subscription|The description of the promotion rule. |
|RuleId|Long|587|The ID of the promotion rule. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribePrice
&RegionId=cn-hangzhou
&ResourceType=instance
&InstanceType=ecs.g6.large
&ImageId=centos_7_05_64_20G_alibase_20181212.vhd
&InstanceNetworkType=vpc
&InternetChargeType=PayByTraffic
&InternetMaxBandwidthOut=5
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribePriceResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <PriceInfo>
            <Price>
                  <Currency>CNY</Currency>
                  <DiscountPrice>655.2</DiscountPrice>
                  <OriginalPrice>4368</OriginalPrice>
                  <TradePrice>3712.8</TradePrice>
            </Price>
            <Rules>
                  <Rule>
                        <Description>Receive a 15% discount on 1-year subscription</Description>
                        <RuleId>ONE_YEAR_85_PERCENT</RuleId>
                  </Rule>
            </Rules>
      </PriceInfo>
</DescribePriceResponse>
```

`JSON` format

```
{
  "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
  "PriceInfo": {
    "Price": {
      "Currency": "CNY",
      "DiscountPrice": 655.2,
      "OriginalPrice": 4368,
      "TradePrice": 3712.8
    },
    "Rules": {
      "Rule": [
        {
          "Description": "Receive a 15% discount on 1-year subscription",
          "RuleId": "ONE_YEAR_85_PERCENT"
        }
      ]
    }
  }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|The error message returned because you are not authorized to use the specified instance type.|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|The error message returned because the specified InstanceType parameter does not exist or because you are not authorized to manage instances of this instance type.|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter "InternetMaxBandwidthOut" is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or because the snapshot size exceeds the maximum capacity allowed for the specified disk category.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|The error message returned because the specified image cannot be used for instances of the specified instance type.|
|403|ImageNotSubscribed|The specified image has not be subscribed.|The error message returned because you have not subscribed to the specified Alibaba Cloud Marketplace image.|
|403|OperationDenied|The specified Image is disabled or is deleted.|The error message returned because the specified image has been disabled or deleted.|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|The error message returned because you are not authorized to use the specified disk category.|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|The error message returned because the total size of disks of the specified category exceeds the maximum capacity allowed for an instance.|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|The error message returned because the specified Alibaba Cloud Marketplace image is unavailable, or because the specified custom image contains the product code of the Alibaba Cloud Marketplace image from which the custom image is derived and the Alibaba Cloud Marketplace image has been removed from Alibaba Cloud Marketplace.|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|The error message returned because the maximum number of removable disks has been reached.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|The error message returned because the network type of the instance does not support the specified billing method for network usage.|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|403|Forbbiden|User not authorized to operate on the specified resource.|The error message returned because you are not authorized to perform operations on the specified resource.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account. Check whether the image ID is correct.|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|The error message returned because the maximum number of disks that can be attached to the instance has been reached.|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|The error message returned because the specified image does not support I/O optimized instances.|
|403|ImageNotSupportInstanceType|The specified image don't support the InstanceType instance.|The error message returned because the specified image does not support the instance type.|
|400|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|The error message returned because the specified IoOptimized parameter is invalid.|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|The error message returned because the specified instance type does not support I/O optimization.|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|The error message returned because the specified disk size is smaller than the snapshot size.|
|403|OperationDenied|The type of the disk does not support the operation|The error message returned because the disk category does not support the specified operation.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified instance billing method does not exist.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|The error message returned because the combination of the specified disk categories is not supported.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|The error message returned because the specified disk category does not support the instance type.|
|403|InvalidDiskCategory.NotSupported|The upgrade operation of instance does not support this category of disk.|The error message returned because the upgrade operations of instances do not the specified disk category.|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or because the snapshot size exceeds the maximum capacity allowed for the specified disk category.|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|The error message returned because the specified instance type is not I/O optimized.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned because the specified system disk size is smaller than the image size.|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the minimum size.|The error message returned because the specified system disk size is less than the lower limit.|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the maximum size|The error message returned because the maximum size of the specified system disk has been reached.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified vm bandwidth is not valid.|The error message returned because the specified bandwidth of the instance is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|The error message returned because the specified ResourceOwnerAccount parameter is invalid.|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|The error message returned because you are not authorized to create instances in the specified region.|
|404|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter Bandwidth is not valid.|The error message returned because the specified bandwidth is invalid.|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|The error message returned because the maximum number of disks that can be attached to the instance has been reached.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|OperationDenied|The resource is out of usage.|The error message returned because the instance is not in the Running state. Start the instance or check whether the operation is valid.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|%s|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the specified data disk category is invalid.|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|The error message returned because the operation is not applicable to the specified system disk category.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidInternetChargeType.ValueNotSupported|%s|The error message returned because the specified InternetChargeType parameter is invalid.|
|400|InvalidInstanceType.ValueNotSupported|%s|The error message returned because the operation is not applicable to the specified instance type.|
|403|InstanceType.Offline|%s|The error message returned because the operation is not supported while the instance type is retired or while resources of the instance type are insufficient.|
|400|RegionUnauthorized|%s|The error message returned because you are not authorized to perform the operation in the specified region.|
|500|InternalError|%s|The error message returned because an internal error has occurred.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the specified data disk size is invalid.|
|404|InvalidInstanceType.Missing|The InstanceType parameter that is mandatory for processing the request is not provided.|The error message returned because the InstanceType parameter is not specified.|
|404|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|The error message returned because the specified NetworkType parameter is invalid.|
|404|InvalidDiskCategory.Missing|The DataDisk.1.Category parameter that is mandatory for processing the request is not provided.|The error message returned because the DataDisk.1.Category parameter is not specified.|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Size" is not valid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|InvalidSystemDiskSize.LessThanImageSize|The specified parameter "SystemDisk.Size" is less than the image size.|The error message returned because the specified system disk size is smaller than the image size.|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.Category" is not valid.|The error message returned because the specified DataDisk.N.Category parameter is invalid.|
|400|InvalidDataDiskSize.ValueNotSupported|The specified parameter "DataDisk.Size" is not valid.|The error message returned because the specified DataDisk.N.Size parameter is invalid.|
|400|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|
|400|PriceNotFound|The price of your queried resource is not available now, please try other resources.|The error message returned because the price of the resource is not found. Modify parameters and try again later.|
|400|InvalidResourceType.ValueNotSupported|The specified parameter ResourceType is not valid.|The error message returned because the specified ResourceType parameter is invalid.|
|400|InvalidPriceUnit.ValueNotSupported|The specified parameter PriceUnit is not valid.|The error message returned because the specified PriceUnit parameter is invalid.|
|403|OperationDenied|The specified parameter InstanceNetworkType is not authorized.|The error message returned because you are not authorized to use the specified network type.|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter InternetMaxBandwidthOut is not valid.|The error message returned because the specified InternetMaxBandwidthOut parameter is invalid.|
|403|InvalidAmount.Malformed|The specified parameter Amount is not valid.|The error message returned because the specified Amount parameter is invalid.|
|400|EncryptedOption.Conflict|%s|The error message returned because the parameter used to encrypt disks is not supported.|
|404|Invalid.InstanceId.NotFound|The Instance provided does not exist.|The error message returned because the specified instance does not exist.|
|403|InvalidDiskSize.TooSmall|Specified system disk size is less than the size of image|The error message returned because the specified system disk size is smaller than the image size.|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|The error message returned because the specified Alibaba Cloud Marketplace image does not exist. Modify the ImageId parameter and try again later.|
|403|InvalidChargeType.MarketImage|The specified chargeType of marketplace image is invalid|The error message returned because the billing method for the Alibaba Cloud Marketplace image is not supported.|
|403|InvalidDiskIds.NotFound|Some of the specified disks do not exist.|The error message returned because some specified disk IDs do not exist.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|The error message returned because the specified disk category does not support the operation.|
|403|PrePaidInstance.Expired|The prePaid instance has expired.|The error message returned because the subscription instance has expired.|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|The error message returned because the specified disk is not removable.|
|404|InvalidSystemDisk.NotFound|The specified system disk does not exist.|The error message returned because the specified system disk does not exist.|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|The error message returned because the specified resource group does not exist.|
|403|InvalidAction.Unauthorized|The specified action is not valid.|The error message returned because the specified operation is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

