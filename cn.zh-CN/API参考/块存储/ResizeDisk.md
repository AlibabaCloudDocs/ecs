# ResizeDisk

调用ResizeDisk扩容一块云盘，支持扩容系统盘和数据盘。

## 接口说明

**说明：** 扩容前，请务必查询云盘采用的分区格式。如果是MBR格式，不支持扩容到2TiB以上，否则会造成数据丢失。对于MBR分区扩容，建议您重新创建并挂载一块数据盘，采用GPT分区格式后，再将已有数据拷贝至新的数据盘上。更多详情，请参见[扩容云盘容量](~~44986~~)。

-   支持扩容的云盘类型包括普通云盘（`cloud`）、高效云盘（`cloud_efficiency`）、SSD云盘（`cloud_ssd`）和ESSD（`cloud_essd`）云盘。
-   当云盘正在创建快照时，不允许扩容。
-   云盘挂载的实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`）。
-   扩容时，不会修改云盘分区和文件系统，您需要在扩容后自行分配存储空间。
-   开启多重挂载特性的云盘只支持离线扩容。扩容前，您需要确保所挂载的全部实例均为**已停止**（`Stopped`）状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ResizeDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ResizeDisk|系统规定参数。取值：ResizeDisk |
|DiskId|String|是|d-bp67acfmxazb4p\*\*\*\*|云盘ID。 |
|NewSize|Integer|是|1900|希望扩容到的云盘容量大小。单位为GiB。取值范围：

 -   高效云盘（cloud\_efficiency）：20~32768
-   SSD云盘（cloud\_ssd）：20~32768
-   ESSD云盘（cloud\_essd）：20~32768
-   普通云盘（cloud）：5~2000

 指定的新云盘容量必须比原云盘容量大。 |
|Type|String|否|offline|扩容云盘的方式。取值范围：

 -   offline（默认）：离线扩容。扩容后，您必须在控制台[重启实例](~~25440~~)或者调用API [RebootInstance](~~25502~~)使操作生效。
-   online：在线扩容，无需重启实例即可完成扩容。云盘类型支持高效云盘、SSD云盘和ESSD云盘。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|20413515388\*\*\*\*|生成的订单ID。

 **说明：** 仅在扩容包年包月云盘时会返回订单ID。 |
|RequestId|String|F3CD6886-D8D0-4FEE-B93E-1B73239673DE|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ResizeDisk
&DiskId=d-bp67acfmxazb4p****
&NewSize=1900
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ResizeDiskResponse>
      <OrderId>20413515388****</OrderId>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ResizeDiskResponse>
```

`JSON`格式

```
{
    "OrderId": "20413515388****",
    "RequestId": "F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的DataDisk.n.Size超出允许范围，或者快照的容量超过指定磁盘类别的大小限制。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|指定的数据磁盘类型无效。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|指定的数据盘容量无效。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|当前操作不支持设置的系统盘大小。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|400|InvalidParam.Type|The specified type is not supported.|指定的参数Type无效。|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|订单正在处理中，稍后重试。|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|指定的镜像不支持扩容。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|403|OperationDenied|The status of the disk or the instance that the disk is attaching with does not support the operation.|此磁盘或实例状态无法执行指定的操作。|
|403|InvalidDiskSize.TooSmall|Specified new disk size is less than the original disk size.|指定的新磁盘小于原始磁盘。|
|403|InvalidDiskSize.TooLarge|Specified new disk size is beyond the permitted range.|指定的新磁盘大小超过限制。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskError|IncorrectDiskStatus|指定的磁盘状态不合法。|
|403|DiskInArrears|The specified operation is denied as your disk owing fee.|指定的磁盘已欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|InvalidDiskSize|Specified new disk size is less than or equal the original disk size.|指定的新磁盘大小必须大于原始磁盘大小。|
|403|Operation.Conflict|The operation may conflicts with others.|该操作与其他操作冲突。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|指定的云盘类型不支持当前操作。|
|403|InvalidRegion.NotSupport|The specified region does not support resize online.|该地域不支持在线扩容。|
|403|InvalidDiskCategory.NotSupported|The specified disk category does not support resize online.|指定的磁盘类型不支持在线扩容。|
|403|IncorrectInstanceStatus|The current status of the resource does not support resize online.|当前资源的状态不支持此操作。|
|403|InvalidInstanceStatus.NotRunning|The status of instance to which the disk attachs must be running when resizing online.|在线调整磁盘大小时，磁盘连接到的实例的状态必须正在运行。|
|403|IncorrectDiskStatus|The current status of the resource does not support resize online|当前资源的状态不支持在线扩容。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|我们检测到您的默认信用卡或借记卡存在安全风险。请通过电子邮件中的链接进行验证。|
|403|InvalidOperation.MultiAttachDiskNotSupportResizeOnline|Multi attach disk does not support resize online.|开启多重挂载特性的云盘不支持在线扩容。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

