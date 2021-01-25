# StartInstance

You can call this operation to start an ECS instance. After the operation is called, the instance enters the Starting state.

## Description

When you call this operation, take note of the following items:

-   The ECS instance to be started must be in the **Stopped** \(`Stopped`\) state.
-   If `OperationLocks` in the DescribeInstances response contains `"LockReason" : "security"` for an instance, the instance is locked for security reasons and cannot be started through calls to this operation. For more information, see [API behavior when an instance is locked for security reasons](~~25695~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=StartInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StartInstance|The operation that you want to perform. Set the value to StartInstance. |
|InstanceId|String|Yes|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance that you want to start. |
|InitLocalDisk|Boolean|No|true|Specifies whether to restore the instance to its initial health status. This parameter is applicable to instances of the instance families such as d1, i1, and i2 that are equipped with local disks. If a local disk of a d1, i1, or i2 instance fails, you can use this parameter to specify whether to restore the instance to its initial health status at startup. Default value: false. Valid values:

-   true: restores the instance to its initial health status at startup. After the instance is restored to its initial health status, data in the original local disks of the instance is lost.
-   false: does not perform any operations and keeps the instance in the current state. |
|DryRun|Boolean|No|true|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include whether your AccessKey pair is valid, whether RAM users are authorized, and whether the required parameters are specified. If the check fails, the corresponding error is returned. If the check succeeds, the DryRunOperation error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2XX HTTP status code is returned and the request is made. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=StartInstance
&InstanceId=i-bp67acfmxazb4p****
&InitLocalDisk=true
&<Common request parameters>
```

Sample success responses

`XML` format

```
<StartInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</StartInstanceResponse>
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
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|InsufficientBalance|Your account does not have enough balance.|The error message returned because your account balance is insufficient. Add funds to your account and try again.|
|500|InstanceNotReady|The specified instance is not ready for use|The error message returned because the specified instance cannot be connected for the moment. Try again later.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|DiskError|IncorrectDiskStatus.|The error message returned because the status of the specified disk is invalid.|
|403|InstanceExpired|The postPaid instance has been expired. Please ensure your account have enough balance.|The error message returned because the pay-as-you-go instance has expired. Make sure that your account balance is sufficient.|
|403|InstanceExpired|The prePaid instance has been expired.|The error message returned because the subscription instance has expired.|
|403|InstanceNotReady|The specified instance is not ready for use.|The error message returned because the operation is not supported while the resource is in the current state. Try again later.|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|The error message returned because the disk has expired due to overdue payments.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because the requested resources are insufficient in the specified zone. Try other resource types, regions, or zones.|
|403|OperationDenied.SpotPriceLowerThanPublicPrice|The spot instance price is lower than public price.|The error message returned because the user-defined maximum hourly price of a preemptible instance is lower than the spot price.|
|403|IncorrectInstanceStatus|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached. Try another region or instance type, or reduce the purchase quantity. You can also go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|The error message returned because the maximum number of instances of the specified instance type in the current region has been reached, or because the maximum number of vCPUs for all instance types has been reached. Go to the ECS console or Quota Center to request a quota increase.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

