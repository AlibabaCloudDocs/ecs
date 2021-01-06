# ModifyDiskSpec

You can call this operation to modify the performance level of an enhanced SSD \(ESSD\).

## Description

To modify the performance level of an enhanced SSD, take note of the following items:

-   You can only upgrade the performance level of a subscription enhanced SSD. However, you can upgrade or downgrade the performance level of a pay-as-you-go enhanced SSD.
-   The enhanced SSD must be in the **In\_Use** or **Available** state.
-   If the enhanced SSD is attached to an ECS instance, the instance must be in the **Running** or **Stopped** state. The instance cannot be in the expired state or stopped due to an overdue payment.
-   If you cannot upgrade the performance level of the enhanced SSD due to its capacity limit, resize the enhanced SSD by calling the [ResizeDisk](~~25522~~) operation and then try again. For more information, see [Enhanced SSDs](~~122389~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyDiskSpec&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDiskSpec|The operation that you want to perform. Set the value to ModifyDiskSpec. |
|DiskId|String|Yes|d-bp131n0q38u3a4zi\*\*\*\*|The ID of the enhanced SSD. |
|PerformanceLevel|String|No|PL2|The performance level of the enhanced SSD. Default value: PL1. Valid values:

-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request. Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include the request format, service limits, available ECS resources, and whether the required parameters are specified. If the check fails, the corresponding error code is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2xx HTTP status code is returned and the request is made. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TaskId|String|null|**Note:** This parameter is in invitational preview and not available. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ModifyDiskSpec
&DiskId=d-bp131n0q38u3a4zi****
&PerformanceLevel=PL2
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyDiskSpecResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyDiskSpecResponse>
```

`JSON` format

```
{
    "RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|The error message returned because you have an overdue payment for the disk.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified instance ID does not exist. Check whether the instance ID is correct.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and your account has no overdue payments.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned because a snapshot is being created from the specified disk.|
|403|OperationDenied|The type of the disk does not support the operation.|The error message returned because the specified disk category does not support this operation.|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|The error message returned because the specified PerformanceLevel parameter is invalid.|
|403|OperationDenied.PerformanceLevelNotMatch|The specified PerformanceLevel and disk size do not match.|The error message returned because the specified performance level and the disk size do not correspond to each other.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

