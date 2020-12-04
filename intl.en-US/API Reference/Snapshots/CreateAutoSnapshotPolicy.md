# CreateAutoSnapshotPolicy

You can call this operation to create an automatic snapshot policy.

## Description

After you create an automatic snapshot policy, you can call the [ApplyAutoSnapshotPolicy](~~25531~~) operation to apply it to a disk. You can also call the [ModifyAutoSnapshotPolicyEx](~~25529~~) operation to modify a created automatic snapshot policy.

When you call this operation, take note of the following items:

-   You can create a maximum of 100 automatic snapshot policies in each region for a single Alibaba Cloud account.
-   If an automatic snapshot is being created when the time scheduled for creating an automatic snapshot is due, the new snapshot task is skipped. This may occur when a disk contains a large volume of data. For example, you have scheduled snapshots to be created at 09:00:00, 10:00:00, 11:00:00, and 12:00:00. The system starts to create a snapshot for the disk at 09:00:00. The process takes 80 minutes because the disk has a large volume of data and ends at 10:20:00. The system does not create a snapshot at 10:00:00, but creates a snapshot at 11:00:00.
-   For information about how to copy a snapshot from a region to another, see the "Background information" section in [Copy a snapshot](~~159441~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateAutoSnapshotPolicy&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateAutoSnapshotPolicy|The operation that you want to perform. Set the value to CreateAutoSnapshotPolicy. |
|regionId|String|Yes|cn-hangzhou|The region ID of the automatic snapshot policy. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|repeatWeekdays|String|Yes|\["1","2"\]|The days of the week on which to create automatic snapshots. Valid values: 1 to 7, which correspond to Monday to Sunday. 1 indicates Monday.

 To schedule multiple automatic snapshots to be created for a disk in a week, you can specify multiple days.

 -   You can specify up to seven days over a one-week period.
-   You must specify the parameter in a JSON-formatted array such as `["1","2"..." 7"]`. Separate multiple values with commas \(,\). |
|retentionDays|Integer|Yes|30|The retention period of the automatic snapshot. Unit: days. Valid values:

 -   -1: The snapshot is permanently retained.
-   1 to 65535: The automatic snapshot is retained for the specified number of days.

 Default value: -1 |
|timePoints|String|Yes|\["0", "1", … "23"\]|The point in time at which to create automatic snapshots. Unit: hours. Valid values: 0 to 23. The values indicate a total of 24 hours from 00:00:00 to 23:00:00. For example, 1 indicates 01:00:00.

 To schedule multiple automatic snapshot tasks for a disk in a day, you can set the timePoints parameter to a JSON-formatted array. You can specify a maximum of 24 points in time. |
|autoSnapshotPolicyName|String|No|TestName|The name of the automatic snapshot policy. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.

 This parameter is empty by default. |
|EnableCrossRegionCopy|Boolean|No|false|Specifies whether to enable the system to automatically copy snapshots across regions.

 -   true: enables the system to automatically copy snapshots across regions.
-   false: disables the system to automatically copy snapshots across regions. |
|TargetCopyRegions|String|No|\["cn-hangzhou"\]|The destination region to which the snapshot is copied. You can set a destination region. |
|CopiedSnapshotsRetentionDays|Integer|No|30|The retention period of the snapshot copied across regions. Unit: days. Valid values:

 -   -1: The snapshot is permanently retained.
-   1 to 65535: The automatic snapshot is retained for the specified number of days.

 Default value: -1 |
|Tag.N.Key|String|No|TestKey|The key of tag N of the snapshot. Valid values of N: 1 to 20. The tag value cannot be an empty string. The tag key can be up to 128 characters in length. It cannot start with aliyun or acs:, or contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N of the snapshot. Valid values of N: 1 to 20. This parameter can be an empty string. The tag value can be up to 128 characters in length. It cannot start with acs: or contain http:// or https://. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoSnapshotPolicyId|String|sp-bp12m37ccmxvbmi5\*\*\*\*|The ID of the automatic snapshot policy. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateAutoSnapshotPolicy
&regionId=cn-hangzhou
&repeatWeekdays=["1"]
&retentionDays=30
&timePoints=["0", "19"]
&autoSnapshotPolicyName=TestName
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateAutoSnapshotPolicyResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
      <AutoSnapshotPolicyId>sp-bp12m37ccmxvbmi5****</AutoSnapshotPolicyId>
</CreateAutoSnapshotPolicyResponse>
```

`JSON` format

```
{
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE",
    "AutoSnapshotPolicyId": "sp-bp12m37ccmxvbmi5****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|The error message returned because the specified regionId parameter is invalid.|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|The error message returned because the specified repeatWeekDays parameter is invalid.|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|The error message returned because the specified timePoints parameter is invalid.|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|The error message returned because the specified retentionDays parameter is invalid.|
|403|AutoSnapshotPolicy.QuotaExceed|The maximum number of automatic snapshot policy has been reached.|The error message returned because the maximum number of automatic snapshot policies has been reached.|
|400|DiskCategory.OperationNotSupported|The type of the specified disk does not support creating a snapshot.|The error message returned because the operation is not supported by the current disk category.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account before you proceed.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not activated.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

