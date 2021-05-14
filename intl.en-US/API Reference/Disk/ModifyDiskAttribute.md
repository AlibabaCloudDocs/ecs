# ModifyDiskAttribute

You can call this operation to modify the properties of one or more Elastic Block Storage \(EBS\) devices, including their names, descriptions, and whether they are released along with their associated instances.

## Description

-   If you set DeleteWithInstance to false for a disk and the instance to which the disk is attached is locked for security reasons, the DeleteWithInstance parameter is ignored and the disk will be released along with the instance. If the value of `LockReason` is security in OperationLocks of the API response when you query information of an instance, the instance is locked for security reasons.
-   You can use the `DiskIds.N` parameter to modify the properties of multiple EBS devices at a time, including their names, descriptions, and whether they are released along with their associated instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyDiskAttribute&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDiskAttribute|The operation that you want to perform. Set the value to ModifyDiskAttribute. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the disk. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|DiskId|String|No|d-bp1famypsnar20bv\*\*\*\*|The ID of the disk.

 **Note:** You can specify `DiskId` or `DiskIds.N`, but you cannot specify both of them. |
|DiskIds.N|RepeatList|No|d-bp1famypsnar20bv\*\*\*\*|The ID of disk N. Valid values of N: 0 to 100.

 **Note:** You can specify `DiskId` or `DiskIds.N`, but you cannot specify both of them. |
|DiskName|String|No|MyDiskName|The name of the disk. The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). |
|Description|String|No|TestDescription|The description of the disk. It must be 2 to 256 characters in length and cannot start with http:// or https://. |
|DeleteWithInstance|Boolean|No|false|Specifies whether to release the disk along with its associated instance. This parameter is empty by default, which indicates that the current value remains unchanged.

 An error is returned if you set this parameter to false in the following cases:

 -   Category is set to ephemeral.
-   Category is set to cloud and Portable is set to false. |
|DeleteAutoSnapshot|Boolean|No|false|Specifies whether to delete the automatic snapshots of the disk when the disk is released. This parameter is empty by default, which indicates that the current value remains unchanged. |
|EnableAutoSnapshot|Boolean|No|true|Specifies whether to enable the automatic snapshot policy feature for the disk.

 -   True: enables the automatic snapshot policy feature for the disk.
-   false: disables the automatic snapshot policy feature for the disk.

 This parameter is empty by default, which indicates that the current value remains unchanged.

 **Note:** By default, the automatic snapshot policy feature is enabled for created disks. You need only to apply an automatic snapshot policy to a disk before you can use the policy. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyDiskAttribute
&RegionId=cn-hangzhou
&DiskId=d-bp1famypsnar20bv****
&DiskName=MyDiskName
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDiskAttributeResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskAttributeResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist. Check whether the disk ID is correct.|
|400|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|The error message returned because the specified DiskName parameter is invalid. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|The error message returned because the specified Description parameter is invalid. The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|400|NoAttributeToModify|No attribute to be modified in this request.|The error message returned because no properties of the specified EBS device are modified.|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|The error message returned because the maximum number of snapshots has been reached. To store new snapshots, delete the snapshots that are no longer needed.|
|403|DiskNotPortable|The specified disk is not a portable disk.|The error message returned because the specified disk is not removable.|
|403|IncorrectDiskStatus|The operation is not supported in this status.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|400|IncompleteParamter|Some fields can not be null in this request.|The error message returned because a required parameter is not specified.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned because you are not authorized to manage the disk. Try again when you are authorized.|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|The error message returned because the specified RegionId parameter is invalid.|
|404|InvalidInstanceId.NotFound|Specified attached instance does not exist.|The error message returned because the specified instance does not exist. Check whether instance ID is correct.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

