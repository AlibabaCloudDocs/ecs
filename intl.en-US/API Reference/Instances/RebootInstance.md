# RebootInstance

You can call this operation to restart an instance that is in the Running state.

## Description

-   Only instances that are in the **Running** \(`Running`\) state can be restarted.
-   After this operation is called, the status of the instance changes to **Starting** \(`Starting`\).
-   An instance can be forcibly restarted. A forced restart \(`ForceStop`\) is equivalent to powering off traditional servers to restart them. This operation can cause data loss if data in the instance is not written to disks.
-   You cannot call this operation on ECS instances that are locked for security reasons. An instance is locked for security reasons if `OperationLocks` in the response contains "LockReason": "security" when you query information of the instance. For more information, see [API behavior when an instance is locked for security reasons](~~25695~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RebootInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RebootInstance|The operation that you want to perform. Set the value to RebootInstance. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of the instance. |
|ForceStop|Boolean|No|false|Specifies whether to forcibly stop the instance to restart it. Default value: false. Valid values:

-   true: forcibly stops the instance. This operation is equivalent to the typical power-off operation. Cache data that is not written to storage in the instance will be lost.
-   false: normally stops the instance. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include the required parameters, request format, service limits, and available ECS resources. If the check fails, the corresponding error is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked, and the request is made if the check succeeds.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=RebootInstance
&InstanceId=i-bp67acfmxazb4ph****
&ForceStop=false
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RebootInstanceResponse>
      <RequestId>F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A</RequestId>
</RebootInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "F2E2C40D-AB09-45A1-B5C5-EB9F5C4E4E4A"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|DiskError|IncorrectDiskStatus.|The error message returned because the specified disk status is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|IncorrectInstanceStatus|%s|The error message returned because this operation is not supported while the instance is in the current state.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

