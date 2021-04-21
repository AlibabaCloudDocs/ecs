# ModifyAutoSnapshotPolicyEx

You can call this operation to modify an automatic snapshot policy. After you modify an automatic snapshot policy that is applied to specific disks, the new policy takes effect immediately on the disks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyAutoSnapshotPolicyEx&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyAutoSnapshotPolicyEx|The operation that you want to perform. Set the value to ModifyAutoSnapshotPolicyEx. |
|autoSnapshotPolicyId|String|Yes|sp-bp12m37ccmxvbmi5\*\*\*\*|The ID of the automatic snapshot policy to be modified. You can call the [DescribeAutoSnapshotPolicyEx](~~25530~~) operation to query the available automatic snapshot policies. |
|regionId|String|Yes|cn-hangzhou|The region ID of the automatic snapshot policy. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|autoSnapshotPolicyName|String|No|SPTestName|The name of the automatic snapshot policy. If this parameter is not specified, the original name is retained. |
|timePoints|String|No|\["0", "1"\]|The points in time of the day at which to create auto snapshots. The time must be in UTC+8. Unit: hours. Valid values are 0 to 23, which correspond to the 24 points in time on the hour from 00:00:00 to 23:00:00. 1 indicates 01:00:00. To schedule multiple automatic snapshots to be created in a week, you can specify multiple days.

-   You can specify up to 24 points in time.
-   You must set this parameter to a JSON-formatted array such as `["0", "1", ... "23"]`. Separate the points in time with commas \(,\). |
|repeatWeekdays|String|No|\["1", "7"\]|The days of the week on which to create automatic snapshots. Valid values are 1 to 7, which correspond to the days of the week. To schedule multiple automatic snapshots to be created in a week, you can specify multiple days.

-   You can specify up to seven days over a one-week period.
-   You must set this parameter to a JSON-formatted array such as `["1", "2" ... "7"]`. Separate the values in the array with commas \(,\). |
|retentionDays|Integer|No|30|The retention period of the automatic snapshot. Unit: days. Default value: -1. Valid values:

-   -1: The automatic snapshot is permanently retained.
-   1 to 65536: The automatic snapshot is retained for the specified number of days. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyAutoSnapshotPolicyEx
&autoSnapshotPolicyId=sp-bp12m37ccmxvbmi5****
&regionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyAutoSnapshotPolicyResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ModifyAutoSnapshotPolicyResponse>
```

`JSON` format

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist.|The error message returned because the specified automatic snapshot policy does not exist.|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|The error message returned because the specified automatic snapshot policy does not exist in the region.|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|The error message returned because the specified regionId parameter is invalid.|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|The error message returned because the specified RepeatWeekDays parameter is invalid.|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|The error message returned because the specified TimePoints parameter is invalid.|
|403|ParameterInvalid|The specified AutoSnapshotPolicyId is invalid.|The error message returned because the specified autoSnapshotPolicyId parameter is invalid.|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|The error message returned because the specified RetentionDays parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

