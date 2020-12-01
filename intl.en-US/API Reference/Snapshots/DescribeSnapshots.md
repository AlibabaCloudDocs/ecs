# DescribeSnapshots

You can call this operation to query the details of one or more snapshots of an ECS instance or a disk.

## Description

You can specify multiple request parameters such as `InstanceId`, `DiskId`, and `SnapshotIds` to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions.

When you call an API operation by using Alibaba Cloud CLI, specify request parameter values of different data types in required formats. For more information, see [CLI parameter formats](~~110340~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshots&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSnapshots|The operation that you want to perform. Set the value to DescribeSnapshots. |
|RegionId|String|Yes|cn-hangzhou|The ID of the region. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId|String|No|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|DiskId|String|No|d-bp67acfmxazb4p\*\*\*\*|The ID of the disk. |
|SnapshotLinkId|String|No|sp-bp67acfmxazb4p\*\*\*\*|The ID of the snapshot chain. |
|SnapshotIds|String|No|\["s-bp67acfmxazb4p\*\*\*\*", "s-bp67acfmxazb5p\*\*\*\*", ... "s-bp67acfmxazb6p\*\*\*\*"\]|The IDs of snapshots. The value can be a JSON array that consists of up to 100 snapshot IDs. Separate multiple snapshot IDs with commas \(,\). |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1 |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10 |
|SnapshotName|String|No|testSnapshotName|The name of the snapshot. |
|Status|String|No|all|The status of the snapshot. Default value: all. Valid values:

-   progressing: The snapshot is being created.
-   accomplished: The snapshot is created.
-   failed: The snapshot fails to be created.
-   all: All snapshot statuses. |
|SnapshotType|String|No|all|The type of the snapshot. Valid values:

-   auto: automatic snapshot
-   user: manual snapshot \(also called user-created snapshot\)
-   all: all snapshot types |
|Filter.1.Key|String|No|CreationStartTime|The key of filter 1 used to query resources. Set the value to CreationStartTime. |
|Filter.2.Key|String|No|CreationEndTime|The key of filter 2 used to query resources. Set the value to CreationEndTime. |
|Filter.1.Value|String|No|2019-12-13T17:00Z|The value of filter 1 used to query resources. The value must be the beginning of the time range in which to query created resources. |
|Filter.2.Value|String|No|2019-12-13T22:00Z|The value of filter 2 used to query resources. The value must be the end of the time range in which to query created resources. |
|Usage|String|No|none|Specifies whether the snapshot has been used to create images or disks. Valid values:

-   image: The snapshot has been used to create custom images.
-   disk: The snapshot has been used to create disks.
-   image\_disk: The snapshot has been used to create custom images and data disks.
-   none: The snapshot has not been used to create custom images or disks. |
|SourceDiskType|String|No|Data|The type of the disk for which the snapshot was created. Valid values:

-   System: system disk
-   Data: data disk

**Note:** These values are case-insensitive. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the snapshot. Valid values of N: 1 to 20.

If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the snapshot. Valid values of N: 1 to 20. |
|Encrypted|Boolean|No|false|Specifies whether the snapshot is encrypted. Default value: false. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the snapshot belongs. If this parameter is specified to query resources, up to 1,000 resources that belong to the specified resource group can be displayed in the response. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are set. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made. |
|KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key used by the data disk. |
|Category|String|No|Standard|The category of the snapshot. Valid values:

-   Standard: normal snapshot
-   Flash: local snapshot

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|Snapshots|Array of Snapshot| |Details about the snapshots. |
|Snapshot| | | |
|Category|String|standard|The category of the snapshot.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|CreationTime|String|2020-08-20T14:52:28Z|The time when the snapshot was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|Description|String|testDescription|The description of the snapshot. |
|Encrypted|Boolean|false|Indicates whether the snapshot was encrypted. |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40826X|The KMS key ID corresponding to the data disk. |
|LastModifiedTime|String|2020-08-25T14:18:09Z|The time when the snapshot was last changed. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|ProductCode|String|jxsc000\*\*\*\*|The product code of the Alibaba Cloud Marketplace image. |
|Progress|String|100|The progress of the snapshot creation task. Unit: percent \(%\). |
|RemainTime|Integer|38|The remaining time required to create the snapshot. Unit: seconds. |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group. |
|RetentionDays|Integer|30|The number of days that an automatic snapshot can be retained. |
|SnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|The ID of the snapshot. |
|SnapshotName|String|testSnapshotName|The name of the snapshot. This parameter is returned only if a snapshot name was specified when the snapshot was being created. |
|SnapshotSN|String|64472-116742336-61976\*\*\*\*|The serial number of the snapshot. |
|SnapshotType|String|all|The type of the snapshot. Valid values:

-   auto: automatic snapshot
-   user: manual snapshot \(also called user-created snapshot\)
-   all: all snapshot types |
|SourceDiskId|String|d-bp67acfmxazb4ph\*\*\*\*|The ID of the source disk. This parameter is retained even after the source disk of the snapshot is released. |
|SourceDiskSize|String|2000|The capacity of the source disk. Unit: GiB. |
|SourceDiskType|String|Data|The category of the source disk. Valid values:

-   system
-   data |
|SourceStorageType|String|disk|The category of the source disk.

**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|Status|String|accomplished|The status of the snapshot. Valid values:

-   progressing
-   accomplished
-   failed |
|Tags|Array of Tag| |The tags of the snapshot. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the snapshot. |
|TagValue|String|TestValue|The tag value of the snapshot. |
|Usage|String|none|Indicates whether the snapshot was used to create images or disks. Valid values:

-   image
-   disk
-   image\_disk
-   none |
|TotalCount|Integer|36|The total number of snapshots. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshots
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4p****
&DiskId=d-bp67acfmxazb4p****
&SnapshotIds=["s-bp67acfmxazb4p****", "s-bp67acfmxazb5p****", ... "s-bp67acfmxazb6p****"]
&PageNumber=1
&PageSize=10
&SnapshotName=testSnapshotName
&Status=all
&SnapshotType=all
&Usage=none
&SourceDiskType=Data
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&Encrypted=false
&DryRun=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSnapshotsResponse>
      <PageNumber>1</PageNumber>
      <PageSize>2</PageSize>
      <RequestId>659F91C6-1949-43B0-90C4-B6342CA757D5</RequestId>
      <Snapshots>
            <Snapshot>
                  <CreationTime>2020-08-20T14:52:28Z</CreationTime>
                  <LastModifiedTime>2020-08-25T14:18:09Z</LastModifiedTime>
                  <Progress>100%</Progress>
                  <SnapshotId>s-943ypfg****</SnapshotId>
                  <SnapshotName>auto_20150730_3</SnapshotName>
                  <SourceDiskId>d-944qyqj****</SourceDiskId>
                  <SourceDiskSize>20</SourceDiskSize>
                  <SnapshotType>user</SnapshotType>
                  <SourceDiskType>system</SourceDiskType>
                  <Status>accomplished</Status>
                  <Usage>none</Usage>
            </Snapshot>
            <Snapshot>
                  <CreationTime>2015-07-30T05:00:14Z</CreationTime>
                  <Progress>100%</Progress>
                  <SnapshotId>s-94osg32****</SnapshotId>
                  <SnapshotName>auto_20150730_3</SnapshotName>
                  <SourceDiskId>d-94j355j****</SourceDiskId>
                  <SourceDiskSize>20</SourceDiskSize>
                  <SourceDiskType>system</SourceDiskType>
                  <Status>accomplished</Status>
                  <Usage>none</Usage>
            </Snapshot>
      </Snapshots>
      <TotalCount>36</TotalCount>
</DescribeSnapshotsResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "PageSize": 2,
    "RequestId": "659F91C6-1949-43B0-90C4-B6342CA757D5",
    "Snapshots": {
        "Snapshot": [
            {
                "CreationTime": "2020-08-20T14:52:28Z",
                "LastModifiedTime": "2020-08-25T14:18:09Z",
                "Progress": "100%",
                "SnapshotId": "s-943ypfg****",
                "SnapshotName": "auto_20150730_3",
                "SourceDiskId": "d-944qyqj****",
                "SourceDiskSize": 20,
                "SnapshotType": "user",
                "SourceDiskType": "system",
                "Status": "accomplished",
                "Usage": "none"
            },
            {
                "CreationTime": "2015-07-30T05:00:14Z",
                "Progress": "100%",
                "SnapshotId": "s-94osg32****",
                "SnapshotName": "auto_20150730_3",
                "SourceDiskId": "d-94j355j****",
                "SourceDiskSize": 20,
                "SourceDiskType": "system",
                "Status": "accomplished",
                "Usage": "none"
            }
        ]
    },
    "TotalCount": 36
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidSnapshotIds.Malformed|The amount of specified specified snapshot Ids exceeds the limit.|The error message returned because the specified SnapshotIds parameter is invalid.|
|404|InvalidFilterKey.NotFound| |The error message returned because the specified start time or end time is invalid.|
|404|InvalidUsage|The specifed Usage is not valid|The error message returned because the specified Usage parameter is invalid. The valid values are image, disk, image\_disk, and none.|
|404|InvalidSourceDiskType|The specifed SourceDiskType is not valid|The error message returned because the specified SourceDiskType parameter is invalid.|
|404|InvalidStatus.NotFound|The specified Status is not found|The error message returned because the specified Status parameter does not exist.|
|404|InvalidSnapshotType.NotFound|The specfied SnapshotType is not found|The error message returned because the specified SnapshotType parameter does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the maximum number of the specified tags has been reached.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|404|InvalidSnapshotLinkId.NotFound|The specified snapshot link is not found.|The error message returned because the specified SnapshotLinkId parameter does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

