# CreateSnapshotGroup

调用CreateSnapshotGroup为指定ECS实例中的云盘创建实例快照。实例快照包含一个或多个云盘对应的快照。

## 接口说明

创建实例快照时，请注意：

-   ECS实例状态为**运行中**（`Running`）或者**已停止**（`Stopped`）。
-   目前只支持ESSD云盘，且云盘状态为**使用中**（`In_use`）。
-   单个实例快照最多包括10块云盘（包括系统盘和数据盘），且总容量不超过32 TiB。
-   您自行创建的快照会一直保留，请定期删除不再需要的快照，避免快照容量持续扣费。
-   开启多重挂载特性的云盘不支持创建实例快照。如果实例挂载了开启多重挂载特性的云盘，您需要设置`ExcludeDiskId.N`参数排除该云盘。

关于实例快照的功能、计费等信息，请参见[实例快照](~~199625~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateSnapshotGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|CreateSnapshotGroup|系统规定参数。取值：CreateSnapshotGroup |
|InstanceId|String|是|i-j6ca469urv8ei629\*\*\*\*|实例ID。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstantAccess|Boolean|否|false|是否开启快照极速可用。取值范围：

 -   true：开启
-   false：关闭

 默认值：false |
|InstantAccessRetentionDays|Integer|否|1|设置快照极速可用的使用时间。单位：天，取值范围：1~65535。

 仅当`InstantAccess=true`时，该参数生效。到期后自动关闭快照极速使用功能。

 默认值：空，表示和快照释放时间一致。 |
|Name|String|否|testName|ECS实例快照名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头，可以包含数字、英文句号（.）、下划线（\_）、短划线（-）或者半角冒号（:）。 |
|Description|String|否|This is description.|描述。长度为2～256个字符，不能以`http://`或`https://`开头。 |
|ExcludeDiskId.N|RepeatList|否|d-j6cf7l0ewidb78lq\*\*\*\*|实例中不需要创建快照的云盘ID。指定云盘ID后，创建的实例快照将不包含该云盘对应的快照。

 默认值：空，表示为实例中的所有云盘创建快照。

 N的取值范围：1~16 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|01ABBD93-1ABB-4D92-B496-1A3D20EC0697|请求ID。 |
|SnapshotGroupId|String|ssg-j6ciyh3k52qp7ovm\*\*\*\*|实例快照ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateSnapshotGroup
&InstanceId=i-j6ca469urv8ei629****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateSnapshotGroupResponse>
      <RequestId>01ABBD93-1ABB-4D92-B496-1A3D20EC0697</RequestId>
      <SnapshotGroupId>ssg-j6ciyh3k52qp7ovm****</SnapshotGroupId>
</CreateSnapshotGroupResponse>
```

`JSON`格式

```
{
	"RequestId": "01ABBD93-1ABB-4D92-B496-1A3D20EC0697",
	"SnapshotGroupId": "ssg-j6ciyh3k52qp7ovm****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSnapshotName.Malformed|The specified SnapshotName is wrongly formed.|快照名称格式不合法。|
|400|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|DiskCategory.OperationNotSupported|The operation is not supported to the specified disk due to its disk category|由于磁盘种类限制，指定的磁盘不支持该操作。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|400|InvalidRetentionDays.Malformed|The specified RetentionDays is not valid.|指定的保留天数无效。请检查RetentionDays参数值是否正确。|
|400|InvalidParameter.Name|The specified Name is invalid.|指定的Name参数无效。|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|当前磁盘有创建中的快照，请您等待创建完成再试。|
|403|InstanceLockedForSecurity|The disk attached instance is locked due to security.|磁盘挂载的实例因安全原因被锁定。|
|403|IncorrectDiskStatus.NeverAttached|The specified disk has never been attached to any instance.|可卸载的云磁盘创建后未被挂载，内容没有变化。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|IncorrectDiskStatus.NeverUsed|The specified disk has never been used after creating.|磁盘创建后未被使用，内容没有变化。|
|403|CreateSnapshot.Failed|The process of creating snapshot is failed.|创建快照失败。|
|403|DiskInArrears|The specified operation is denied as your disk has expired.|磁盘欠费过期。|
|403|DiskId.ValueNotSupported|The specified parameter diskid is not supported.|指定的块存储类型不支持此操作。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|403|IncorrectVolumeStatus|The current volume status does not support this operation.|共享块存储状态不支持当前操作。|
|403|IdempotentParameterMismatch|The specified clientToken is used.|指定的客户令牌已经被使用。|
|403|IncorrectDiskStatus.Invalid|The specified device status invalid, restart instance and try again.|当前磁盘的状态无效，请重启实例后重试。|
|403|IncorrectDiskType.NotSupport|The specified device type is not supported.|指定磁盘存储类型不支持此操作。|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|指定磁盘正在迁移中，请在迁移完毕后重试。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|IdempotentProcessing|The previous idempotent request\(s\) is still processing.|先前的幂等请求仍在处理中，请稍后重试。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|403|InvalidSnapshotCategory.Malformed|The specified Category is not valid.|指定的快照类型无效。请检查Category参数值是否正确。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidDiskId.NotFound|The specified DiskId does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|404|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidVolumeId.NotFound|The specified volume does not exist.|指定的共享块存储不存在，请您检查共享块存储是否正确。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

