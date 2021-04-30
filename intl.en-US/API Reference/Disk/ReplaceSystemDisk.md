# ReplaceSystemDisk

You can call this operation to replace the system disk or operating system of an Elastic Compute Service \(ECS\) instance. After the system disk is replaced, the ID of the system disk changes and the original disk is released.

## Description

When you call this operation, take note of the following items:

-   You cannot change the category of the system disk.
-   You cannot change the billing method of the system disk.
-   The instance must be in the Stopped \(Stopped\) state.

**Note:** For VPC-type instances only: You must disable the No Fees for Stopped Instances \(VPC-Connected\) feature when you stop an instance. This prevents the instance from failing to be restarted due to insufficient ECS resources after the system disk is replaced. For more information, see [StopInstance](~~25501~~).

-   The instance must not be locked for security reasons. If the value of `LockReason` in `OperationLocks` is security in the response when you query details of an instance, the instance is locked for security reasons. For more information, see [API behavior when an instance is locked for security reasons](~~25695~~).
-   You cannot have overdue payments for the instance to which the system disk is attached.
-   You can configure the SystemDisk.Size parameter to re-specify the capacity of the new system disk.

After you call this operation, you can use one of the following methods to check whether the system disk is replaced:

-   You can call the [DescribeDisks](~~25514~~) operation to query the status of the new system disk. If the new system disk is in the In\_use state, the system disk is replaced.
-   You can call the [DescribeInstances](~~25506~~) operation to query the status of the instance whose system disk is replaced. If `OperationLocks` is empty for the instance in the response, the system disk is replaced.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ReplaceSystemDisk&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ReplaceSystemDisk|The operation that you want to perform. Set the value to ReplaceSystemDisk. |
|InstanceId|String|Yes|i-bp67acfmxazb4ph\*\*\*\*|The ID of the instance. |
|ImageId|String|No|m-bp67acfmxazb4ph\*\*\*\*|The ID of the image to be used to replace the system disk. |
|SystemDisk.Size|Integer|No|80|The capacity of the new system disk. Unit: GiB. Valid values: Max\{20, the size of the image specified by ImageId\} to 500.

 Default value: Max\{40, the size of the image specified by ImageId\}.

 **Note:** You are charged for the capacity that exceeds `Max{20, the capacity of the original system disk}`. |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000|The client token that is used to ensure the idempotence of the request You can use the client to generate the value, but you must make sure that it is unique among different requests. The **ClientToken** value must contain only ASCII characters and cannot exceed 64 characters in length. For more information, see [How to ensure idempotence](~~25693~~). |
|UseAdditionalService|Boolean|No|true|Specifies whether to use the system configurations for virtual machines provided by Alibaba Cloud \(Windows: NTP and KMS. Linux: NTP and YUM\).

 **Note:** This parameter takes effect only when you attach a system disk, whose device name is /dev/xvda. |
|Password|String|No|EcsV587!|The new password of the instance. The password must be 8 to 30 characters in length and include at least three of the following characters types: uppercase letters, lowercase letters, digits, and special characters. Special characters include

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 The password of a Windows instance cannot start with a forward slash \(/\).

 This parameter is empty by default, which indicates that the current password remains unchanged.

 **Note:** If the `Password` parameter is specified, we recommend that you send requests over HTTPS to avoid password leaks. |
|PasswordInherit|Boolean|No|false|Specifies whether to use the password that is preset in the image.

 Default value: false

 **Note:** If the PasswordInherit parameter is specified, you must leave the Password parameter empty and make sure that the selected image has a password preset. |
|KeyPairName|String|No|testKeyPairName|The name of the SSH key pair.

 **Note:** This parameter is applicable only to Linux instances. You can bind an SSH key pair to the instance as a logon credential. However, the password logon method is disabled after you bind the SSH key pair. |
|Platform|String|No|CentOS|The distribution of the operating system. Valid values:

 -   CentOS
-   Ubuntu |
|Architecture|String|No|i386|The system architecture. Valid values:

 -   i386
-   x86\_64 |
|SecurityEnhancementStrategy|String|No|Active|Specifies whether to activate Security Center for free after you replace the system disk. Valid values:

 -   Active: Security Center is used for free after the system disk is replaced. This value is applicable only to public images.
-   Deactive: Security Center is not used for free after the system disk is replaced. This value is applicable to all images.

 Default value: Deactive. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|DiskId|String|d-bp67acfmxazb4ph\*\*\*\*|The ID of the new system disk. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=ReplaceSystemDisk
&InstanceId=i-bp67acfmxazb4ph****
&ImageId=m-bp67acfmxazb4ph****
&SystemDisk.Size=80
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&PasswordInherit=false
&KeyPairName=testKeyPairName
&SecurityEnhancementStrategy=Active
&<Common Request Parameters>
```

Sample success responses

`XML` format

```
<ReplaceSystemDiskResponse>
      <DiskId>d-bp67acfmxazb4ph****</DiskId>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReplaceSystemDiskResponse>
