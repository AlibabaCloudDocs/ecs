# CreateDedicatedBlockStorageCluster

You can call this operation to create dedicated block storage clusters.

## Description

Dedicated Block Storage Cluster is a block storage service that offers physical isolation and allows you exclusive access to the entire block storage cluster. For more information, see [What is Dedicated Block Storage Cluster?](~~208883~~)

Disks created on a dedicated block storage cluster can be attached only to ECS instances within the same zone. Before you create a dedicated block storage cluster, you must plan the region and zone where to create the cluster.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateDedicatedBlockStorageCluster&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDedicatedBlockStorageCluster|The operation that you want to perform. Set the value to CreateDedicatedBlockStorageCluster. |
|Capacity|Integer|Yes|72|The capacity of the dedicated block storage cluster. Valid values: 72 to 2304. Unit: TB. |
|Category|String|Yes|cloud\_essd|The category of the disk that can be created on the dedicated block storage cluster. Set the value to cloud\_essd. Only enhanced SSDs \(ESSDs\) can be created on the dedicated block storage cluster. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the dedicated block storage cluster. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ZoneId|String|Yes|cn-hangzhou-h|The zone ID of the dedicated block storage cluster. You can call the [DescribeZones](~~25610~~) operation to query the zone list. |
|DedicatedBlockStorageClusterName|String|No|myDBSCCluster|The name of the dedicated block storage cluster. |
|Description|String|No|myDBSCCluster|The description of the dedicated block storage cluster. |
|PerformanceLevel|String|No|PL1|The performance level of the ESSD. Set the value to PL1.

For information about the performance parameters of PL1 ESSDs, see [Enhanced ESSDs](~~122389~~). |
|Period|Integer|No|2|The subscription period of the dedicated block storage cluster. The unit is specified by the `PeriodUnit` parameter.

-   When the `PeriodUnit` parameter is set to `Year`, valid values of the `Period` parameter are 1, 2, 3, and 4.
-   When the `PeriodUnit` parameter is set to `Month`, valid values of the `Period` parameter are 6, 7, 8, 9, 10, and 11.

Default value: 6. |
|PeriodUnit|String|No|Year|The unit of the subscription period. Valid values:

-   Year
-   Month

Default value: Month. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate a token, but you must ensure that it is unique among different requests.

The `ClientToken` value can contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DedicatedBlockStorageClusterId|String|dbsc-xxxxx|The ID of the dedicated block storage cluster. |
|DedicatedBlockStorageClusterOrderId|String|50155660025\*\*\*\*|The ID of the order. |
|RequestId|String|20758A-585D-4A41-A9B2-28DA8F4F534F|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateDedicatedBlockStorageCluster
&Capacity=72
&Category=cloud_essd
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-h
&<Common Request Parameters>
```

Sample success responses

`XML` format

```
<CreateDedicatedBlockStorageClusterResponse>
      <DedicatedBlockStorageClusterOrderId>50155660025****</DedicatedBlockStorageClusterOrderId>
      <RequestId>20758A-585D-4A41-A9B2-28DA8F4F534F</RequestId>
      <DedicatedBlockStorageClusterId>dbsc-xxxxx</DedicatedBlockStorageClusterId>
</CreateDedicatedBlockStorageClusterResponse>
```

`JSON` format

```
{
    "DedicatedBlockStorageClusterOrderId": "50155660025****",
    "RequestId": "20758A-585D-4A41-A9B2-28DA8F4F534F",
    "DedicatedBlockStorageClusterId": "dbsc-xxxxx"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|The error message returned because the specified ZoneId parameter does not exist.|
|404|InvalidRegionId.NotFound|The specified region does not exist.|The error message returned because the specified RegionId parameter does not exist. Check whether the service is available in the specified region.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

