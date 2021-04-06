# CreateSnapshotGroup

You can call this operation to create an instance snapshot for the disks in an ECS instance. An instance snapshot contains snapshots of one or more disks.

## Description

When you create an instance snapshot, take note of the following items:

-   The instance is in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) state.
-   The instance snapshot feature applies only to disks that are enhanced SSDs \(ESSDs\) and in the **In Use** \(`In_use`\) state.
-   A single instance snapshot can contain snapshots of up to 10 disks including the system disk and data disks, and cannot exceed 32 TiB in size.
-   Created snapshots are stored unless you delete them. We recommend that you delete snapshots that are no longer needed on a regular basis to reduce snapshot storage fees.

For information about the instance snapshot feature and its billing, see [Instance snapshots](~~199625~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateSnapshotGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|No|CreateSnapshotGroup|The operation that you want to perform. Set the value to CreateSnapshotGroup. |
|InstanceId|String|Yes|i-j6ca469urv8ei629\*\*\*\*|The ID of the instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ExcludeDiskId.N|RepeatList|No|d-j6cf7l0ewidb78lq\*\*\*\*|The ID of disk N for which you do not need to create snapshots. After this parameter is specified, the created instance snapshot does not contain snapshots of the disks.

This parameter is empty by default, which indicates that snapshots are created for all the disks in the instance.

Valid values of N: 1 to 16. |
|InstantAccess|Boolean|No|false|Specifies whether to enable the instant access feature. Valid values:

-   true: enables the instance access feature.
-   false: disables the instance access feature.

Default value: false. |
|InstantAccessRetentionDays|Integer|No|1|Specifies the number of days for which the instant access feature is available. Unit: days. Valid values: 1 to 65535.

This parameter take effect only when `InstantAccess` is set to true. The instant access feature is automatically disabled when the specified duration ends.

This parameter is empty by default, which indicates that the expiration time of the instant access feature is determined by the time when snapshots are released. |
|Name|String|No|testName|The name of the instance snapshot. The name must be 2 to 128 characters in length, and can contain letters, digits, periods \(.\), underscores \(\_\), hyphens \(-\), and colons \(:\). It must start with a letter or a digit and cannot start with `http://` or `https://`. |
|Description|String|No|This is description.|The description. It must be 2 to 256 characters in length, and cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|01ABBD93-1ABB-4D92-B496-1A3D20EC0697|The ID of the request. |
|SnapshotGroupId|String|ssg-j6ciyh3k52qp7ovm\*\*\*\*|The ID of the instance snapshot. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateSnapshotGroup
&InstanceId=i-j6ca469urv8ei629****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateSnapshotGroupResponse>
      <RequestId>01ABBD93-1ABB-4D92-B496-1A3D20EC0697</RequestId>
      <SnapshotGroupId>ssg-j6ciyh3k52qp7ovm****</SnapshotGroupId>
</CreateSnapshotGroupResponse>
```

`JSON` format

```
{
    "RequestId": "01ABBD93-1ABB-4D92-B496-1A3D20EC0697",
    "SnapshotGroupId": "ssg-j6ciyh3k52qp7ovm****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|The error message returned because the specified disk does not exist. Check whether the disk ID is correct.|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|The error message returned because the specified Name parameter is invalid.|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length, and cannot start with http:// or https://.|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|The error message returned because another snapshot is being created. Wait until the snapshot is created and try again.|
|403|InstanceLockedForSecurity|The disk attached instance is locked due to security.|The error message returned because the instance to which the disk is attached is locked for security reasons.|
|403|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|The error message returned because the removable disk has never been attached to instances and its content remains unchanged.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned because the maximum number of snapshots has been reached. To store new snapshots, delete snapshots that are no longer needed.|
|403|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|The error message returned because the specified disk has never been used and its content remains unchanged.|
|403|CreateSnapshot.Failed|The process of creating snapshot is failed.|The error message returned because the snapshot has failed to be created.|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|The error message returned because the disk has expired due to overdue payments.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|The error message returned because the category of the specified Elastic Block Storage device does not support this operation.|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|The error message returned because the disk category does not support the operation.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not activated.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|The error message returned because the operation is not supported while the Shared Block Storage device is in the current state.|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|The error message returned because the specified Shared Block Storage device does not exist. Check whether the Shared Block Storage device ID is correct.|
|403|IdempotentParameterMismatch|The specified clientToken is used.|The error message returned because the specified client token is already in use.|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|The error message returned because the status of the specified disk is invalid. Restart the instance and try again.|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|The error message returned because the specified disk category does not support the operation.|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|The error message returned because the specified disk is being migrated. Wait until the disk is migrated and try again.|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|The error message returned because the customer master key \(CMK\) is not enabled after a KMS key ID is specified for an encrypted disk. You can call the DescribeKey operation provided by KMS to query the information about a specific CMK.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because the specified tag key already exists. Tag keys must be unique.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|The error message returned because the previous idempotent request is being processed. Try again later.|
|400|InvalidRetentionDays.Malformed|The specified RetentionDays is not valid.|The error message returned because the specified InstantAccessRetentionDays parameter is invalid. Check whether the specified InstantAccessRetentionDays parameter is valid.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|
|403|InvalidSnapshotCategory.Malformed|The specified Category is not valid.|The error message returned because the specified snapshot type is invalid. Check whether the specified Category parameter is valid.|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|
|400|InvalidParameter.Name|The specified Name is invalid.|The error message returned because the specified Name parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

