# DescribeSnapshots

Queries the details of one or more snapshots of an Elastic Compute Service \(ECS\) instance or disk.

## Description

You can specify multiple request parameters such as `InstanceId`, `DiskId`, and `SnapshotIds` to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions.

When you call an API operation by using Alibaba Cloud Command Line Interface \(CLI\), you must specify request parameter values of different data types in required formats. For more information, see [Parameter format overview](~~110340~~).

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

 Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page. Maximum value: 100.

 Default value: 10. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the query. Obtain the NextToken value from the response to the previous request. |
|MaxResults|Integer|No|10|The maximum number of entries to return on each page.

 Maximum value: 100.

 Default value: 10. |
|SnapshotName|String|No|testSnapshotName|The name of the snapshot. |
|Status|String|No|all|The status of the snapshot. Default value: all. Valid values:

 -   progressing: The snapshot is being created.
-   accomplished: The snapshot is created.
-   failed: The snapshot fails to be created.
-   all: all snapshot statuses. |
|SnapshotType|String|No|all|The type of the snapshot. Default value: all. Valid values:

 -   auto: automatic snapshot
-   user: manual snapshot \(also called user-created snapshot\)
-   all: all snapshot types |
|Filter.1.Key|String|No|CreationStartTime|The key of filter 1 used to query resources. Set the value to `CreationStartTime`. You can set both `Filter.1.Key` and `Filter.1.Value` to specify the beginning of the time range in which to query created resources. |
|Filter.2.Key|String|No|CreationEndTime|The key of filter 2 used to query resources. Set the value to `CreationEndTime`. You can set both `Filter.2.Key` and `Filter.2.Value` to specify the end of the time range in which to query created resources. |
|Filter.1.Value|String|No|2019-12-13T17:00Z|The value of filter 1 used to query resources. Set the value to the beginning of the time range to query. When you specify this parameter, you must also specify `Filter.1.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Filter.2.Value|String|No|2019-12-13T22:00Z|The value of filter 2 used to query resources. Set the value to the end of the time range to query. When you specify this parameter, you must also specify `Filter.2.Key`. Specify the time in the `yyyy-MM-ddTHH:mmZ` format. The time must be in UTC. |
|Usage|String|No|none|Specifies whether the snapshot has been used to create images or disks. Valid values:

 -   image: The snapshot has been used to create custom images.
-   disk: The snapshot has been used to create disks.
-   image\_disk: The snapshot has been used to create custom images and data disks.
-   none: The snapshot has not been used to create custom images or disks. |
|SourceDiskType|String|No|Data|The type of the source disk for which the snapshot was created. Valid values:

 -   System: system disk
-   Data: data disk

 **Note:** These values are case-insensitive. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the snapshot. Valid values of N: 1 to 20.

 If a single tag is specified to query resources, up to 1,000 resources that are bound with this tag can be displayed in the response. If multiple tags are specified to query resources, up to 1,000 resources that are bound with all these tags can be displayed in the response. To query more than 1,000 resources that are bound with specified tags, call the [ListTagResources](~~110425~~) operation. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the snapshot. Valid values of N: 1 to 20. |
|Encrypted|Boolean|No|false|Specifies whether the snapshot is encrypted. Default value: false. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the snapshot belongs. If this parameter is specified to query resources, up to 1,000 resources that belong to the specified resource group can be displayed in the response. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Valid values:

 -   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are specified. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made. |
|KMSKeyId|String|No|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the Key Management Service \(KMS\) key used by the data disk. |
|Category|String|No|Standard|The category of the snapshot. Valid values:

 -   Standard: normal snapshot
-   Flash: local snapshot

 The local snapshot feature is replaced by the instant access feature. When you specify this parameter, take note of the following items:

 -   If you have used local snapshots before December 14, 2020, you can use this parameter.
-   If you have not used local snapshots before December 14, 2020, you cannot use this parameter.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|Snapshots|Array of Snapshot| |Details about the snapshots. |
|Snapshot| | | |
|Category|String|standard|The category of the snapshot.

 **Note:** This parameter will be removed in the future. We recommend that you use the `InstantAccess`parameter to ensure future compatibility. |
|CreationTime|String|2020-08-20T14:52:28Z|The time when the snapshot was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|Description|String|testDescription|The description of the snapshot. |
|Encrypted|Boolean|false|Indicates whether the snapshot was encrypted. |
|InstantAccess|Boolean|false|Indicates whether the instant access feature was enabled. Valid values:

 -   true: The instant access feature was enabled. This feature can be enabled only for enhanced SSDs \(ESSDs\).
-   false: The instant access feature was disabled. The snapshot is a normal snapshot for which the instant access feature was disabled. |
|InstantAccessRetentionDays|Integer|30|Indicates the duration of the instant access feature. The instant access feature is automatically disabled when the specified duration expires.

 By default, the value of this parameter is the same as that of `RetentionDays`. |
|KMSKeyId|String|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|The ID of the KMS key used by the data disk. |
|LastModifiedTime|String|2020-08-25T14:18:09Z|The time when the snapshot was last changed. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|ProductCode|String|jxsc000\*\*\*\*|The product code of the Alibaba Cloud Marketplace image. |
|Progress|String|100%|The progress of the snapshot creation task. Unit: percent \(%\). |
|RemainTime|Integer|38|The remaining time required to create the snapshot. Unit: seconds. |
|ResourceGroupId|String|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the snapshot belongs. |
|RetentionDays|Integer|30|The number of days that an automatic snapshot can be retained. |
|SnapshotId|String|s-bp67acfmxazb4p\*\*\*\*|The ID of the snapshot. |
|SnapshotName|String|testSnapshotName|The name of the snapshot. This parameter is returned only if a snapshot name was specified when the snapshot was created. |
|SnapshotSN|String|64472-116742336-61976\*\*\*\*|The serial number of the snapshot. |
|SnapshotType|String|all|The type of the snapshot. Valid values:

 -   auto or timer: automatic snapshot
-   user: manual snapshot
-   all: all snapshot types |
|SourceDiskId|String|d-bp67acfmxazb4ph\*\*\*\*|The ID of the source disk for which the snapshot was created. This parameter is retained even after the source disk of the snapshot is released. |
|SourceDiskSize|String|40|The capacity of the source disk. Unit: GiB. |
|SourceDiskType|String|system|The category of the source disk. Valid values:

 -   system
-   data |
|SourceStorageType|String|disk|The type of the source disk.

 **Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|Status|String|accomplished|The status of the snapshot. Valid values:

 -   progressing
-   accomplished
-   failed |
|Tags|Array of Tag| |The tags of the snapshot. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the snapshot. |
|TagValue|String|TestValue|The tag value of the snapshot. |
|Usage|String|image|Indicates whether the snapshot has been used to create images or disks. Valid values:

 -   image
-   disk
-   image\_disk
-   none |
|TotalCount|Integer|1|The total number of snapshots. |

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
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>10</PageSize>
      <NextToken>caeba0bbb2be03f84eb48b699f0a4883</NextToken>
      <PageNumber>1</PageNumber>
      <Snapshots>
            <Snapshot>
                  <Status>accomplished</Status>
                  <InstantAccess>false</InstantAccess>
                  <Progress>100%</Progress>
                  <Usage>image</Usage>
                  <Description>testDescription</Description>
                  <Category>standard</Category>
                  <KMSKeyId>0e478b7a-4262-4802-b8cb-00d3fb40****</KMSKeyId>
                  <ProductCode>jxsc000****</ProductCode>
                  <Encrypted>false</Encrypted>
                  <SnapshotName>testSnapshotName</SnapshotName>
                  <SourceDiskId>d-bp67acfmxazb4ph****</SourceDiskId>
                  <SourceStorageType>disk</SourceStorageType>
                  <SnapshotId>s-bp67acfmxazb4p****</SnapshotId>
                  <SnapshotSN>64472-116742336-61976****</SnapshotSN>
                  <SourceDiskSize>40</SourceDiskSize>
                  <CreationTime>2020-08-20T14:52:28Z</CreationTime>
                  <LastModifiedTime>2020-08-25T14:18:09Z</LastModifiedTime>
                  <SnapshotType>all</SnapshotType>
                  <SourceDiskType>system</SourceDiskType>
                  <Tags>
            </Tags>
            </Snapshot>
      </Snapshots>
</DescribeSnapshotsResponse>
```

