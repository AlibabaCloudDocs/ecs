# CreateSnapshot

调用CreateSnapshot为一块云盘创建一份快照。

## 接口说明

原本地快照更替为快照极速可用功能。参数说明如下：

-   如果您在2020年12月14日之前使用过本地快照。您可以正常使用参数`Category`和`InstantAccess`，但需要注意：
    -   参数`Category`和`InstantAccess`不能同时传值。
    -   参数`Category`和`InstantAccess`均不传值时，默认创建普通快照。
-   如果您在2020年12月14日之前未使用过本地快照。您只能使用参数`InstantAccess`，不能使用参数`Category`。


以下场景中，您无法为指定的云盘创建快照：

-   云盘保留的手动快照数达到了256份。
-   上份快照还未完成创建。
-   云盘挂载的实例从未启动过。
-   云盘挂载的实例未处于**已停止**（`Stopped`）或者**运行中**（`Running`）状态。
-   查询ECS实例信息时，如果返回数据中包含`{"OperationLocks": {"LockReason" : "security"}}`，则禁止一切操作。

创建快照时，您需要注意：

-   新建一台云服务器ECS或者更换系统盘大约一小时后才可以创建快照，新增一块数据盘可创建快照的时间取决于云盘数据的大小。
-   如果创建快照还未完成，这份快照无法用于创建自定义镜像（[CreateImage](~~25535~~)）。
-   如果云盘已挂载到ECS实例上，创建快照期间请勿变更实例状态。
-   支持对处于**已过期**（`Expired`）状态的云盘创建快照。若创建快照时云盘正好达到过期释放时间，云盘被释放的同时也会删除**创建中**（`Creating`）的快照。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateSnapshot&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSnapshot|系统规定参数。取值：CreateSnapshot |
|DiskId|String|是|d-bp1s5fnvk4gn2tws0\*\*\*\*|云盘ID。 |
|SnapshotName|String|否|testSnapshotName|快照的显示名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 为防止和自动快照的名称冲突，不能以auto开头。 |
|Description|String|否|testDescription|快照的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空 |
|RetentionDays|Integer|否|30|设置快照的保留时间，单位为天。保留时间到期后快照会被自动释放，取值范围：1~65536

 默认值：空，表示快照不会被自动释放。 |
|Category|String|否|Standard|快照类型。取值范围：

 -   Standard：普通快照
-   Flash：本地快照

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用参数`InstantAccess`。该参数和参数`InstantAccess`不能同时传值。更多信息，请参见接口说明。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Tag.N.value|String|否|null|快照的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。 |
|Tag.N.key|String|否|null|快照的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。 |
|Tag.N.Key|String|否|TestKey|快照的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|快照的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|快照所在的企业资源组ID。 |
|InstantAccess|Boolean|否|false|是否开启快照极速可用功能。取值范围：

 -   true：开启。仅ESSD云盘支持开启该功能。
-   false：关闭。即创建普通快照。

 默认值：false

 **说明：** 该参数和参数`Category`不能同时传值。更多信息，请参见接口说明。 |
|InstantAccessRetentionDays|Integer|否|1|设置快照极速可用功能的保留时间，保留时间到期后快照将自动释放。该参数在`InstantAccess=true`时生效。单位：天。取值范围：1~65535。默认与参数`RetentionDays`的值一致。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|SnapshotId|String|s-bp17441ohwka0yuh\*\*\*\*|快照ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateSnapshot
&DiskId=d-bp1s5fnvk4gn2tws0****
&SnapshotName=testSnapshotName
&Description=testDescription
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateSnapshotResponse>
          <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
          <SnapshotId>s-bp17441ohwka0yuh****</SnapshotId>
</CreateSnapshotResponse>
```

`JSON` 格式

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "SnapshotId": "s-bp17441ohwka0yuh****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|快照名称格式不合法。|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|当前磁盘有创建中的快照，请您等待创建完成再试。|
|403|InstanceLockedForSecurity|The disk attached instance is locked due to security.|磁盘挂载的实例因安全原因被锁定。|
|403|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|可卸载的云磁盘创建后未被挂载，内容没有变化。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|磁盘创建后未被使用，内容没有变化。|
|403|CreateSnapshot.Failed|The process of creating snapshot is failed.|创建快照失败。|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|磁盘欠费过期。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|指定的块存储类型不支持此操作。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|共享块存储状态不支持当前操作。|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|指定的共享块存储不存在，请您检查共享块存储是否正确。|
|403|IdempotentParameterMismatch|The specified clientToken is used.|指定的客户令牌已经被使用。|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|当前磁盘的状态无效，请重启实例后重试。|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|指定磁盘存储类型不支持此操作。|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|指定磁盘正在迁移中，请在迁移完毕后重试。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|先前的幂等请求仍在处理中，请稍后重试。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