```

`JSON` format

```
{
    "RequestId": "337568C5-64F3-4B76-8CDD-D3D8C57B5B8C",
    "DiskId": "d-bp67acfmxazb4ph****"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|404|InvalidInstanceId.NotFound|The specified instance does not exist.|The error message returned because the specified Instance does not exist. Check whether the instance ID is correct.|
|403|InvalidSystemDiskStatus.IsTransfering|The current status of the resource does not support this operation, system disk is transfering.|The error message returned because the operation is not supported while the resource is in the current state. Try again after the system disk stops transmitting data.|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|The error message returned because the operation is not supported while the disk is in the current state. Make sure that the disk is available and you have no overdue payments.|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|The error message returned because the specified image does not exist within this account. Check whether the image ID is correct.|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|The error message returned because the operation is not supported while the resource is in the current state.|
|403|InstanceLockedForSecurity|The instance is locked due to security.|The error message returned because the operation is not supported while the resource is locked for security reasons.|
|403|ImageNotSubscribed|The specified image has not be subscribed.|The error message returned because you have not subscribed to the specified Alibaba Cloud Marketplace image.|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|The error message returned because the specified Alibaba Cloud Marketplace image is unavailable, or because the specified custom image contains the product code of the Alibaba Cloud Marketplace image from which the custom image is derived and the Alibaba Cloud Marketplace image has been removed from Alibaba Cloud Marketplace.|
|500|OperationDenied|Internal Error.|The error message returned because an unknown internal error occurs.|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|The error message returned because the specified image does not support the specified instance type.|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|The error message returned because the specified system disk size exceeds the allowed maximum size.|
|500|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned because the subscription instance has expired. Renew the instance first.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned because the billing method of the instance does not support this operation.|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|The error message returned because a snapshot of the specified disk is being created.|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|The error message returned because the specified image is not supported for I/O optimized instances.|
|403|ImageNotSupportInstanceType|The specified image don not support the InstanceType instance.|The error message returned because the specified image does not support the specified instance type.|
|403|QuotaExceed.BuyImage|The specified image is from the image market,You have not bought it or your quota has been exceeded.|The error message returned because you have not purchased the specified Alibaba Cloud Marketplace image or you have no image quotas.|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|The error message returned because the specified system disk size is smaller than the size of the image.|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|The error message returned because the specified system disk size is smaller than the minimum size.|
|404|NoSuchResource|The specified resource is not found.|The error message returned because the specified resource does not exist.|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|The error message returned because the specified image does not support resizing.|
|400|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|403|INST\_HAS\_UNPAID\_ORDER|The instance has unpaid order.|The error message returned because you have unpaid orders for the instance.|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|The error message returned because the specified Password parameter is invalid.|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|The error message returned because the Password parameter is specified when PasswdInherit is configured.|
|400|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|The error message returned because the operation is not supported while the image contains data disk snapshots.|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|The error message returned because the specified SystemDisk.Category parameter is invalid.|
|403|OperationDenied.InstanceCreating|The specified instance is creating.|The error message returned because the specified instance is being created.|
|400|InvalidParameter.Conflict|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|The error message returned because the specified system disk size is not supported.|
|400|OperationDenied|%s|The error message returned because the operation is denied.|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|The error message returned because the specified KeyPairName parameter does not exist.|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceId is not valid.|The error message returned because the specified InstanceId parameter is invalid.|
|403|InvalidParameter.NotMatch|%s|The error message returned because a specified parameter is invalid. Check whether parameter conflicts exist.|
|400|MissingParameter.Architecture|Architecture should not be null.|The error message returned because the Architecture parameter is not specified.|
|400|InvalidArchitecture.Malformed|Architecture is not valid.|The error message returned because the specified Architecture parameter is invalid.|
|400|MissingParameter.Platform|Platform should not be null.|The error message returned because the Platform parameter is not specified.|
|400|InvalidPlatform.Malformed|Platform is not valid.|The error message returned because the specified Platform parameter is invalid.|
|400|InvalidParameter.AllEmpty|%s|The error message returned because the required parameters are not specified.|
|400|InvalidDiskId.NotFound|The specified disk do not exist.|The error message returned when the specified disk does not exist.|
|400|InvalidDatadisk.DiskStatusViolation|The operation is not permitted due to status of the Datadisk.|The error message returned because the operation is not supported while the data disk is in the current state.|
|400|InvalidDatadisk.DiskCategoryViolation|The operation is not permitted due to category of the Datadisk.|The error message returned because the category of the data disk does not support the operation.|
|403|ResourcesNotInSameZone|The specified instance and disk are not in the same zone.|The error message returned because the specified instance and disk are not in the same zone.|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified SystemDiskSize is not valid.|The error message returned because the specified SystemDisk.Size parameter is invalid.|
|400|MissingParameter|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|The error message returned because the ImageId parameter is not specified.|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|The error message returned because the specified Alibaba Cloud Marketplace image does not support the instance type.|
|400|InvalidInstance.NotFoundSystemDisk|The specified instance has no system disk.|The error message returned because the specified instance has no system disk attached. Make sure that the specified instance has a system disk attached. You can call the DescribeInstances operation to query the most recent instance list.|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|
|403|OperationDenied.UnpaidOrder|The specified instance has unpaid order.|The error message returned because you have unpaid orders for the specified instance. You can log on to the ECS console to pay for the orders.|
|403|OperationDenied.ImageNotValid|%s|The error message returned because the image does not support the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

