# AttachDisk

调用AttachDisk为一台ECS实例挂载一块按量付费数据盘，或者挂载一块系统盘。实例和云盘必须在同一个可用区。

## 接口说明

调用该接口时，您需要注意：

-   云盘的状态必须为**待挂载**（`Available`）。
-   挂载数据盘时：
    -   目标ECS实例必须处于**运行中**（`Running`）或者**已停止**（`Stopped`）状态。
    -   如果是您单独购买的云盘，计费方式必须是按量付费。
    -   从ECS实例上卸载的系统盘作为数据盘挂载时，不限制计费方式。
-   挂载系统盘时：
    -   目标ECS实例必须是卸载系统盘时的源实例。
    -   目标ECS实例必须处于**已停止**（`Stopped`）状态。
    -   您必须设置实例登录凭证。
-   查询ECS实例信息时，如果返回数据中包含`{"OperationLocks": {"LockReason" : "security"}}`，则禁止一切操作。
-   开启多重挂载特性的云盘，只能挂载到支持NVMe协议的实例上。更多信息，请参见[ESSD云盘支持NVMe](~~256487~~)以及[使用多重挂载功能](~~262105~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=AttachDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AttachDisk|系统规定参数。取值：AttachDisk |
|DiskId|String|是|d-bp1j4l5axzdy6ftk\*\*\*\*|待挂载的云盘ID。云盘（`DiskId`）和实例（`InstanceId`）必须在同一个可用区。

 **说明：** 支持挂载数据盘和系统盘，相关约束条件请参见上文接口说明章节。 |
|InstanceId|String|是|i-bp1dq5lozx5f4pmd\*\*\*\*|目标ECS实例的ID。 |
|Device|String|否|testDeviceName|云盘设备名称。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用其他参数。 |
|DeleteWithInstance|Boolean|否|false|释放实例时，该云盘是否随实例一起释放。

 -   true：释放。
-   false：不释放。云盘会转换成按量付费数据盘而被保留下来。

 默认值：false

 设置该参数时，您需要注意：

 -   将`DeleteWithInstance`置为`false`后，一旦ECS实例被安全控制，即`OperationLocks`中标记了`"LockReason" : "security"`，释放ECS实例时会忽略云盘的该属性，被同时释放。
-   开启多重挂载特性的云盘，不支持设置该参数。 |
|Bootable|Boolean|否|false|是否作为系统盘挂载。

 默认值：false

 **说明：** 设置为`Bootable=true`时，目标ECS实例必须处于无系统盘状态。 |
|Password|String|否|EcsV587!|挂载系统盘时，设置实例的用户名密码，仅对administrator和root用户名生效，其他用户名不生效。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。 |
|KeyPairName|String|否|KeyPairTestName|挂载系统盘时，为Linux系统ECS实例绑定的SSH密钥对的名称。

 -   Windows Server系统：不支持SSH密钥对。即使填写了该参数，只执行`Password`的配置。
-   Linux系统：密码登录方式会被初始化成禁止。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=AttachDisk
&DiskId=d-bp1j4l5axzdy6ftk****
&InstanceId=i-bp1dq5lozx5f4pmd****
&DeleteWithInstance=false
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<AttachDiskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</AttachDiskResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDevice.Malformed|The specified device is not valid.|指定的磁盘设备名不存在。|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|InvalidParameter|The input parameter is mandatory for processing this request is empty.|参数不能为空。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|400|InvalidOperation.InstanceTypeNotSupport|The instance type of the specified instance does not support hot attach disk.|磁盘挂载的实例不支持磁盘热插拔操作。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|InvalidOperation.InstanceTypeNotSupport|The specified disk which has kms key should only attach to ioOptimized instance.|指定的实例无效，只有I/O优化类型的实例支持设置KMS Key。|
|400|InvalidParameter.AllEmpty|%s|您没有输入任何参数，请输入必要的参数。|
|403|InstanceDiskLimitExceeded|The amount of the disk on instance in question reach its limits.|指定实例已经达到可挂载磁盘的最大值。|
|403|InvalidDevice.InUse|The specified device has been occupied.|指定的设备已经挂载了磁盘。|
|403|DiskNotPortable|The specified disk is not a portable disk.|指定的磁盘不是可卸载的磁盘，Portable为false的磁盘无法卸载。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|ResourcesNotInSameZone|The specified instance and disk are not in the same zone.|指定的实例和磁盘不在同一可用区。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|403|DiskError|IncorrectDiskStatus.|指定的磁盘状态不合法。|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|指定的块存储类型不支持此操作。|
|403|DiskId.StatusNotSupported|The specified disk status is not supported.|当前磁盘的状态不支持此操作。|
|403|IncorrectDiskStatus|The operation is not supported in this status.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|InvalidInstanceType.NotSupportDiskCategory|The instanceType of the specified instance does not support this disk category.|指定的实例规格（InstanceType）不支持当前实例的云盘类别。请尝试更换其它实例规格。关于实例规格支持的云盘类型，请参见实例规格族文档。|
|403|InvalidInstanceType.NvmeRequired|The instanceType of the specified instance requires nvme protocol.|指定实例的规格要求使用NVMe协议|
|403|InvalidInstanceType.NvmeUnsupported|The instanceType of the specified instance does not support nvme protocol.|指定实例的规格不支持NVMe协议|
|403|InvalidInstanceType.NotSupportMultiAttachDisk|The instanceType of the specified instance does not support multi attach disk.|指定的实例规格不支持挂载开启多重挂载特性的云盘。|
|403|DiskAttachedNumberExceeded|The attaching times of the specified disk exceeded.|指定的云盘所挂载的实例数量已达上限。|
|403|InvalidOperation.CanNotAttachMultiAttachDiskAsSystemDisk|Multi attach disk can not be attached as system disk.|开启多重挂载特性的云盘不支持作为系统盘使用。|
|403|DeleteWithInstance.Conflict|Multi attach disk cannot be set to DeleteWithInstance attribute.|开启多重挂载特性的云盘不支持设置DeleteWithInstance。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidDisk.InUse|The specified disk has been occupied.|指定的磁盘已占用。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

