# DescribeZones

You can call this operation to query zones in a region.

## Description

When you call this operation, only a list of zones and some resource information related to each zone is returned. If you want to query instance types and disk categories that are available for purchase in a specified zone, we recommend that you call the [DescribeAvailableResource](~~66186~~) operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeZones&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeZones|The operation that you want to perform. Set the value to DescribeZones. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region for which to query zones. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceChargeType|String|No|PostPaid|The billing method supported in the zone. For more information, see [Billing overview](~~25398~~). Default value: PostPaid. Valid values:

-   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|SpotStrategy|String|No|NoSpot|The bidding policy for pay-as-you-go instances. You can specify this parameter when the InstanceChargeType parameter is set to PostPaid. For more information, see [Preemptible instances](~~52088~~). Default value: NoSpot. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have maximum hourly prices.
-   SpotAsPriceGo: applies to preemptible instances priced at the market price at the time of purchase. |
|AcceptLanguage|String|No|zh-CN|The natural language that is used to filter responses. For more information, visit [RFC 7231](https://tools.ietf.org/html/rfc7231). Valid values:

-   zh-CN
-   en-US
-   ja

Default value: zh-CN. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|Zones|Array of Zone| |An array consisting of Zone data. |
|Zone| | | |
|AvailableDedicatedHostTypes|List|Compute type|The supported types of dedicated hosts. The data type of this parameter is List. |
|AvailableDiskCategories|List|cloud|The supported disk categories. The data type of this parameter is List. |
|AvailableInstanceTypes|List|c5|The instance types of instances that can be created. The data type of this parameter is List. |
|AvailableResourceCreation|List|DedicatedHost|The types of the resources that can be created. The data type of this parameter is List. |
|AvailableResources|Array of ResourcesInfo| |An array consisting of ResourcesInfo data. |
|ResourcesInfo| | | |
|DataDiskCategories|List|cloud\_ssd|The categories of data disks. The data type of this parameter is List. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   ephemeral\_ssd: local SSD |
|InstanceGenerations|List|Ⅳ|The generation numbers of instance families. The data type of this parameter is List. |
|InstanceTypeFamilies|List|\["d1", "d1ne"\]|The collection of supported instance families. The data type of this parameter is List. |
|InstanceTypes|List|\["ecs.g5.large"\]|The instance types of instances. The data type of this parameter is List. |
|IoOptimized|Boolean|true|Indicates whether the instance is I/O optimized. |
|NetworkTypes|List|VPC|The types of the network. The data type of this parameter is List. Valid values:

-   VPC
-   Classic |
|SystemDiskCategories|List|cloud\_ssd|The categories of system disks. The data type of this parameter is List. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD |
|AvailableVolumeCategories|List|san\_ssd|The categories of available shared storage. The data type of this parameter is List. |
|DedicatedHostGenerations|List|I|The generation numbers of dedicated hosts. The data type of this parameter is List. |
|LocalName|String|Hangzhou Zone G|The name of the zone in the local language. |
|ZoneId|String|cn-hangzhou-g|The zone ID. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeZones
&RegionId=cn-hangzhou
&InstanceChargeType=PostPaid
&SpotStrategy=NoSpot
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeZonesResponse>
      <Zones>
            <Zone>
                  <AvailableResourceCreation>
                        <ResourceTypes>Instance</ResourceTypes>
                        <ResourceTypes>Disk</ResourceTypes>
                  </AvailableResourceCreation>
                  <LocalName></LocalName>
                  <ZoneId>cn-hangzhou-d</ZoneId>
                  <AvailableDiskCategories>
                        <DiskCategories>cloud</DiskCategories>
                  </AvailableDiskCategories>
            </Zone>
            <Zone>
                  <AvailableResourceCreation>
                        <ResourceTypes>Instance</ResourceTypes>
                        <ResourceTypes>Disk</ResourceTypes>
                  </AvailableResourceCreation>
                  <LocalName></LocalName>
                  <ZoneId>cn-hangzhou-b</ZoneId>
                  <AvailableDiskCategories>
                        <DiskCategories>cloud</DiskCategories>
                  </AvailableDiskCategories>
            </Zone>
      </Zones>
      <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeZonesResponse>
```

`JSON` format

```
{
  "RequestId": "A347EF0E-BBCC-4EFA-BD79-27AA3ACFD1BF",
  "Zones": {
    "Zone": [
      {
        "AvailableDiskCategories": {
          "DiskCategories": [
            "cloud"
          ]
        },
        "AvailableResourceCreation": {
          "ResourceTypes": [
            "Instance",
            "Disk"
          ]
        },
        "LocalName": "",
        "ZoneId": "cn-hangzhou-d"
      },
      {
        "AvailableDiskCategories": {
          "DiskCategories": [
            "cloud"
          ]
        },
        "AvailableResourceCreation": {
          "ResourceTypes": [
            "Instance",
            "Disk"
          ]
        },
        "LocalName": "",
        "ZoneId": "cn-hangzhou-b"
      }
    ]
  }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|The error message returned because the specified InstanceChargeType parameter does not exist.|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|404|InvalidAcceptLanguage.NotFound|Only Chinese \(zh-CN\), English \(en-US\), and Japanese \(ja\) are allowed.|The error message returned because the selected language is not supported. Only Chinese, English, and Japanese are supported.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

