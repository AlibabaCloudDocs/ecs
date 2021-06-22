# ReplaceSystemDisk

调用ReplaceSystemDisk更换一台ECS实例的系统盘或者操作系统。系统盘的云盘ID会发生变化，原云盘会被释放。

## 接口说明

更换系统盘时，您需要注意：

-   不支持更换系统盘的云盘类型。
-   不支持变更系统盘计费方式。
-   实例的状态必须为已停止（Stopped）状态。

**说明：** 仅适用于专有网络VPC类型实例：如果ECS实例开启了VPC内实例停机不收费功能，为防止地域内ECS实例库存不足而引起更换系统盘后无法重启实例，您需要在停止实例时关闭停机不收费功能。更多信息，请参见[StopInstance](~~25501~~)。

-   ECS实例不能被安全锁定，即实例的`OperationLocks`参数值包含`"LockReason": "security"`。更多信息，请参见[安全锁定时的API行为](~~25695~~)。
-   系统盘挂载的ECS实例不能有未支付的订单。
-   您可以通过参数SystemDisk.Size重新指定系统盘的容量大小。

更换系统盘后，建议您通过以下任一方式验证是否更换成功：

-   通过[DescribeDisks](~~25514~~)接口查询新系统盘的状态。如果已挂载实例，则表示更换系统盘的操作已完成。
-   通过[DescribeInstances](~~25506~~)接口查询更换系统盘的实例的状态。如果返回值`OperationLocks`为空，则表示更换系统盘的操作已完成。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReplaceSystemDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReplaceSystemDisk|系统规定参数。取值：ReplaceSystemDisk |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*\*|指定实例的ID。 |
|ImageId|String|否|m-bp67acfmxazb4ph\*\*\*\*|重置系统时使用的镜像ID。 |
|SystemDisk.Size|Integer|否|80|新的系统盘容量，单位为GiB。取值范围：Max\{20, 参数ImageId对应的镜像大小\}~500

 默认值：Max\{40, 参数ImageId对应的镜像大小\}

 **说明：** 超过`Max{20, 更换前的系统盘容量}`的云盘容量部分，将收取额外费用。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|UseAdditionalService|Boolean|否|true|是否使用阿里云提供的虚拟机系统配置（Windows：NTP、KMS；Linux：NTP、YUM）。

 **说明：** 挂载系统盘时（即设备名为/dev/xvda）有效。 |
|Password|String|否|EcsV587!|是否重置ECS实例的用户名密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 默认值：保持不变。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。

 默认值：false

 **说明：** 使用该参数时，Password参数必须为空。同时您需要确保使用的镜像已经设置了密码。 |
|KeyPairName|String|否|testKeyPairName|密钥对名称。

 **说明：** 该参数仅对Linux系统ECS实例生效。您可以为ECS实例绑定一个SSH密钥对，作为登录凭证。使用了SSH密钥对后，用户名密码的登录凭证方式将被禁用。 |
|Platform|String|否|CentOS|操作系统发行版。取值范围：

 -   CentOS
-   Ubuntu |
|Architecture|String|否|i386|系统架构。取值范围：

 -   i386
-   x86\_64 |
|SecurityEnhancementStrategy|String|否|Active|更换系统盘后，是否免费使用云安全中心服务。取值范围：

 -   Active：使用。该值仅支持公共镜像。
-   Deactive：不使用。该值支持所有镜像。

 默认值：Deactive |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskId|String|d-bp67acfmxazb4ph\*\*\*\*|新系统盘的云盘ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ReplaceSystemDisk
&InstanceId=i-bp67acfmxazb4ph****
&ImageId=m-bp67acfmxazb4ph****
&SystemDisk.Size=80
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&PasswordInherit=false
&KeyPairName=testKeyPairName
&SecurityEnhancementStrategy=Active
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ReplaceSystemDiskResponse>
      <DiskId>d-bp67acfmxazb4ph****</DiskId>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReplaceSystemDiskResponse>
