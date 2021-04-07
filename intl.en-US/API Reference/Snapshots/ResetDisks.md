# ResetDisks

You can call this operation to roll back one or more disks by using an instance snapshot.

## Description

Before you call this operation to roll back disks, you must understand the precautions for the rollback feature. For more information, see [Roll back disks by using an instance snapshot](~~209160~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ResetDisks&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ResetDisks|The operation that you want to perform. Set the value to ResetDisks. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|Disk.N.DiskId|String|No|d-j6cf7l0ewidb78lq\*\*\*\*|The ID of disk N to be rolled back. Valid values of N: 1 to 10. |
|Disk.N.SnapshotId|String|No|s-j6cdofbycydvg7ey\*\*\*\*|The ID of the snapshot contained in the instance snapshot for disk N. Valid values of N: 1 to 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OperationProgressSet|Array of OperationProgress| |Details about the rollback operation. |
|OperationProgress| | | |
|ErrorCode|String|400|The error code. This parameter is empty when the operation was successful.

For more information about error codes and error messages, visit the [API error center](https://error-center.alibabacloud.com/status/product/Ecs). |
|ErrorMsg|String|testErrorMsg|The error message. This parameter is empty when the operation was successful.

For more information about error codes and error messages, visit the [API error center](https://error-center.alibabacloud.com/status/product/Ecs). |
|OperationStatus|String|Success|Indicates whether the operation was successful.

If the operation was successful, a value of Success is returned. If the operation failed, an error code and error message are returned. |
|RelatedItemSet|Array of RelatedItem| |Details about the resources. |
|RelatedItem| | | |
|Name|String|SnapshotId|The name of the resource. |
|Value|String|s-j6cdofbycydvg7ey\*\*\*\*|The ID of the resource. |
|RequestId|String|3D66C85C-AA97-4A00-B0ED-2D9A80FE782C|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ResetDisks
&RegionId=cn-hangzhou
&Disk.1.DiskId=d-j6cf7l0ewidb78lq****
&Disk.1.SnapshotId=s-j6cdofbycydvg7ey****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ResetDisksResponse>
      <RequestId>5C4160C1-C77D-4FD0-9C47-DB9FFA3D1220</RequestId>
      <OperationProgressSet>
            <OperationProgress>
                  <OperationStatus>Success</OperationStatus>
                  <ErrorMsg></ErrorMsg>
                  <RelatedItemSet>
                        <RelatedItem>
                              <Value>s-j6cdofbycydvg7ey****</Value>
                              <Name>SnapshotId</Name>
                        </RelatedItem>
                        <RelatedItem>
                              <Value>d-j6cf7l0ewidb78lq****</Value>
                              <Name>DiskId</Name>
                        </RelatedItem>
                  </RelatedItemSet>
                  <ErrorCode></ErrorCode>
            </OperationProgress>
      </OperationProgressSet>
</ResetDisksResponse>
```

`JSON` format

```
{
    "RequestId": "5C4160C1-C77D-4FD0-9C47-DB9FFA3D1220",
    "OperationProgressSet": {
        "OperationProgress": [
            {
                "OperationStatus": "Success",
                "ErrorMsg": "",
                "RelatedItemSet": {
                    "RelatedItem": [
                        {
                            "Value": "s-j6cdofbycydvg7ey****",
                            "Name": "SnapshotId"
                        },
                        {
                            "Value": "d-j6cf7l0ewidb78lq****",
                            "Name": "DiskId"
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

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist. Check whether the disk ID is correct.|
|404|Disk.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist. Check whether the disk ID is correct.|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|The error message returned because the specified snapshot does not exist. Check whether the snapshot ID is correct.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned because the operation is not supported while the resource is locked for security reasons.|
|403|InvalidParameter.Mismatch|The specified snapshot is not created from the specified disk.|The error message returned because an encrypted snapshot cannot be used to roll back an unencrypted disk.|
|403|InvalidSnapshot.TooOld|The snapshotId is created before 2013-07-15, it cannot be restored since the first time the disk detached.|The error message returned because snapshots created before July 15, 2013 do not support this operation.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|OperationDenied|The specified snapshot dees not support ResetDisk.|The error message returned because the specified snapshot does not support the operation.|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|The error message returned because the specified snapshot is being created.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|The error message returned because the disk category does not support the operation.|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|The error message returned because the operation is not supported while the snapshot service is not activated.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified instance does not exist. Check whether the instance ID is correct.|
|403|Operation.Conflict|The operation may conflicts with others.|The error message returned because the operation conflicts with other operations.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned because you are not authorized to manage the disk. Try again when you are authorized.|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|The error message returned because the specified RegionId parameter is invalid.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|The error message returned because the customer master key \(CMK\) is not enabled when KMSKeyId is specified for an encrypted disk. You can call the DescribeKey operation provided by KMS to query the information of a specific CMK.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