`JSON` format

```
{
	"TotalCount": 1,
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PageSize": 10,
	"NextToken": "caeba0bbb2be03f84eb48b699f0a4883",
	"PageNumber": 1,
	"Snapshots": {
		"Snapshot": [
			{
				"Status": "accomplished",
				"InstantAccess": false,
				"Progress": "100%",
				"Usage": "image",
				"Description": "testDescription",
				"Category": "standard",
				"KMSKeyId": "0e478b7a-4262-4802-b8cb-00d3fb40****",
				"ProductCode": "jxsc000****",
				"Encrypted": false,
				"SnapshotName": "testSnapshotName",
				"SourceDiskId": "d-bp67acfmxazb4ph****",
				"SourceStorageType": "disk",
				"SnapshotId": "s-bp67acfmxazb4p****",
				"SnapshotSN": "64472-116742336-61976****",
				"SourceDiskSize": 40,
				"CreationTime": "2020-08-20T14:52:28Z",
				"LastModifiedTime": "2020-08-25T14:18:09Z",
				"SnapshotType": "all",
				"SourceDiskType": "system",
				"Tags": {
					"Tag": []
				}
			}
		]
	}
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
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags exceeds the upper limit.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|404|InvalidSnapshotLinkId.NotFound|The specified snapshot link is not found.|The error message returned because the specified SnapshotLinkId parameter does not exist.|
|403|InvalidSnapshotCategory.Malformed|The specified Category is not valid.|The error message returned because the specified Category parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

