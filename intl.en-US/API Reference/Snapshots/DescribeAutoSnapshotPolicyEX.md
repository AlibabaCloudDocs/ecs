# DescribeAutoSnapshotPolicyEX

You can call this operation to query the automatic snapshot policies that you have created.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAutoSnapshotPolicyEx&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAutoSnapshotPolicyEx|The operation that you want to perform. Set the value to DescribeAutoSnapshotPolicyEx. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the automatic snapshot policy that you want to query. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|AutoSnapshotPolicyId|String|No|sp-bp67acfmxazb4ph\*\*\*\*|The ID of the automatic snapshot policy. |
|PageNumber|Integer|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|1|The number of entries to return on each page.

Maximum value: 100.

Default value: 10. |
|Tag.N.Key|String|No|TestKey|The key of tag N of the automatic snapshot policy. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the automatic snapshot policy. Valid values of N: 1 to 20. The tag value can be an empty string. The tag value can be up to 128 characters in length. It cannot start with acs: or contain http:// or https://. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoSnapshotPolicies|Array of AutoSnapshotPolicy| |Details about the automatic snapshot policies. |
|AutoSnapshotPolicy| | | |
|AutoSnapshotPolicyId|String|sp-bp67acfmxazb4ph\*\*\*\*|The ID of the automatic snapshot policy. |
|AutoSnapshotPolicyName|String|testAutoSnapshotPolicyName|The name of the automatic snapshot policy. |
|CopiedSnapshotsRetentionDays|Integer|0|**Note:** This parameter will be available soon. |
|CreationTime|String|2014-04-21T12:08:52Z|The time when the auto snapshot policy was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|DiskNums|Integer|1|The number of disks to which the automatic snapshot policy is applied. |
|EnableCrossRegionCopy|Boolean|false|**Note:** This parameter will be available soon. |
|RegionId|String|cn-hangzhou|The region ID of the automatic snapshot policy. |
|RepeatWeekdays|String|\["6"\]|The days of the week on which automatic snapshots are created. Valid values are 1 to 7, which correspond to the days of the week. 1 indicates Monday. One or more days can be specified. |
|RetentionDays|Integer|30|The retention period of the automatic snapshot. Unit: days. Valid values:

-   -1: The automatic snapshot is permanently retained.
-   1 to 65536: The automatic snapshot is retained for the specified number of days. |
|Status|String|Normal|The status of the automatic snapshot policy. Valid values:

-   Normal: The automatic snapshot policy is normal.
-   Expire: The automatic snapshot policy cannot be used because you have overdue payments in your account. |
|Tags|Array of Tag| |Details about tags of the automatic snapshots. |
|Tag| | | |
|TagKey|String|TestKey|The tag key of the snapshot. |
|TagValue|String|TestValue|The tag value of the snapshot. |
|TargetCopyRegions|String|test|**Note:** This parameter will be available soon. |
|TimePoints|String|\["4", "19"\]|The points in time of the day at which automatic snapshots are created.

The time is displayed in UTC+8. Unit: hours. Valid values are 0 to 23, which correspond to the 24 points in time on the hour from 00:00:00 to 23:00:00. 1 indicates 01:00:00. Multiple points in time can be specified.

The parameter value is a JSON-formatted array such as `["0", "1",... "23"]`.The array can contain a maximum of 24 points in time separated by commas \(,\). |
|VolumeNums|Integer|2|The number of extended volumes to which the policy is applied. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|1|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|2|The total number of automatic snapshot policies. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAutoSnapshotPolicyEx
&RegionId=cn-hangzhou
&AutoSnapshotPolicyId=sp-bp67acfmxazb4ph****
&PageNumber=1
&PageSize=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAutoSnapshotPolicyExResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <AutoSnapshotPolicies>
            <AutoSnapshotPolicy>
                  <CreationTime>2019-01-22 11:38:08</CreationTime>
                  <Status>Normal</Status>
                  <DiskNums>1</DiskNums>
                  <AutoSnapshotPolicyName>testAutoSnapshotPolicyName</AutoSnapshotPolicyName>
                  <RegionId>cn-hangzhou</RegionId>
                  <VolumeNums>2</VolumeNums>
                  <RetentionDays>30</RetentionDays>
                  <TimePoints>["0"]</TimePoints>
                  <AutoSnapshotPolicyId>sp-bp67acfmxazb4ph****</AutoSnapshotPolicyId>
                  <RepeatWeekdays>["7"]</RepeatWeekdays>
                  <Tags>
                        <Tag>
                              <TagKey>TestKey</TagKey>
                              <TagValue>TestValue</TagValue>
                        </Tag>
                  </Tags>
            </AutoSnapshotPolicy>
      </AutoSnapshotPolicies>
      <PageSize>1</PageSize>
      <RequestId>CC323EDF-BBB7-420F-BCD1-D9B9D2E9D424</RequestId>
</DescribeAutoSnapshotPolicyExResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "AutoSnapshotPolicies": {
        "AutoSnapshotPolicy": [
            {
                "CreationTime": "2019-01-22 11:38:08",
                "Status": "Normal",
                "DiskNums": 1,
                "AutoSnapshotPolicyName": "testAutoSnapshotPolicyName",
                "RegionId": "cn-hangzhou",
                "VolumeNums": 2,
                "RetentionDays": 30,
                "TimePoints": "[\"0\"]",
                "AutoSnapshotPolicyId": "sp-bp67acfmxazb4ph****",
                "RepeatWeekdays": "[\"7\"]",
                "Tags": {
                    "Tag": [
                        {
                            "TagKey": "TestKey",
                            "TagValue": "TestValue"
                        }
                    ]
                }
            }
        ]
    },
    "PageSize": 1,
    "RequestId": "CC323EDF-BBB7-420F-BCD1-D9B9D2E9D424"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|The error message returned because the specified Tag.N.Key and Tag.N.Value parameters do not match.|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|The error message returned because the number of specified tags has exceeded the upper limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

