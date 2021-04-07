# ModifyDiskSpec

You can call this operation to change the category of a disk or modify the performance level of an enhanced SSD \(ESSD\).

## Description

When you call this operation, take note of the following items:

-   To modify the performance level of an ESSD, take note of the following items:
    -   For a subscription ESSD, you can only upgrade its performance level.
    -   For a pay-as-you-go ESSD, You can upgrade or downgrade its performance level. However, you cannot downgrade the performance level to PL0.
    -   The ESSD must be in the **In Use** \(In\_Use\) or **Unattached** \(Available\) state.
    -   If the ESSD is attached to an ECS instance, the instance must be in the **Running** \(Running\) or **Stopped** \(Stopped\) state. The instance cannot be in the Expired state or stopped due to an overdue payment.
    -   If you cannot upgrade the performance level of an ESSD due to its capacity, resize the ESSD by calling the [ResizeDisk](~~25522~~) operation and then try again. For more information, see [Enhanced SSDs](~~122389~~).
-   For more information about the limits on changing the category of a disk, see the "Limits" section of the [Change the category of a disk](~~161980~~) topic.

The new disk category or performance level takes effect immediately after this operation is executed. Alibaba Cloud calculates the bill based on the new disk category and performance level.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyDiskSpec&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyDiskSpec|The operation that you want to perform. Set the value to ModifyDiskSpec. |
|DiskId|String|Yes|d-bp131n0q38u3a4zi\*\*\*\*|The ID of the ESSD. |
|DiskCategory|String|No|cloud\_essd|The category of the disk. Valid values:

-   cloud\_essd: ESSD
-   cloud\_ssd: standard SSD
-   cloud\_efficiency: ultra disk

This parameter is empty by default, which indicates that the disk category is not changed.

**Note:** The preceding values are listed in descending order of disk performance. The disk cannot be downgraded if it is a subscription disk. |
|PerformanceLevel|String|No|PL2|The performance level of the ESSD. Default value: PL1. Valid values:

-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS. |
|DryRun|Boolean|No|false|Specifies whether to check the validity of the request without actually making the request.request Default value: false. Valid values:

-   true: The validity of the request is checked but the request is not made. Check items include the required parameters, request format, service limits, and available ECS resources. If the check fails, the corresponding error message is returned. If the check succeeds, the `DryRunOperation` error code is returned.
-   false: The validity of the request is checked. If the check succeeds, a 2xx HTTP status code is returned and the request is made. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|20413515388\*\*\*\*|The ID of the generated order.

**Note:** This parameter is returned only when the category of a subscription disk or the performance level of a subscription ESSD is modified. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TaskId|String|t-bp67acfmxazb4p\*\*\*\*|The task ID of changing the disk category.

**Note:** If you only modify the performance level of an ESSD, this parameter is not returned. |

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
    <TaskId>t-bp67acfmxazb4p****</TaskId>
    <RequestId>5B38289D-88AB-42BD-B021-12FC6942F099</RequestId>
    <OrderId>20413515388****</TaskId>
</ModifyDiskSpecResponse>
```

`JSON` format

```
{
  "TaskId": "t-bp67acfmxazb4p****",
  "RequestId": "5B38289D-88AB-42BD-B021-12FC6942F099",
  "OrderId": "20413515388****"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified DiskId parameter does not exist. Check whether the disk ID is correct.|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|The error message returned because you have an overdue payment for the disk.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified instance does not exist. Check whether the InstanceId parameter is correct.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned because a snapshot is being created for the specified disk.|
|403|OperationDenied|The type of the disk does not support the operation.|The error message returned because the specified disk category does not support this operation.|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|The error message returned because the specified PerformanceLevel parameter is invalid.|
|403|OperationDenied.PerformanceLevelNotMatch|The specified PerformanceLevel and disk size do not match.|The error message returned because the specified performance level and the disk size do not correspond to each other.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified disk category is invalid.|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|The error message returned because the requested resources are insufficient in the specified zone. Try other resource types, regions, or zones.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

