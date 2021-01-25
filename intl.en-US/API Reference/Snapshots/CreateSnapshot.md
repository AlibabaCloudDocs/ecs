# CreateSnapshot

You can call this operation to create a snapshot for a disk.

## Description

The local snapshot feature is replaced by the instant aaccess feature. The following section describes the related parameters:

-   If you have used local snapshots before December 14, 2020, you can use the `Category` or `InstantAccess` parameter. Take note of the following items:
    -   The `Category` and `InstantAccess` parameters cannot be specified at the same time.
    -   If neither of the `Category` and `InstantAccess` parameters is specified, normal snapshots are created.
-   If you have not used local snapshots before December 14, 2020, you can use only the `InstantAccess` parameter, and cannot use the `Category` parameter.


In the following scenarios, you cannot create snapshots for a disk:

-   The number of manual snapshots \(also called user-created snapshots\) of the disk has reached 256.
-   A snapshot is being created for the disk.
-   The instance to which the disk is attached has never been started.
-   The instance to which the disk is attached is not in the **Stopped** \(`Stopped`\) or **Running** \(`Running`\) state.
-   If the response contains `{"OperationLocks": {"LockReason" : "security"}}` when you query information of the instance, the instance is locked for security reasons and all operations are prohibited on the instance.

When you create a snapshot, take note of the following items:

-   About 1 hour after an instance is created or the system disk of an instance is replaced, you can create a snapshot for a disk that is attached to the instance. After a data disk is attached to an instance, you must wait for a period of time before you can create a snapshot. The amount of time to wait depends on the volume of data stored on the disk.
-   If a snapshot is being created, you cannot call the [CreateImage](~~25535~~) operation to create a custom image from this snapshot.
-   If the disk for which you want to create a snapshot is attached to an ECS instance, do not change the instance status while a snapshot is being created.
-   You can create snapshots for a disk that is in the **Expired** \(`Expired`\) state. If the release time scheduled for a disk in the Expired state arrives when a snapshot is being created for the disk, the snapshot is in the **Creating** \(`Creating`\) state and is deleted when the disk is released.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateSnapshot&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateSnapshot|The operation that you want to perform. Set the value to CreateSnapshot. |
|DiskId|String|Yes|d-bp1s5fnvk4gn2tws0\*\*\*\*|The ID of the disk. |
|SnapshotName|String|No|testSnapshotName|The name of the snapshot. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.

It cannot start with auto because snapshots whose names start with auto are recognized as automatic snapshots. |
|Description|String|No|testDescription|The description of the snapshot. The description must be 2 to 256 characters in length and cannot start with http:// or https://.

This parameter is empty by default. |
|RetentionDays|Integer|No|30|The retention period of the snapshot. Valid values: 1 to 65536. Unit: days. The snapshot is automatically released when the retention period ends.

This parameter is empty by default, which indicates that the snapshot will not be automatically released. |
|Category|String|No|Standard|The category of the snapshot. Valid values:

-   Standard: normal snapshot
-   Flash: local snapshot

**Note:** This parameter will be removed in the future. We recommend that you use the `InstantAccess` parameter to ensure future compatibility. This parameter and the `InstantAccess` parameter cannot be specified at the same time. For more information, see the "Description" section in this topic. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request. You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value can only contain ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|Tag.N.value|String|No|null|The value of tag N to be bound to the snapshot.

**Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Value parameter to ensure future compatibility. |
|Tag.N.key|String|No|null|The key of tag N to be bound to the snapshot.

**Note:** This parameter will be removed in the future. We recommend that you use the Tag.N.Key parameter to ensure future compatibility. |
|Tag.N.Key|String|No|TestKey|The key of tag N to be bound to the snapshot. Valid values of N: 1 to 20. The tag key cannot be an empty string. It can be up to 128 characters in length and cannot start with acs: or aliyun. It cannot contain http:// or https://. |
|Tag.N.Value|String|No|TestValue|The value of tag N to be bound to the snapshot. Valid values of N: 1 to 20. The tag value can be an empty string. It can be up to 128 characters in length and cannot start with acs: or contain http:// or https://. |
|ResourceGroupId|String|No|rg-bp67acfmxazb4p\*\*\*\*|The ID of the resource group to which the snapshot belongs. |
|InstantAccess|Boolean|No|false|Specifies whether to enable the instant access feature. Valid values:

-   true: enables the instant access feature. This feature can be enabled only for enhanced SSDs \(ESSDs\).
-   false: disables the instant access feature. If InstantAccess is set to false, normal snapshots are created.

Default value: false.

**Note:** This parameter and the `Category` parameter cannot be specified at the same time. For more information, see the "Description" section in this topic. |
|InstantAccessRetentionDays|Integer|No|1|Specifies the retention period of the instant access feature. After the retention period ends, the snapshot is automatically released. This parameter takes effect only when `InstantAccess` is set to true. Unit: days. Valid values: 1 to 65535. By default, the value of this parameter is the same as that of `RetentionDays`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|SnapshotId|String|s-bp17441ohwka0yuh\*\*\*\*|The ID of the snapshot. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-bp1s5fnvk4gn2tws0****
&SnapshotName=testSnapshotName
&Description=testDescription
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateSnapshotResponse>
          <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
          <SnapshotId>s-bp17441ohwka0yuh****</SnapshotId>
</CreateSnapshotResponse>
```

`JSON` format

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "SnapshotId": "s-bp17441ohwka0yuh****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|The error message returned because the specified SnapshotName parameter is invalid.|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
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
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments in your account.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not activated.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|The error message returned because the operation is not supported while the Shared Block Storage device is in the current state.|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|The error message returned because the specified Shared Block Storage device does not exist. Check whether the Shared Block Storage device ID is correct.|
|403|IdempotentParameterMismatch|The specified clientToken is used.|The error message returned because the specified client token is already in use.|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|The error message returned because the status of the specified disk is invalid. Restart the instance and try again.|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|The error message returned because the specified disk category does not support the operation.|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|The error message returned because the specified disk is being migrated. Wait until the disk is migrated and try again.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|The error message returned because a tag with the identical key already exists.|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|The error message returned because the specified Tag.N.Key parameter is invalid.|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|The error message returned because the specified Tag.N.Value parameter is invalid.|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|The error message returned because the previous idempotent request is being processed. Try again later.|
|403|QuotaExceed.Tags|%s|The error message returned because the maximum number of tags has been reached.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

