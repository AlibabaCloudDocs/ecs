# ReInitDisk

调用ReInitDisk重新初始化一块云盘到创建时的初始状态。

## 接口说明

调用该接口时，您需要注意：

-   云盘的状态必须为**使用中**（In\_use），云盘挂载的ECS实例的状态必须为**已停止**（Stopped）。
-   实例首次启动前，不能重新初始化挂载在其上的云盘。
-   已存在本地快照的云盘，不能重新初始化。
-   开启多重挂载特性的云盘，不能重新初始化。
-   对于系统盘，初始化到镜像的最初状态。若创建云盘的源镜像被删除，则无法初始化。
-   对于直接创建的数据盘，初始化到空盘状态。
-   对于通过快照创建的数据盘，初始化到快照状态。

**说明：** 对于通过快照创建的数据盘，若源快照已被删除，则无法初始化并返回错误。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReInitDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReInitDisk|系统规定参数。取值：ReInitDisk |
|DiskId|String|是|d-bp67acfmxazb4ph\*\*\*\*|指定的云盘ID。 |
|Password|String|否|EcsV587!|重新初始化系统盘时，是否重置ECS实例的用户名密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 其中，Windows实例不能以斜线号（/）为密码首字符。

 **说明：** 如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。 |
|KeyPairName|String|否|testKeyPairName|密钥对名称。

 **说明：** 该参数仅适用于Linux实例。重新初始化系统盘时，您可以为ECS实例绑定一个SSH密钥对，作为登录凭证。使用了SSH密钥对后，用户名密码的登录凭证方式将被禁用。 |
|AutoStartInstance|Boolean|否|true|重新初始化云盘后，是否自动启动实例。

 默认值：false |
|SecurityEnhancementStrategy|String|否|Active|当指定的云盘为系统盘时，重新初始化云盘后是否免费使用云安全中心服务。取值范围：

 -   Active：使用。该值仅支持公共镜像。
-   Deactive：不使用。该值支持所有镜像。

 默认值：Deactive |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ReInitDisk
&DiskId=d-bp67acfmxazb4ph****
&KeyPairName=testKeyPairName
&AutoStartInstance=true
&SecurityEnhancementStrategy=Active
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ReInitDiskResponse>
      <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ReInitDiskResponse>
```

`JSON`格式

```
{
    "RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的Password参数不合法。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|InvalidKeyPairName.NotFound|The specified KeyPairName does not exist.|指定的KeyPairName不存在。|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceId is not valid.|指定的实例IO优化配置不合法。|
|400|InvalidRegionId.MalFormed|The specified RegionId is not valid|指定的RegionId不合法。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|InstanceLockedForSecurity|The instance is locked due to security.|您的资源被安全锁定，拒绝操作。|
|403|InvalidSnapshot.TooOld|The disk is created from a snapshotId made before 2013-07-15, it cannot be re-initiated the specified disk any more since the detached first time.|创建于2013年7月15日之前的快照不支持此操作。|
|403|OperationDenied|The snapshot which is used to create the specified disk has been deleted.|用来创建指定磁盘的快照不存在。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|DiskCreatingSnapshot|The operation is denied due to a snapshot of the specified disk is not completed yet.|指定的磁盘正在创建快照。|
|403|InvalidSourceSnapshot|The snapshot which is used to create the specified disk has been deleted.|用于创建指定磁盘的快照已被删除。|
|403|SharedImageDeleted|The specified image by others shared is deleted.|指定的共享镜像已删除。|
|403|UserNotInTheWhiteList|The user is not in volume white list.|用户不在共享块存储白名单中，请您提交工单申请白名单。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|404|InvalidDiskId.OperationNotSupported|The operation is not supported due to image not exist.|指定的镜像不存在。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

