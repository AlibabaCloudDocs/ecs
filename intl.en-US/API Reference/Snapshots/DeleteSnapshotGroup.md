# DeleteSnapshotGroup

You can call this operation to delete an instance snapshot.

## Description

If you have custom images that were created from a disk snapshot contained in an instance snapshot, the disk snapshot is retained when the instance snapshot is deleted. Before you can delete the disk snapshot, you must call the [DeleteImage](~~25537~~) operation to delete the custom images. Then, you can call the [DeleteSnapshot](~~25525~~) operation to delete the disk snapshot.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteSnapshotGroup&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteSnapshotGroup|The operation that you want to perform. Set the value to DeleteSnapshotGroup. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance snapshot. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|SnapshotGroupId|String|Yes|ssg-j6c9lpuyxo2uxxny\*\*\*\*|The ID of the instance snapshot. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OperationProgressSet|Array of OperationProgress| |Details about the delete operation. |
|OperationProgress| | | |
|ErrorCode|String|400|The error code. This parameter is empty when the operation was successful.

 For more information about error codes and error messages, visit the [API error center](https://error-center.alibabacloud.com/status/product/Ecs). |
|ErrorMsg|String|testErrorMsg|The error message. This parameter is empty when the operation was successful.

 For more information about error codes and error messages, visit the [API error center](https://error-center.alibabacloud.com/status/product/Ecs). |
|OperationStatus|String|Success|Indicates whether the operation was successful. If the operation was successful, a value of Success is returned. If the operation failed, error codes and messages are returned. |
|RelatedItemSet|Array of RelatedItem| |Details about the resources. |
|RelatedItem| | | |
|Name|String|SnapshotId|The name of the resource. |
|Value|String|s-j6c9lpuyxo2uxxnx\*\*\*\*|The ID of the resource. |
|RequestId|String|6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteSnapshotGroup
&RegionId=cn-hangzhou
&SnapshotGroupId=ssg-j6c9lpuyxo2uxxny****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteSnapshotGroupResponse>
      <RequestId>6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E</RequestId>
      <OperationProgressSet>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6c9lpuyxo2uxxnx****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6c9lpuyxo2uxxnx****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
      </OperationProgressSet>
</DeleteSnapshotGroupResponse>
```

`JSON` format

```
{
	"RequestId": "6EDE885A-FDC1-4FAE-BC44-6EACAEA6CC6E",
	"OperationProgressSet": {
		"OperationProgress": [
			{
				"OperationStatus": "Success",
				"ErrorMsg": "",
				"RelatedItemSet": {
					"RelatedItem": [
						{
							"Value": "s-j6c9lpuyxo2uxxnx****",
							"Name": "SnapshotId"
						}
					]
				},
				"ErrorCode": ""
			},
			{
				"OperationStatus": "Success",
				"ErrorMsg": "",
				"RelatedItemSet": {
					"RelatedItem": [
						{
							"Value": "s-j6c9lpuyxo2uxxnx****",
							"Name": "SnapshotId"
						}
					]
				},
				"ErrorCode": ""
			}
		]
	}
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

