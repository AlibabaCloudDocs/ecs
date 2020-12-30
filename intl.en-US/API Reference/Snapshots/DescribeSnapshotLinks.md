# DescribeSnapshotLinks

You can call this operation to query the snapshot chains of one or more disks. A snapshot chain is a chain of all the snapshots created for a disk. A disk corresponds to a chain of snapshots.

## Description

When you call this operation, take note of the following items:

-   You can specify multiple request parameters such as `RegionId`, `DiskIds`, and `InstanceId` to be queried. Specified parameters have logical AND relations.
-   Only the specified parameters are used as filter conditions. If both `DiskIds` and `SnapshotLinkIds` are set to empty JSON arrays, they are regarded as valid filter conditions and an empty response is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotLinks&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSnapshotLinks|The operation that you want to perform. Set the value to DescribeSnapshotLinks. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId|String|No|i-bp1h6jmbefj2cyqs\*\*\*\*|The ID of the instance. |
|DiskIds|String|No|\["d-bp1d6tsvznfghy7y\*\*\*\*", "d-bp1ippxbaql9zet7\*\*\*\*", ... "d-bp1ib7bcz07lcxa9\*\*\*\*"\]|The IDs of the disks. The value is a JSON array that consists of up to 100 disk IDs. Separate multiple disk IDs with commas \(,\). |
|SnapshotLinkIds|String|No|\["sl-bp1grgphbcc9brb5\*\*\*\*", "sl-bp1c4izumvq0i5bs\*\*\*\*", ... "sl-bp1akk7isz866dds\*\*\*\*"\]|The IDs of the snapshot chains. The value is a JSON array that consists of up to 100 snapshot chain IDs. Separate multiple snapshot chain IDs with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|50|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|50|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|SnapshotLinks|Array of SnapshotLink| |Details about the snapshot chains. |
|SnapshotLink| | | |
|Category|String|standard|The category of the snapshot.

**Note:** This parameter will be removed in the future. We recommend that you use the `InstantAccess`parameter to ensure future compatibility. |
|InstanceId|String|i-bp1h6jmbefj2cyqs\*\*\*\*|The ID of the instance. |
|InstanceName|String|testInstanceName|The name of the instance. |
|InstantAccess|Boolean|false|Indicates whether the instant access feature is enabled. Valid values:

-   true: The instant access feature is enabled. This feature can be enabled only for enhanced SSDs \(ESSDs\).
-   false: The instant access feature is disabled The snapshot is a normal snapshot for which the instant access feature is disabled. |
|RegionId|String|cn-hangzhou|The ID of the region in which the source disk of the snapshot chain is located. |
|SnapshotLinkId|String|sl-2ze0y1jwzpb1geqx\*\*\*\*|The ID of the snapshot chain. |
|SourceDiskId|String|d-bp1d6tsvznfghy7y\*\*\*\*|The ID of the source disk. This parameter is retained even if the source disk is deleted. |
|SourceDiskName|String|testSourceDiskName|The name of the source disk. |
|SourceDiskSize|Integer|40|The capacity of the source disk. Unit: GiB. |
|SourceDiskType|String|data|The category of the source disk. Valid values:

-   system: system disk
-   data: data disk |
|TotalCount|Integer|1|The total number of snapshots. |
|TotalSize|Long|2097152|The total capacity of all snapshots in the snapshot chain. Unit: byte. |
|TotalCount|Integer|9|The total number of snapshot chains. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotLinks
&RegionId=cn-hangzhou
&InstanceId=i-bp1h6jmbefj2cyqs****
&DiskIds=["d-bp1d6tsvznfghy7y****", "d-bp1ippxbaql9zet7****", ... "d-bp1ib7bcz07lcxa9****"]
&SnapshotLinkIds=["sl-bp1grgphbcc9brb5****", "sl-bp1c4izumvq0i5bs****", ... "sl-bp1akk7isz866dds****"]
&PageNumber=1
&PageSize=10
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSnapshotLinksResponse>
      <SnapshotLinks>
            <SnapshotLink>
                  <InstanceName>testInstanceName1</InstanceName>
                  <TotalCount>1</TotalCount>
                  <Category>standard</Category>
                  <SourceDiskSize>40</SourceDiskSize>
                  <InstanceId>i-bp1dh0xo8nucqe1o****</InstanceId>
                  <SnapshotLinkId>sl-bp1hgvjgqo3wn8u7****</SnapshotLinkId>
                  <SourceDiskName>testSourceDiskName1</SourceDiskName>
                  <RegionId></RegionId>
                  <SourceDiskType>system</SourceDiskType>
                  <TotalSize>3806330880</TotalSize>
                  <SourceDiskId>d-bp149tb0mqn0boy6****</SourceDiskId>
            </SnapshotLink>
            <SnapshotLink>
                  <InstanceName>testInstanceName2</InstanceName>
                  <TotalCount>1</TotalCount>
                  <Category>standard</Category>
                  <InstanceId>i-bp1c84ts5f4b6t6z****</InstanceId>
                  <SnapshotLinkId>sl-bp163h35n7endbpv****</SnapshotLinkId>
                  <SourceDiskName>testSourceDiskName2</SourceDiskName>
                  <RegionId></RegionId>
                  <TotalSize>2709520384</TotalSize>
                  <SourceDiskType>data</SourceDiskType>
                  <SourceDiskId>d-bp1cl4hqnh0i2u5h****</SourceDiskId>
            </SnapshotLink>
      </SnapshotLinks>
      <PageNumber>1</PageNumber>
      <PageSize>2</PageSize>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <TotalCount>9</TotalCount>
</DescribeSnapshotLinksResponse>
```

`JSON` format

```
{
    "SnapshotLinks": {
        "SnapshotLink": [
            {
                "InstanceName": "testInstanceName1",
                "TotalCount": 1,
                "Category": "standard",
                "SourceDiskSize": 40,
                "InstanceId": "i-bp1dh0xo8nucqe1o****",
                "SnapshotLinkId": "sl-bp1hgvjgqo3wn8u7****",
                "SourceDiskName": "testSourceDiskName1",
                "RegionId": "",
                "SourceDiskType": "system",
                "TotalSize": 3806330880,
                "SourceDiskId": "d-bp149tb0mqn0boy6****"
            },
            {
                "InstanceName": "testInstanceName2",
                "TotalCount": 1,
                "Category": "standard",
                "InstanceId": "i-bp1c84ts5f4b6t6z****",
                "SnapshotLinkId": "sl-bp163h35n7endbpv****",
                "SourceDiskName": "testSourceDiskName2",
                "RegionId": "",
                "TotalSize": 2709520384,
                "SourceDiskType": "data",
                "SourceDiskId": "d-bp1cl4hqnh0i2u5h****"
            }
        ]
    },
    "PageNumber": 1,
    "PageSize": 1,
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "TotalCount": 2
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegionId|The specified regionId is invalid.|The error message returned because the specified RegionId parameter is invalid.|
|400|InvalidSnapshotLinkIds|The specified snapshotLinkIds is invalid.|The error message returned because the specified SnapshotLinkIds parameter is invalid.|
|400|InvalidDiskIds|The specified diskIds is invalid.|The error message returned because the specified DiskIds parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

