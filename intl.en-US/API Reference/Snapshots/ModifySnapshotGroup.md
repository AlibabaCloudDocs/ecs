# ModifySnapshotGroup

You can call this operation to modify the name and description of an instance snapshot.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifySnapshotGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifySnapshotGroup|The operation that you want to perform. Set the value to ModifySnapshotGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance snapshot. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|SnapshotGroupId|String|Yes|ssg-j6ciyh3k52qp7ovm\*\*\*\*|The ID of the instance snapshot. |
|Name|String|No|testName02|The new name of the instance snapshot. The name must be 2 to 128 characters in length. It can contain letters, digits, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|Description|String|No|This is new description|The new description of the instance snapshot. The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|A00B5E55-76B7-42C8-8A80-AF10E980DCC7|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifySnapshotGroup
&RegionId=cn-hangzhou
&SnapshotGroupId=ssg-j6ciyh3k52qp7ovm****
&Name=testName02
&Description=This is new description
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifySnapshotGroupResponse>
      <RequestId>A00B5E55-76B7-42C8-8A80-AF10E980DCC7</RequestId>
</ModifySnapshotGroupResponse>
```

`JSON` format

```
{
    "RequestId": "A00B5E55-76B7-42C8-8A80-AF10E980DCC7"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|InvalidParameter.Name|The specified Name is invalid.|The error message returned because the specified Name parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

