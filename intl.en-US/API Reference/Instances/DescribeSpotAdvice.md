# DescribeSpotAdvice

Queries information such as the average release rate and the percentage of the average price relative to the pay-as-you-go instance price that is generated for preemptible instances in the last 30 days in a specified region.

## Description

-   You can call this operation to query information that is generated for preemptible instances in the last 30 days and select suitable instance types based on the query results. The information that you can query by calling this operation includes:
    -   Average release rate of preemptible instances
    -   Percentage of the average preemptible instance price relative to the pay-as-you-go instance price
    -   Average preemptible instance price that is calculated based on the preceding percentage
-   This operation is applicable only to I/O optimized preemptible instances that are located in virtual private clouds \(VPCs\).
-   You can use one of the following methods to query information that is generated for preemptible instances in the last 30 days:
    -   Set the `Cores` and `Memory` parameters or the `MinCores` and `MinMemory` parameters to query information about instance types that have the specified number of vCPUs and memory size.
    -   Set the `InstanceTypes.N` parameter to query information of the specified instance types.
    -   Set the `Cores` and `Memory` parameters or the `MinCores` and `MinMemory` parameters, and set the `InstanceTypeFamily` or `InstanceFamilyLevel` parameter to query information of the instance types that have the specified number of vCPUs and memory size within the specified instance family or at the specified instance family level.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeSpotAdvice&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|DescribeSpotAdvice|The operation that you want to perform. Set the value to DescribeSpotAdvice. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Cores|Integer|No|2|The number of vCPUs of the instance type. For information about the valid values, see [Instance families](~~25378~~). |
|Memory|Float|No|8.0|The memory size of the instance type. Unit: GiB. For information about the valid values, see [Instance families](~~25378~~). |
|MinCores|Integer|No|2|The minimum number of vCPUs of the instance type. For information about the valid values, see [Instance families](~~25378~~). |
|MinMemory|Float|No|8.0|The minimum memory size of the instance type. For information about the valid values, see [Instance families](~~25378~~). |
|ZoneId|String|No|cn-hangzhou-i|The ID of the zone.

 This parameter is empty by default, which indicates that all zones in the specified region are queried. |
|InstanceTypes.N|RepeatList|No|ecs.c5.large|Instance type N. Valid values of N: 1 to 10. For information about the valid values, see [Instance families](~~25378~~). |
|InstanceTypeFamily|String|No|ecs.c5|The instance family. For information about the valid values, see [Instance families](~~25378~~). |
|InstanceFamilyLevel|String|No|EntryLevel|The level of the instance family. Valid values:

 -   EntryLevel
-   EnterpriseLevel
-   CreditEntryLevel. For more information, see [Burstable instance overview](~~59977~~).

 This parameter is empty by default, which indicates that instance families of all levels are queried. |
|GpuSpec|String|No|NVIDIA T4|The GPU type. Valid values:

 -   NVIDIA P4
-   NVIDIA T4
-   NVIDIA P100
-   NVIDIA V100
-   NVIDIA A100

 This parameter is empty by default, which indicates that all GPU types are queried. For more information, see [GPU-accelerated compute optimized instance types](~~108496~~). |
|GpuAmount|Integer|No|2|The number of GPUs per GPU-accelerated instance. For information about the valid values, see [GPU-accelerated compute optimized instance types](~~108496~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AvailableSpotZones|Array of AvailableSpotZone| |Details about preemptible instances in the zones of the specified region.

 **Note:** The return values are sorted based on the historical percentages of average preemptible instance prices relative to pay-as-you-go instance prices for instance types. |
|AvailableSpotZone| | | |
|AvailableSpotResources|Array of AvailableSpotResource| |Details about preemptible instances in the last 30 days, including release rates and percentages of average preemptible instance prices relative to pay-as-you-go instance prices. |
|AvailableSpotResource| | | |
|AverageSpotDiscount|Integer|20|The percentage of the average preemptible instance relative to the pay-as-you-go instance price in the last 30 days. Unit: percent \(%\). Valid values: 1 to 100.

 You can calculate the average preemptible instance price based on the return value. For example, if the pay-as-you-go instance price is 1 and the return value of this parameter is 20, the average preemptible instance price in the last 30 days is 0.2. |
|InstanceType|String|ecs.c5.large|The instance type. |
|InterruptRateDesc|String|0-3%|The release rate range of preemptible instances in the last 30 days, which corresponds to the `InterruptionRate` value. Valid values:

 -   0-3%
-   3-5%
-   5-10%
-   10-100% |
|InterruptionRate|Float|0|The average release rate of preemptible instances in the last 30 days. Unit: percent \(%\). |
|ZoneId|String|cn-hangzhou-i|The ID of the zone. |
|RegionId|String|cn-hangzhou|The ID of the region. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeSpotAdvice
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-i
&InstanceTypes.1=ecs.c5.large
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSpotAdviceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <AvailableSpotZones>
            <AvailableSpotZone>
                  <ZoneId>cn-hangzhou-i</ZoneId>
            </AvailableSpotZone>
            <AvailableSpotZone>
                  <AvailableSpotResources>
                        <AvailableSpotResource>
                              <InterruptRateDesc>0-3%</InterruptRateDesc>
                              <InstanceType>ecs.c5.large</InstanceType>
                              <AverageSpotDiscount>20</AverageSpotDiscount>
                              <InterruptionRate>0</InterruptionRate>
                        </AvailableSpotResource>
                  </AvailableSpotResources>
            </AvailableSpotZone>
      </AvailableSpotZones>
      <RegionId>cn-hangzhou</RegionId>
</DescribeSpotAdviceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "AvailableSpotZones": {
        "AvailableSpotZone": [
            {
                "ZoneId": "cn-hangzhou-i"
            }, 
            {
                "AvailableSpotResources": {
                    "AvailableSpotResource": [
                        {
                            "InterruptRateDesc": "0-3%", 
                            "InstanceType": "ecs.c5.large", 
                            "AverageSpotDiscount": "20", 
                            "InterruptionRate": "0"
                        }
                    ]
                }
            }
        ]
    }, 
    "RegionId": "cn-hangzhou"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Invalid.RegionId|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter is invalid.|
|404|Unavailable.Regions|The available regions does not exists|The error message returned because the specified RegionId parameter is invalid.|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|The error message returned because the specified ResourceType parameter is invalid.|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|The error message returned because the specified DestinationResource parameter is invalid.|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|The error message returned because the specified IoOptimized parameter is invalid.|
|404|Invalid.NetworkType|The specified NetworkType is not valid.|The error message returned because the specified NetworkType parameter is invalid.|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist in our records.|The error message returned because the specified dedicated host does not exist in the current region.|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|The error message returned because the InstanceTypes.N, Cores, and Memory parameters are all empty.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

