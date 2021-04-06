# DescribeSnapshotGroups

You can call this operation to query the information of one or more instance snapshots.

## Description

You can specify multiple request parameters such as `InstanceId`, `SnapshotGroupId.N`, and `Status.N` to be queried. Specified parameters have logical AND relations. Only the specified parameters are included in the filter conditions.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeSnapshotGroups&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSnapshotGroups|The operation that you want to perform. Set the value to DescribeSnapshotGroups. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId|String|No|i-j6ca469urv8ei629\*\*\*\*|The ID of the instance. |
|SnapshotGroupId.N|RepeatList|No|ssg-j6ciyh3k52qp7ovm\*\*\*\*|The ID of instance snapshot N. Valid values of N: 1 to 10. |
|Status.N|RepeatList|No|accomplished|The status of instance snapshot N. Valid values:

 -   progressing: The instance snapshot is being created.
-   accomplished: The instance snapshot is created.
-   failed: The instance snapshot fails to be created.

 Valid values of N: 1 to 3. |
|Name|String|No|testName|The name of the instance snapshot. |
|NextToken|String|No|caeba0bbb2be03f84eb48b699f0a4883|The query token. Set this parameter to the NextToken value that is returned in the last API call. |
|MaxResults|Integer|No|10|The number of entries to return on each page.

 Maximum value: 100.

 Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|NextToken|String|caeba0bbb2be03f84eb48b699f0a4883|The token used to start the next query. |
|RequestId|String|3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A|The ID of the request. |
|SnapshotGroups|Array of SnapshotGroup| |Details about the instance snapshots. |
|SnapshotGroup| | | |
|CreationTime|String|2021-03-23T10:58:48Z|The time when the instance snapshot was created. |
|Description|String|This is description.|The description. |
|InstanceId|String|i-j6ca469urv8ei629\*\*\*\*|The ID of the instance for which the instance snapshot was created. |
|Name|String|testName|The name of the instance snapshot. |
|ProgressStatus|String|null|**Note:** This parameter is unavailable. |
|SnapshotGroupId|String|ssg-j6ciyh3k52qp7ovm\*\*\*\*|The ID of the instance snapshot. |
|Snapshots|Array of Snapshot| |Details about the snapshots contained in the instance snapshot. |
|Snapshot| | | |
|InstantAccess|Boolean|true|Indicates whether the instant access feature is enabled. Valid values:

 -   true: The instant access feature is enabled. This feature can be enabled only for enhanced SSDs \(ESSDs\).
-   false: The instant access feature is disabled. The snapshot is a normal snapshot for which the instant access feature is disabled. |
|InstantAccessRetentionDays|Integer|3|The retention period of the instant access feature. After the retention period ends, the snapshot is automatically released. |
|Progress|String|100%|The progress of the snapshot creation task. Unit: percent \(%\). |
|SnapshotId|String|s-j6cbzmrlbf09w72q\*\*\*\*|The ID of the snapshot. |
|SourceDiskId|String|d-j6c3ogynmvpi6wy7\*\*\*\*|The ID of the source disk. This parameter is retained even after the source disk is released. |
|SourceDiskType|String|system|The category of the source disk. Valid values:

 -   system: system disk
-   data: data disk |
|Status|String|accomplished|The status of the instance snapshot. Valid values:

 -   progressing: The instance snapshot is being created.
-   accomplished: The instance snapshot is created.
-   failed: The instance snapshot fails to be created. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotGroups
&RegionId=cn-hangzhou
&SnapshotGroupId.1=ssg-j6ciyh3k52qp7ovm****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeSnapshotGroupsResponse>
      <RequestId>3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A</RequestId>
      <NextToken></NextToken>
      <SnapshotGroups>
            <SnapshotGroup>
                  <Status>accomplished</Status>
                  <Description>This is description.</Description>
                  <InstanceId>i-j6ca469urv8ei629****</InstanceId>
                  <CreationTime>2021-03-23T10:58:48Z</CreationTime>
                  <SnapshotGroupId>ssg-j6ciyh3k52qp7ovm****</SnapshotGroupId>
                  <Snapshots>
                        <Snapshot>
                              <SnapshotId>s-j6cbzmrlbf09w72q****</SnapshotId>
                              <InstantAccess>true</InstantAccess>
                              <Progress>100%</Progress>
                              <SourceDiskType>system</SourceDiskType>
                              <InstantAccessRetentionDays>3</InstantAccessRetentionDays>
                              <SourceDiskId>d-j6c3ogynmvpi6wy7****</SourceDiskId>
                        </Snapshot>
                        <Snapshot>
                              <SnapshotId>s-j6cdofbycydvg7ey****</SnapshotId>
                              <InstantAccess>true</InstantAccess>
                              <Progress>100%</Progress>
                              <SourceDiskType>data</SourceDiskType>
                              <InstantAccessRetentionDays>3</InstantAccessRetentionDays>
                              <SourceDiskId>d-j6cf7l0ewidb78lq****</SourceDiskId>
                        </Snapshot>
                  </Snapshots>
                  <Name>testName</Name>
            </SnapshotGroup>
      </SnapshotGroups>
</DescribeSnapshotGroupsResponse>
```

`JSON` format

```
{
	"RequestId": "3F9A4CC4-362F-469A-B9EF-B3204EF8AA3A",
	"NextToken": "",
	"SnapshotGroups": {
		"SnapshotGroup": [
			{
				"Status": "accomplished",
				"Description": "This is description.",
				"InstanceId": "i-j6ca469urv8ei629****",
				"CreationTime": "2021-03-23T10:58:48Z",
				"SnapshotGroupId": "ssg-j6ciyh3k52qp7ovm****",
				"Snapshots": {
					"Snapshot": [
						{
							"SnapshotId": "s-j6cbzmrlbf09w72q****",
							"InstantAccess": true,
							"Progress": "100%",
							"SourceDiskType": "system",
							"InstantAccessRetentionDays": 3,
							"SourceDiskId": "d-j6c3ogynmvpi6wy7****"
						},
						{
							"SnapshotId": "s-j6cdofbycydvg7ey****",
							"InstantAccess": true,
							"Progress": "100%",
							"SourceDiskType": "data",
							"InstantAccessRetentionDays": 3,
							"SourceDiskId": "d-j6cf7l0ewidb78lq****"
						}
					]
				},
				"Name": "testName"
			}
		]
	}
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|InvalidStatus.ValueNotSupported|%s|The error message returned because the operation is not supported while the resource is in the current state.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

