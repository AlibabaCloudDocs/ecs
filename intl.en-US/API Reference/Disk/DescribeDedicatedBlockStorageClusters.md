# DescribeDedicatedBlockStorageClusters

You can call this operation to query the created dedicated block storage clusters.

## Description

You can specify multiple request parameters. These request parameters can be used to filter query results. The request parameters that you specify have logical AND relations. Only the specified parameters are included in the filter conditions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeDedicatedBlockStorageClusters&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDedicatedBlockStorageClusters|The operation that you want to perform. Set the value to DescribeDedicatedBlockStorageClusters. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the dedicated block storage cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|No|cn-hangzhou-h|The zone ID of the dedicated block storage cluster. You can call the [DescribeZones](~~25610~~) operation to query the zone list. |
|DedicatedBlockStorageClusterId.N|RepeatList|No|dbsc-bp12wlf6am0v\*\*\*\*|The ID of dedicated block storage cluster N.

This parameter is required if you want to query one or more specified clusters. For example, if you want to query the `dbsc-bp12wlf6am0v****` and `dbsc-bp12wlf6abcd****` clusters, specify this parameter in the following manner:

```

&DedicatedBlockStorageClusterId.1=dbsc-bp12wlf6am0v****
&DedicatedBlockStorageClusterId.2=dbsc-bp12wlf6abcd****
                                
``` |
|Status.N|RepeatList|No|Running|Status N of the dedicated block storage cluster. Valid values:

-   Preparing: The cluster is pending delivery.
-   Running: The cluster is running.
-   Expired: The cluster expires.
-   Offline: The cluster is offline.

Valid values of N: 1 to 4.

This parameter is required if you want to query clusters in a specified state. For example, if you want to query clusters in the Preparing and Running states, specify this parameter in the following manner:

```

&Status.1=Preparing
&Status.2=Running
                                
``` |
|Category|String|No|cloud\_essd|The category of the disk on the dedicated block storage cluster. Only enhanced SSDs \(ESSDs\) can be created on dedicated block storage clusters, so set this parameter to cloud\_essd. |
|NextToken|String|No|AAAAAdDWBF2|The query token.

Use `NextToken` to configure the query token. Set this parameter to the `NextToken` value returned in the last call to the DescribeDedicatedBlockStorageClusters operation. Then, use `MaxResults` to specify the maximum number of entries to return on each page. |
|MaxResults|Integer|No|10|The maximum number of entries to return on each page. Valid values: 1 to 500.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DedicatedBlockStorageClusters|Array of DedicatedBlockStorageCluster| |The dedicated block storage clusters. |
|DedicatedBlockStorageCluster| | | |
|Category|String|cloud\_essd|The category of the disk on the dedicated block storage cluster. Valid value: cloud\_essd. |
|CreateTime|String|2021-03-06 10:16:34|The time when the dedicated block storage cluster was created. |
|DedicatedBlockStorageClusterCapacity|Struct| |The storage capacity of the dedicated block storage cluster. |
|AvailableCapacity|Long|40|The available capacity of the dedicated block storage cluster. Unit: TB. |
|TotalCapacity|Long|72|The total capacity of the dedicated block storage clusters. Unit: TB. |
|DedicatedBlockStorageClusterId|String|dbsc-xxxxxx|The ID of the dedicated block storage cluster. |
|DedicatedBlockStorageClusterName|String|myDBSCCluster|The name of the dedicated block storage cluster. |
|Description|String|myDBSCCluster|The description of the dedicated block storage cluster. |
|ExpiredTime|String|2022-03-06 10:16:34|The expiration time of the dedicated block storage cluster. |
|PerformanceLevel|String|PL1|The performance level of the ESSD. Valid value: PL1.

For information about the performance parameters of PL1 ESSDs, see [Enhanced ESSDs](~~122389~~). |
|Status|String|Running|The status of the dedicated block storage cluster. Valid values:

-   Preparing: The cluster is pending delivery.
-   Running: The cluster is running.
-   Expired: The cluster expires.
-   Offline: The cluster is offline. |
|ZoneId|String|cn-hangzhou-h|The zone ID of the dedicated block storage cluster. |
|NextToken|String|AAAAAdDWBF2|The query token returned in this call. |
|RequestId|String|11B55F58-D3A4-4A9B-9596-342420D02FF8|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeDedicatedBlockStorageClusters
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

Sample success responses

`XML` format

```
<DescribeDedicatedBlockStorageClustersResponse>
      <DedicatedBlockStorageClusters>
            <DedicatedBlockStorageCluster>
                  <Status>Running</Status>
                  <Description>myDBSCCluster</Description>
                  <ZoneId>cn-hangzhou-h</ZoneId>
                  <DedicatedBlockStorageClusterId>dbsc-xxxxxx</DedicatedBlockStorageClusterId>
                  <PerformanceLevel>PL1</PerformanceLevel>
                  <CreateTime>2021-03-06 10:16:34</CreateTime>
                  <ExpiredTime>2022-03-06 10:16:34</ExpiredTime>
                  <Category>cloud_essd</Category>
                  <DedicatedBlockStorageClusterName>myDBSCCluster</DedicatedBlockStorageClusterName>
                  <DedicatedBlockStorageClusterCapacity>
                        <AvailableCapacity>40</AvailableCapacity>
                        <TotalCapacity>72</TotalCapacity>
                  </DedicatedBlockStorageClusterCapacity>
            </DedicatedBlockStorageCluster>
      </DedicatedBlockStorageClusters>
      <NextToken>AAAAAdDWBF2</NextToken>
      <RequestId>11B55F58-D3A4-4A9B-9596-342420D02FF8</RequestId>
</DescribeDedicatedBlockStorageClustersResponse>
```

`JSON` format

```
{
    "DedicatedBlockStorageClusters": {
        "DedicatedBlockStorageCluster": [{
            "Status": "Running",
            "Description": "myDBSCCluster",
            "ZoneId": "cn-hangzhou-h",
            "DedicatedBlockStorageClusterId": "dbsc-xxxxxx",
            "PerformanceLevel": "PL1",
            "CreateTime": "2021-03-06 10:16:34",
            "ExpiredTime": "2022-03-06 10:16:34",
            "Category": "cloud_essd",
            "DedicatedBlockStorageClusterName": "myDBSCCluster",
            "DedicatedBlockStorageClusterCapacity": {
                "AvailableCapacity": "40",
                "TotalCapacity": "72"
            }
        }]
    },
    "NextToken": "AAAAAdDWBF2",
    "RequestId": "11B55F58-D3A4-4A9B-9596-342420D02FF8"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidStatus.ValueNotSupported|%s|The error message returned because the operation is not supported while the resource is in the current state.|
|404|InvalidRegionId.NotFound|The specified region does not exist.|The error message returned because the specified RegionId parameter does not exist. Check whether the service is available in the specified region.|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|The error message returned because the specified ZoneId parameter does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

