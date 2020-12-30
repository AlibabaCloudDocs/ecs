# ModifySnapshotAttribute

You can call this operation to modify the name or description of a snapshot, or disable the instant access feature.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifySnapshotAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySnapshotAttribute|The operation that you want to perform. Set the value to ModifySnapshotAttribute. |
|SnapshotId|String|Yes|s-bp199lyny9bb47pa\*\*\*\*|The ID of the snapshot. |
|SnapshotName|String|No|testSnapshotName|The name of the snapshot. The name must be 2 to 128 characters in length, and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.

It cannot start with auto because snapshots whose names start with auto are recognized as automatic snapshots. |
|Description|String|No|testDescription|The description of the snapshot. The description must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DisableInstantAccess|Boolean|No|false|Specifies whether to disable the instant access feature. Valid values:

-   true: disables the instant access feature.
-   false: enables the instant access feature.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifySnapshotAttribute
&SnapshotId=s-bp199lyny9bb47pa****
&SnapshotName=testSnapshotName
&Description=testDescription
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySnapshotAttributeResponse>
            <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
</ModifySnapshotAttributeResponse>
```

`JSON` format

```
{
    "RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified description is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|The error message returned because the specified SnapshotName parameter is invalid.|
|400|NoAttributeToModify|No attribute to be modified in this request.|The error message returned because no properties of the specified snapshot are modified.|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|The error message returned because the specified SnapshotId parameter does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

