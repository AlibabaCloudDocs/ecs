# DescribeAvailableResource

You can call this operation to query resources in a zone. For example, you can query available resources in a zone before you create ECS instances \(RunInstances\) or before you modify instance specifications \(ModifyInstanceSpec\).

## Description

Values for the `DestinationResource` parameter have dependencies. When you select a value in the following chain for the DestinationResource parameter, the more to the right the selected value is ordered, the more parameters you must specify.

-   Sequence: `Zone > IoOptimized > InstanceType = Network = ddh > SystemDisk > DataDisk`
-   Examples:
    -   If you set `DestinationResource` to `DataDisk`, you must specify the `IoOptimized`, `InstanceType`, `SystemDiskCategory`, and `DataDiskCategory` parameters.
    -   If you set `DestinationResource` to `InstanceType`, you must specify the `IoOptimized` and `InstanceType` parameters.
    -   If you want to query the ecs.g5.large resources in all zones of the China \(Hangzhou\) region, you must set RegionId to cn-hangzhou, DestinationResource to InstanceType, IoOptimized to optimized, and InstanceType to ecs.g5.large.``
    -   If you want to query the zones where ecs.g5.large resources are available within the China \(Hangzhou\) region, you must set RegionId to cn-hangzhou, DestinationResource to Zone, IoOptimized to optimized, and InstanceType to ecs.g5.large.``

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAvailableResource&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAvailableResource|The operation that you want to perform. Set the value to DescribeAvailableResource. |
|DestinationResource|String|Yes|InstanceType|The resource type to be queried. Valid values:

-   Zone: zone
-   IoOptimized: I/O optimzied
-   InstanceType: instance type
-   SystemDisk: system disk
-   DataDisk: data disk
-   Network: network type
-   ddh: dedicated host

For more information about how to set the DestinationResource parameter, see the preceding Description section. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-e|The zone ID.

This parameter is empty by default. When this parameter is empty, the system returns resources that match the other criteria of all zones within the region specified by `RegionId`. |
|InstanceChargeType|String|No|PrePaid|The billing method of the resource. For more information, see [Billing overview](~~25398~~). Valid values:

-   PrePaid: subscription
-   PostPaid: pay-as-you-go

Default value: PostPaid. |
|SpotStrategy|String|No|NoSpot|The preemption policy for the preemptible or pay-as-you-go instance. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have maximum hourly prices.
-   SpotAsPriceGo: applies to preemptible instances priced at the market price at the time of purchase.

Default value: NoSpot.

This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid. |
|IoOptimized|String|No|optimized|Specifies whether the instance is I/O optimized. Valid values:

-   none
-   optimized

Default value: optimized |
|DedicatedHostId|String|No|dh-bp165p6xk2tlw61e\*\*\*\*|The ID of the dedicated host. |
|InstanceType|String|No|ecs.g5.large|The instance type. For more information, see [Instance type families](~~25378~~) or call the [DescribeInstanceTypes](~~25620~~) operation to query the most recent instance type list.

When the DestinationResource parameter is set to SystemDisk or DataDisk, the InstanceType parameter is required. |
|SystemDiskCategory|String|No|cloud\_ssd|The category of the system disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

When DestinationResource is set to SystemDisk, InstanceType, or DataDisk, the SystemDiskCategory parameter is optional.

Default value: cloud\_efficiency. |
|DataDiskCategory|String|No|cloud\_ssd|The category of the data disk. Valid values:

-   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD |
|NetworkCategory|String|No|vpc|The network type. Valid values:

-   vpc
-   classic |
|Cores|Integer|No|2|The number of vCPU cores of the instance type. For more information, see [Instance type families](~~25378~~).

This parameter takes effect only when the DestinationResource parameter is set to InstanceType. |
|Memory|Float|No|8.0|The memory size of the instance type. Unit: GiB. For more information, see [Instance type families](~~25378~~).

The Memory parameter takes effect only when the DestinationResource parameter is set to InstanceType. |
|ResourceType|String|No|instance|The type of the resource. Valid values:

-   instance: ECS instance
-   disk: cloud disk
-   reservedinstance: reserved instance
-   ddh: dedicated host |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AvailableZones|Array| |An array consisting of zones. |
|AvailableZone| | | |
|AvailableResources|Array| |An array consisting of available resource types. |
|AvailableResource| | | |
|SupportedResources|Array| |An array consisting of available resource types. |
|SupportedResource| | | |
|Max|Integer|2|The maximum number of resources of a specific type that can be created. No value is returned when this parameter is empty. |
|Min|Integer|1|The minimum value of resources of a specific type that can be created. No value is returned when the parameter is empty. |
|Status|String|Available|The status of the resource. Valid values:

-   Available
-   SoldOut |
|StatusCategory|String|WithStock|The resource category based on the stock. Valid values:

-   WithStock: Resources are in sufficient stock.
-   ClosedWithStock: Resources are insufficient. We recommend that you use resources in sufficient stock.
-   WithoutStock: Resources are sold out and will be replenished. We recommend that you use resources in sufficient stock.
-   ClosedWithoutStock: Resources are sold out and will not be replenished.We recommend that you use resources in sufficient stock. |
|Unit|String|null|The unit of the resource type. No value is returned when the parameter is empty. |
|Value|String|ecs.d1ne.xlarge|The value of the resource. |
|Type|String|InstanceType|The type of the resource. Valid values:

-   Zone: zone
-   IoOptimized: I/O optimized
-   InstanceType: instance type
-   SystemDisk: system disk
-   DataDisk: data disk
-   Network: network type
-   ddh: dedicated host |
|RegionId|String|cn-hangzhou|The region ID. |
|Status|String|Available|The status of the resource. Valid values:

-   Available
-   SoldOut |
|StatusCategory|String|WithStock|The resource category based on the stock. Valid values:

-   WithStock: Resources are in sufficient stock.
-   ClosedWithStock: Resources are insufficient. We recommend that you use resources in sufficient stock.
-   WithoutStock: Resources are sold out and will be replenished. We recommend that you use resources in sufficient stock.
-   ClosedWithoutStock: Resources are sold out and will not be replenished.We recommend that you use resources in sufficient stock. |
|ZoneId|String|cn-hangzhou-e|The zone ID. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAvailableResource
&RegionId=cn-hangzhou
&DestinationResource=InstanceType
&IoOptimized=optimized
&InstanceType=ecs.g5.large
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAvailableResourceResponse>
      <RequestId>0041D94C-FB92-4C49-B115-259DA1CE1923</RequestId>
      <AvailableZones>
            <AvailableZone>
                  <Status>Available</Status>
                  <RegionId>cn-hangzhou</RegionId>
                  <AvailableResources>
                        <AvailableResource>
                              <Type>InstanceType</Type>
                              <SupportedResources>
                                    <SupportedResource>
                                          <Status>Available</Status>
                                          <Value>ecs.g5.large</Value>
                                          <StatusCategory>WithStock</StatusCategory>
                                    </SupportedResource>
                              </SupportedResources>
                        </AvailableResource>
                  </AvailableResources>
                  <ZoneId>cn-hangzhou-i</ZoneId>
                  <StatusCategory>WithStock</StatusCategory>
            </AvailableZone>
      </AvailableZones>
</DescribeAvailableResourceResponse>
```

`JSON` format

```
{
    "RequestId": "0041D94C-FB92-4C49-B115-259DA1CE1923",
    "AvailableZones": {
        "AvailableZone": [
            {
                "Status": "Available",
                "RegionId": "cn-hangzhou",
                "AvailableResources": {
                    "AvailableResource": [
                        {
                            "Type": "InstanceType",
                            "SupportedResources": {
                                "SupportedResource": [
                                    {
                                        "Status": "Available",
                                        "Value": "ecs.g5.large",
                                        "StatusCategory": "WithStock"
                                    }
                                ]
                            }
                        }
                    ]
                },
                "ZoneId": "cn-hangzhou-i",
                "StatusCategory": "WithStock"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Invalid.RegionId|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter is invalid.|
|404|Unavailable.Regions|The available regions does not exists|The error message returned because the specified RegionId parameter is invalid.|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|The error message returned because the specified InstanceChargeType parameter is invalid.|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|The error message returned because the specified ResourceType parameter is invalid.|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|The error message returned because the specified IoOptimized parameter is invalid.|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|The error message returned because the specified NetworkCategory parameter is invalid.|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|The error message returned because the specified SpotStrategy parameter is invalid.|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|The error message returned because the specified dedicated host does not exist.|
|404|Invalid.NetworkType|The specified NetworkType is not valid.|The error message returned because the specified NetworkCategory parameter is invalid.|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records|The error message returned because the specified ResourceId parameter is invalid. Check whether the resource exists.|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|The error message returned because none of the InstanceType, Cores, and Memory parameters are specified.|
|403|InvalidParam.Cores|The specified parameter 'Cores' should be empty|The error message returned because the Cores parameter is specified.|
|403|InvalidParam.Memory|The specified parameter 'Memory' should be empty|The error message returned because the Memory parameter is specified.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

