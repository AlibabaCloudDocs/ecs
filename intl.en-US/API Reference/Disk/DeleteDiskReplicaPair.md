# DeleteDiskReplicaPair

You can call this operation to delete a replication relationship.

Only replication relationships in the **Suspended** \(`paused`\) state can be deleted. This operation deletes only the specified replication relationship and does not affect the associated primary or secondary disk.

You must delete a replication relationship from the region where the primary disk is located. After the replication relationship is deleted, the secondary disk can be attached, read, written, or resized.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteDiskReplicaPair&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteDiskReplicaPair|The operation that you want to perform. Set the value to DeleteReplicaPair. |
|RegionId|String|Yes|cn-beijing|The region ID of the primary disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ReplicaPairId|String|Yes|rp-dsaf233kj23j2j35\*\*\*\*|The ID of the replication relationship. You can call the [DescribeDiskReplicaPairs](~~209201~~) operation to query the IDs of replication relationships. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|20758A-585D-4A41-A9B2-28DA8F4F534F|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteDiskReplicaPair
&RegionId=cn-beijing
&ReplicaPairId=rp-dsaf233kj23j2j35****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteReplicaPairResponse>
      <RequestId>20758A-585D-4A41-A9B2-28DA8F4F534F</RequestId>
</DeleteReplicaPairResponse>
```

`JSON` format

```
{
    "RequestId": "20758A-585D-4A41-A9B2-28DA8F4F534F"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|The error message returned because the specified RegionId parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

