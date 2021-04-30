# ResizeDisk

You can call this operation to resize a system disk or data disk.

## Description

**Note:** Before you call this operation, you must check the partition format of the disk. You cannot resize an MBR-formatted disk to greater than or equal to 2 TiB without data loss. To resize an MBR-formatted disk to greater than or equal to 2 TiB in size, we recommend that you create and attach a new data disk with the desired size. Then, you can partition and format the new data disk to GPT and copy data from the MBR-formatted data disk to the new GPT-formatted data disk. For more information, see [Resize cloud disks offline](~~44986~~).

-   You can resize the following categories of disks: basic disks \(`cloud`\), ultra disks \(`cloud_efficiency`\), standard SSDs \(`cloud_ssd`\), and enhanced SSDs \(ESSDs\) \(`cloud_essd`\).
-   You cannot resize a disk when a snapshot is being created for the disk.
-   The instance to which the disk to be resized is attached must be in the **Running** \(`Running`\) or **Stopped** \(`Stopped`\) state.
-   After you resize a disk, its partitions and file systems are not changed. You must manually allocate the storage space on the disk after it is resized.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ResizeDisk&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ResizeDisk|The operation that you want to perform. Set the value to ResizeDisk. |
|DiskId|String|Yes|d-bp67acfmxazb4p\*\*\*\*|The ID of the disk. |
|NewSize|Integer|Yes|1900|The new disk capacity. Unit: GiB. Valid values:

-   Ultra disk \(cloud\_efficiency\): 20 to 32768
-   Standard SSD \(cloud\_ssd\): 20 to 32768
-   Enhanced SSD \(cloud\_essd\): 20 to 32768
-   Basic disk \(cloud\): 5 to 2000

The new disk capacity must be greater than the original disk capacity. |
|Type|String|No|offline|The method that you use to resize the disk. Default value: offline. Valid values:

-   offline. After you resize a disk offline, you must restart the instance by using the ECS console or by calling the RebootInstance operation for the resizing operation to take effect. For more information, see [Restart the instance](~~25440~~) and [RebootInstance](~~25502~~).
-   online. After you resize a disk online, the resizing operation takes effect immediately and you do not need to restart the instance. You can resize ultra disks, standard SSDs, and ESSDs online. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|OrderId|String|20413515388\*\*\*\*|The ID of the order.

**Note:** This parameter is returned only when subscription disks are resized. |
|RequestId|String|F3CD6886-D8D0-4FEE-B93E-1B73239673DE|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ResizeDisk
&DiskId=d-bp67acfmxazb4p****
&NewSize=1900
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ResizeDiskResponse>
      <OrderId>20413515388****</OrderId>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResizeDiskResponse>
```

`JSON` format

```
{
    "OrderId": "20413515388****",
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|The error message returned because the specified DataDisk.N.Size parameter is invalid or the snapshot size exceeds the maximum capacity that is allowed for the specified category.|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|The error message returned because the specified disk does not exist. Check whether the disk ID is correct.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified Instance does not exist. Check whether the instance ID is correct.|
|403|OperationDenied|The type of the disk does not support the operation.|The error message returned because the specified disk category does not support this operation.|
|403|OperationDenied|The status of the disk or the instance that the disk is attaching with does not support the operation.|The error message returned because the operation is not supported while the disk or instance is in the current state.|
|403|InvalidDiskSize.TooSmall|Specified new disk size is less than the original disk size.|The error message returned because the specified new disk capacity is smaller than the original disk capacity.|
|403|InvalidDiskSize.TooLarge|Specified new disk size is beyond the permitted range.|The error message returned because the specified new disk capacity exceeds the capacity limit.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|DiskError|IncorrectDiskStatus|The error message returned because the status of the specified disk is invalid.|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|The error message returned because you have overdue payments for the disk.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned because a snapshot is being created for the specified disk.|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|The error message returned because the specified data disk category is invalid.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidDataDiskSize.ValueNotSupported|%s|The error message returned because the specified data disk capacity is invalid.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned because the specified system disk size is not supported.|
|403|InvalidDiskSize|Specified new disk size is less than or equal the original disk size.|The error message returned because the specified new disk capacity is smaller than or equal to the original disk capacity.|
|400|IncompleteParamter|Some fields can not be null in this request.|The error message returned because some required parameters are not specified.|
|403|Operation.Conflict|The operation may conflicts with others.|The error message returned because the operation conflicts with other operations.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned because the operation is not supported while the resource is locked for security reasons.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments for it.|
|403|UserNotInTheWhiteList|The user is not in disk white list.|The error message returned because you are not authorized to manage the disk. Try again when you are authorized.|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|The error message returned because the specified RegionId parameter is invalid.|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|The error message returned because the specified disk category does not support the current operation.|
|400|InvalidParam.Type|The specified type is not supported.|The error message returned because the specified Type parameter is invalid.|
|403|InvalidRegion.NotSupport|The specified region does not support resize online.|The error message returned because online resizing is not supported in the specified region.|
|403|InvalidDiskCategory.NotSupported|The specified disk category does not support resize online.|The error message returned because the specified disk category does not support online resizing.|
|403|IncorrectInstanceStatus|The current status of the resource does not support resize online.|The error message returned because this operation is not supported while the resource is in the current state.|
|403|InvalidInstanceStatus.NotRunning|The status of instance to which the disk attachs must be running when resizing online.|The error message returned because the instance to which the disk is attached is not in the Running state when you resize the disk online.|
|403|IncorrectDiskStatus|The current status of the resource does not support resize online|The error message returned because online resizing is not supported while the resource is in the current state.|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|The error message returned because the order is being processed. Try again later.|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|The error message returned because the customer master key \(CMK\) is not enabled when a Key Management Service \(KMS\) key ID is specified for a disk. You can call the DescribeKey operation provided by KMS to query the information about a specific CMK.|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|The error message returned because Elastic Compute Service \(ECS\) is not authorized to access your KMS resources.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|The error message returned because risks are detected in your default credit card or debit card. Click the link in the email for verification.|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|The error message returned because disks created by using the specified image cannot be resized.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

