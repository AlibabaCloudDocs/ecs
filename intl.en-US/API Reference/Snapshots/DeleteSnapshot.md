# DeleteSnapshot

You can call this operation to delete a snapshot. If you call this operation to delete a snapshot that is being created, the snapshot creation task is canceled.

## Description

When you call this operation, take note of the following items:

-   If the specified snapshot ID does not exist, the request is ignored.
-   A snapshot that has been used to create custom images cannot be deleted. The snapshot can be deleted only after the created custom images are deleted \([DeleteImage](~~25537~~)\).
-   A snapshot that has been used to create disks cannot be deleted. If you do want to delete the snapshot, set the `Force` parameter to true to force delete the snapshot. The disks created from the snapshot cannot be re-initialized after the snapshot is force deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshot&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteSnapshot|The operation that you want to perform. Set the value to DeleteSnapshot. |
|SnapshotId|String|Yes|s-bp1c0doj0taqyzzl\*\*\*\*|The ID of the snapshot. |
|Force|Boolean|No|false|Specifies whether to force delete the snapshot that has been used to create disks. Valid values:

-   true: force deletes the snapshot. After the snapshot is force deleted, the disks created from this snapshot cannot be re-initialized.
-   false: does not force delete the snapshot.

Default value: false |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteSnapshot
&SnapshotId=s-bp1c0doj0taqyzzl****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteSnapshotResponse>
       <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId>
</DeleteSnapshotResponse>
```

`JSON` format

```
{
    "RequestId": "CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|SnapshotCreatedImage|The snapshot has been used to create user defined image\(s\).|The error message returned because the snapshot has been used to create custom images and cannot be deleted. The snapshot can be deleted only after the custom images created from the snapshot are deleted \(DeleteImage\).|
|403|SnapshotCreatedDisk|The snapshot has been used to create disk\(s\).|The error message returned because the snapshot has been used to create disks and cannot be deleted. If you do want to delete the snapshot, set the Force parameter to true to force delete the snapshot. The disks created from the snapshot cannot be re-initialized after the snapshot is force deleted.|
|400|MissingParameter|The input parameter SnapshotId that is mandatory for processing this request is not supplied.|The error message returned because the required SnapshotId parameter is not specified.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|404|InvalidSnapshotId.NotFound|The specified snapshot is not found|The error message returned because the specified SnapshotId parameter does not exist.|
|403|Operation.Conflict|The operation may conflicts with others, please retry later.|The error message returned because the operation conflicts with other operations. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

