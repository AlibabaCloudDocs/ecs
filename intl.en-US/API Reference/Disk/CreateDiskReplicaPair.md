# CreateDiskReplicaPair

You can call this operation to create a replication relationship to asynchronously replicate data between disks.

## Description

Asynchronous Block Storage Replication \(ABSR\) is a feature that can asynchronously replicate data from one cloud disk to another cloud disk within a different region. This approach provides data redundancy and reduces or prevents data loss if an exception occurs on the primary disk \(source disk\). Services can be resumed based on the secondary disk \(destination disk\). This way, service continuity is ensured. For more information, see [Asynchronous Block Storage Replication](~~208904~~).

To use ABSR to replicate data between disks, you must call the CreateDiskReplicaPair operation to create a replication relationship, and then call the [StartDiskReplicaPair](~~209199~~) operation to start the relationship.

Before you can create a replication relationship for a primary disk, you must create a secondary disk in the destination region. The secondary disk must have the same specifications and capacity as the primary disk. You can call the [DescribeDisks](~~25514~~) operation to query the specifications and capacity of the primary disk, and call the [CreateDisk](~~25513~~)operation to create the secondary disk in the destination region.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateDiskReplicaPair&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateDiskReplicaPair|The operation that you want to perform. Set the value to CreateDiskReplicaPair. |
|DestinationDiskId|String|Yes|d-asdfjl2342kj2l3k4\*\*\*\*|The ID of the secondary disk. |
|DestinationRegionId|String|Yes|cn-shanghai|The region ID of the secondary disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DiskId|String|Yes|d-bp131n0q38u3a4zi\*\*\*\*|The ID of the primary disk. |
|PairName|String|Yes|TestReplicaPair|The name of the replication relationship. |
|RegionId|String|Yes|cn-beijing|The region ID of the primary disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Description|String|No|TestReplicaPairDescription|The description of the replication relationship. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PairId|String|rp-dsaf233kj23j2j35\*\*\*\*|The ID of the replication relationship. |
|RequestId|String|20758A-585D-4A41-A9B2-28DA8F4F534F|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateDiskReplicaPair
&DiskId=d-bp1famypsnar20bv****
&PairName=TestReplicaPair
&RegionId=cn-beijing
&DestinationRegionId=cn-shanghai
&DestinationDiskId=d-asdfjl2342kj2l3k4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateDiskReplicaPairResponse>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
        <PairId>rp-dsaf233kj23j2j3****</PairId>
</CreateDiskReplicaPairResponse>
```

`JSON` format

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "PairId": "rp-dsaf233kj23j2j3****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist.|
|403|IncorrectDiskStatus|The operation is not supported in this status.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|400|IncompleteParamter|Some fields can not be null in this request.|The error message returned because some required parameters are not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

