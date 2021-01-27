# StopInstance

You can call this operation to stop an ECS instance that is in the Running state. After the operation is called, the status of the instance changes to Stopping and then to Stopped.

## Description

-   You cannot call this operation on ECS instances that are locked for security reasons. An instance is locked for security reasons if `OperationLocks` in the response contains "LockReason": "security" when you query information of the instance. For more information, see [API behavior when an instance is locked for security reasons](~~25695~~).
-   To stop an instance of an instance family that is equipped with local SSDs, take note of the following items:
    -   `ConfirmStop` is a required parameter when you call this operation to stop an [i1](~~25378#i1~~) instance that is attached with [local disks](~~63138~~). Set ConfirmStop to `true`. Otherwise, the call will fail.
    -   After the instance is stopped, data in its local disks is cleared. We recommend that you implement data redundancy at the application layer to ensure data availability.
    -   ECS automatically ignores the `ConfirmStop` parameter in the requests to stop instances of other instance families.
-   If the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled, you can set `StoppedMode` to KeepCharging. Then the instance will continue to be billed after it is stopped. The instance type resources and public IP address are reserved for the instance.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates a sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=StopInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|StopInstance|The operation that you want to perform. Set the value to StopInstance. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of the instance. |
|StoppedMode|String|No|KeepCharging|Specifies whether billing for the instance continues after the instance is stopped. Valid values:

-   StopCharging: Billing stops after the instance is stopped. For information about how `StopCharging` takes effect, see the "Prerequisites" section in [No fees for stopped VPC instances](~~63353~~).
-   KeepCharging: Billing continues after the instance is stopped.

Default value: If the prerequisites required for enabling the No Fees for Stopped Instances \(VPC-Connected\) feature are met and you have enabled this feature in the ECS console, the default value is `StopCharging`. For more information about how to enable the No Fees for Stopped Instances \(VPC-Connected\) feature, see [No Fees for Stopped Instances \(VPC-Connected\)](~~63353#default~~). Otherwise, the default value is `KeepCharging`. |
|ConfirmStop|Boolean|No|true|Specifies whether to confirm the stop operation. This parameter is required and takes effect only for instances of the i1 instance family.

Default value: false. |
|ForceStop|Boolean|No|false|Specifies whether to forcibly stop the instance. Valid values:

-   true: forcibly stops the instance.
-   false: normally stops the instance.

Default value: false. |
|DryRun|Boolean|No|true|Specifies whether to check the validity of the request without actually making the request. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include the required parameters, request format, service limits, and available ECS resources. If the check fails, the corresponding error is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked, and the request is made if the check succeeds.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|1C488B66-B819-4D14-8711-C4EAAA13AC01|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=StopInstance
&InstanceId=i-bp67acfmxazb4ph****
&ConfirmStop=true
&ForceStop=false
&StoppedMode=KeepCharging
&<Common request parameters>
```

Sample success responses

`XML` format

```
<StopInstanceResponse>
      <RequestId>1C488B66-B819-4D14-8711-C4EAAA13AC01</RequestId>
</StopInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "1C488B66-B819-4D14-8711-C4EAAA13AC01"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|DiskError|IncorrectDiskStatus|The error message returned because the specified disk status is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InstanceType.ParameterMismatch|The input parameter ConfirmStop must be true when an instance have localstorage.|The error message returned because the ConfirmStop parameter is set to false for an instance that uses local storage.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|InvalidInstanceId.NotSupport|Classic network Instance does not support this operation.|The error message returned because the operation is not supported by instances in the classic network.|
|403|InvalidInstanceId.NotSupport|Pre pay instance does not support this operation.|The error message returned because subscription instances do not support this operation.|
|403|InvalidInstanceId.NotSupport|Local disk instance does not support this operation.|The error message returned because the operation is not supported by instances that use local disks.|
|403|InvalidInstanceId.NotSupport|Spot instance does not support this operation.|The error message returned because the operation is not supported by preemptible instances.|
|403|IncorrectInstanceStatus|%s|The error message returned because this operation is not supported while the instance is in the current state.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because ECS is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

