# DescribeDiskReplicaPairs

You can call this operation to query replication relationships in a region.

## Description

In the response, you can view all the replication relationships in the specified region as well as the associated primary and secondary disks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeDiskReplicaPairs&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeDiskReplicaPairs|The operation that you want to perform. Set the value to DescribeDiskReplicaPairs. |
|RegionId|String|Yes|cn-beijing|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|MaxResults|Integer|No|50|The maximum number of entries to return on each page. Valid values: 1 to 500.

 Default value: 10. |
|NextToken|String|No|AAAAAdDWBF2\*\*\*\*|The query token.

 Use `NextToken` to configure the query token. Set this parameter to the `NextToken` value returned in the last call to the `DescribeDiskReplicaPairs` operation. Then, use `MaxResults` to specify the maximum number of entries to return on each page. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|AAAAAdDWBF2\*\*\*\*|The query token returned in this call. |
|ReplicaPairs|Array of ReplicaPair| |Details about the replication relationships. |
|ReplicaPair| | | |
|Description|String|TestReplicaPairDescription|The description of the replication relationship. |
|DestinationDiskId|String|d-asdfjl2342kj2l3k4\*\*\*\*|The ID of the secondary disk. |
|DestinationRegion|String|cn-shanghai|The region ID of the secondary disk. |
|PairName|String|TestReplicaPair|The name of the replication relationship. |
|ReplicaPairId|String|rp-dsaf233kj23j2j35\*\*\*\*|The ID of the replication relationship. |
|SourceDiskId|String|d-bp131n0q38u3a4zi\*\*\*\*|The ID of the primary disk. |
|SourceRegion|String|cn-beijing|The region ID of the primary disk. |
|Status|String|active|The status of the replication relationship. Valid values:

 -   `inactive`
-   `active`
-   `paused`
-   `pausing`
-   `starting`
-   `deleting` |
|RequestId|String|E69EF3CC-94CD-42E7-8926-F133B86387C0|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeDiskReplicaPairs
&RegionId=cn-beijing
&MaxResults=50
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeDiskReplicaPairsResponse>
      <ReplicaPairs>
            <ReplicaPair>
                  <Status>active</Status>
                  <Description>TestReplicaPairDescription</Description>
                  <DestinationDiskId>d-asdfjl2342kj2l3k4****</DestinationDiskId>
                  <PairName>TestReplicaPair</PairName>
                  <DestinationRegion>cn-shanghai</DestinationRegion>
                  <ReplicaPairId>rp-dsaf233kj23j2j35****</ReplicaPairId>
                  <SourceRegion>cn-beijing</SourceRegion>
                  <SourceDiskId>d-bp131n0q38u3a4zi****</SourceDiskId>
            </ReplicaPair>
      </ReplicaPairs>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</DescribeDiskReplicaPairsResponse>
```

`JSON` format

```
{
	"ReplicaPairs": {
		"ReplicaPair": [{
			"Status": "active",
			"Description": "TestReplicaPairDescription",
			"DestinationDiskId": "d-asdfjl2342kj2l3k4****",
			"PairName": "TestReplicaPair",
			"DestinationRegion": "cn-shanghai",
			"ReplicaPairId": "rp-dsaf233kj23j2j35****",
			"SourceRegion": "cn-beijing",
			"SourceDiskId": "d-bp131n0q38u3a4zi****"
		}]
	},
	"NextToken": "AAAAAdDWBF2****",
	"RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|IncompleteParamter|Some fields can not be null in this request.|The error message returned because some required parameters are not specified.|
|400|InvalidParamter|Some parameters are invalid in this request.|The error message returned because the request contains invalid parameters.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

