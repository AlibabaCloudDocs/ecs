# RedeployInstance

You can call this operation to redeploy an ECS instance when the instance receives an event notification.

## Description

RedeployInstance is an asynchronous operation. It migrates data before it restarts the instance. After the instance is redeployed, the instance enters the Running \(`Running`\) state. If the instance fails to be redeployed, the instance returns to the original physical server and its original state.

When you call this operation, take note of the following items:

-   The instance must be in the Running or Stopped state. After the instance is redeployed, the status of the instance has the following changes:
    -   If the instance is in the Running \(`Running`\) state, the instance enters the Stopping `Stopping` state.
    -   If the instance is in the Stopped \(`Stopped`\) state, the instance enters the Starting \(`Starting`\) state.
-   Instances on dedicated hosts cannot be redeployed.
-   If `OperationLocks` in the DescribeInstances response contains `"LockReason": "security"` for the instance, the instance is locked for security reasons and cannot be redeployed.
-   If the instance receives simulated events that are created by calling the CreateSimulatedSystemEvent operation, you cannot redeploy the instance by calling the RedeployInstance operation.
-   When you handle local disk-related system events, if the damaged local disks are isolated but the SystemMaintenance.RebootAndReInitErrorDisk \(**instance restart and re-initialization of damaged disks due to system maintenance**\) event is not sent, you can still call the RedeployInstance operation to redeploy the instance. For more information, see [Overview of system events on ECS instances equipped with local disks](~~107693~~).

The following table lists the types and status of events to which you can respond by calling the RedeployInstance operation.

|System event

|Status |
|--------------|--------|
|Instance restart due to system maintenance \(SystemMaintenance.Reboot\)

|Inquiring and Scheduled |
|Instance redeployment due to system maintenance \(SystemMaintenance.Redeploy\)

|Inquiring and Scheduled |
|Instance restart and replacement of damaged disks due to system maintenance \(SystemMaintenance.RebootAndIsolateErrorDisk\)

|Inquiring |
|Instance restart and re-initialization of damaged disks due to system maintenance \(SystemMaintenance.RebootAndReInitErrorDisk\)

|Inquiring |
|Instance redeployment due to a system error \(SystemFailure.Redeploy\)

|Inquiring and Scheduled |
|For instances equipped with local disks only: instance restart due to a system error \(SystemFailure.Reboot\)

|Executing |
|Isolation of damaged disks due to system maintenance \(SystemMaintenance.IsolateErrorDisk\)

|Inquiring |
|Re-initialization of damaged disks due to system maintenance \(SystemMaintenance.ReInitErrorDisk\)

|Inquiring |

**Note:** When the system redeploys instances equipped with local disks, the local disks are re-initialized and data in the local disks is cleared.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=RedeployInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RedeployInstance|The operation that you want to perform. Set the value to RedeployInstance. |
|InstanceId|String|Yes|i-bp1azkttqpldxgted\*\*\*\*|The ID of the instance. |
|ForceStop|Boolean|No|false|Specifies whether to force stop the instance in the Running state.

Default value: false.

**Note:** The effect of a forced stop is the same as a power failure. Data in the instance operating system that has not been written to local disks may be lost. We recommend that you redeploy instances when they are in the Stopped state. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TaskId|String|t-bp10e8orkp8x\*\*\*\*|The ID of the redeployment task.

You can call the [DescribeTasks](~~25622~~) operation to query the migration result. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=RedeployInstance
&InstanceId=i-bp1azkttqpldxgted****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RedeployInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <TaskId>t-bp10e8orkp8x****</TaskId>
</RedeployInstanceResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "TaskId": "t-bp10e8orkp8x****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|The error message returned because the operation is not supported while the instance is locked for security reasons.|
|403|DiskError|IncorrectDiskStatus.|The error message returned because the specified disk status is invalid.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the problem persists, submit a ticket.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance and try again.|
|403|IncorrectInstanceStatus|%s|The error message returned because the operation is not supported while the instance is in the current state.|
|403|InvalidOperation.RedeployInstance|%s|The error message returned because the operation is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