```

`JSON`格式

```
{
    "RequestId": "337568C5-64F3-4B76-8CDD-D3D8C57B5B8C",
    "DiskId": "d-bp67acfmxazb4ph****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|指定的SystemDisk.Size不合法。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|指定的镜像不支持扩容。|
|400|InvalidSystemDiskSize|The specified parameter SystemDisk.Size is invalid.|指定的SystemDisk.Size不合法。|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid|指定的参数SystemDisk.Size不合法。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的Password参数不合法。|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|启用PasswdInherit后，用户名密码应该设置为空。|
|400|OperationDenied|The specified image contains the snapshot of the data disk,does not support this operation.|包含了数据盘快照的镜像，不支持此操作。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|当前操作不支持设置的系统盘大小。|
|400|OperationDenied|%s|拒绝操作。|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|指定的KeyPairName不存在。|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceId is not valid.|指定的实例IO优化配置不合法。|
|400|MissingParameter.Architecture|Architecture should not be null.|参数Architecture不能为空。|
|400|InvalidArchitecture.Malformed|Architecture is not valid.|您输入的参数Architecture无效，请查看该参数格式是否正确。|
|400|MissingParameter.Platform|Platform should not be null.|参数Platform不能为空。|
|400|InvalidPlatform.Malformed|Platform is not valid.|指定的平台无效。|
|400|InvalidParameter.AllEmpty|%s|您没有输入任何参数，请输入必要的参数。|
|400|InvalidDiskId.NotFound|The specified disk do not exist.|指定的磁盘不存在。|
|400|InvalidDatadisk.DiskStatusViolation|The operation is not permitted due to status of the Datadisk.|当前数据盘的状态不支持此操作。|
|400|InvalidDatadisk.DiskCategoryViolation|The operation is not permitted due to category of the Datadisk.|该数据盘的类型不支持该操作。|
|400|InvalidSystemDiskSize.ValueNotSupported|The specified SystemDiskSize is not valid.|指定的SystemDisk.Size不合法。|
|400|MissingParameter|The input parameter "ImageId" that is mandatory for processing this request is not supplied.|参数ImageId不得为空。|
|400|InvalidInstance.NotFoundSystemDisk|The specified instance has no system disk.|指定的实例没有挂载系统盘。请确保指定的实例已挂载了系统盘。您可以调用DescribeInstances查询指定实例的信息。|
|403|InvalidSystemDiskStatus.IsTransfering|The current status of the resource does not support this operation, system disk is transfering.|当前资源的状态不支持此操作，请再系统盘停止传输数据后重试。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的市场镜像不可用，或者指定的用户定义镜像包含产品代码，因为它基于从市场订购的镜像，并且市场中包含完全相同的产品代码的镜像已被删除。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持I/O优化型实例。|
|403|ImageNotSupportInstanceType|The specified image don not support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|403|QuotaExceed.BuyImage|The specified image is from the image market,You have not bought it or your quota has been exceeded.|您暂时不能使用指定的市场镜像。|
|403|INST\_HAS\_UNPAID\_ORDER|The instance has unpaid order.|该实例有未完成的账单。|
|403|OperationDenied.InstanceCreating|The specified instance is creating.|指定的实例已存在。|
|403|InvalidParameter.NotMatch|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|ResourcesNotInSameZone|The specified instance and disk are not in the same zone.|指定的实例和磁盘不在同一可用区。|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|指定的市场镜像不支持该实例规格。|
|403|OperationDenied.UnpaidOrder|The specified instance has unpaid order.|指定的实例ID已存在未支付订单，您可以登录ECS管理控制台支付。|
|403|OperationDenied.ImageNotValid|%s|当前镜像不支持此操作。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidInstanceId.NotFound|The specified instance does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified SystemDisk.Size parameter exceeds the maximum size.|指定的系统盘大小超出最大容量。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数SystemDisk.Size小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|指定的系统盘小于最低容量。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在。|
|500|OperationDenied|Internal Error.|内部错误。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

