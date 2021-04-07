# CreateImage

调用CreateImage创建一份自定义镜像。您可以使用创建的自定义镜像创建ECS实例（RunInstances），或者更换实例的系统盘（ReplaceSystemDisk）。

## 接口说明

调用该接口时，您需要注意：

-   等待镜像状态变为可用（Available）后才能使用镜像资源。
-   查询ECS实例信息时，如果返回数据中包含`{"OperationLocks": {"LockReason" : "security"}}`，则禁止一切操作。

以下描述了三种通过该接口创建自定义镜像的方法。请求参数的优先级为：`InstanceId` \> `DiskDeviceMapping` \> `SnapshotId`，若您的请求中同时含有两个及以上参数，默认以优先级更高的参数为准创建镜像。

-   **方法一**：使用一台实例做模板，只需要指定实例ID（`InstanceId`）。该台实例的状态必须为运行中（`Running`）或者已停止（`Stopped`）。接口调用成功后，该台实例的每块云盘均会新增一份快照。由于运行中的实例存在缓存数据未落盘的情况，可能导致创建的自定义镜像数据与实例数据不完全一致。因此阿里云推荐您停止实例（[StopInstances](~~155372~~)）后创建镜像。
-   **方法二**：针对某一台实例的系统盘创建自定义镜像，只需要指定实例系统盘的一份历史快照ID（`SnapshotId`）。其中，指定的快照不能是2013年7月15日（含）之前创建的快照。
-   **方法三**：将多份快照组合成一个镜像模板，需要建立几块云盘的数据关联（`DiskDeviceMapping`）。

使用方法三创建自定义镜像时，请注意：

-   只能指定一个系统盘快照，系统盘的设备名必须为/dev/xvda。
-   可以指定多个数据盘快照，数据盘设备名默认由系统有序分配，从/dev/xvdb依次排序到/dev/xvdz，不能重复。
-   可以不指定`SnapshotId`，不指定时会创建一个指定大小的没有任何数据的空数据盘。
-   指定的快照不能是2013年7月15日（含）之前创建的快照。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateImage&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateImage|系统规定参数。取值：CreateImage |
|RegionId|String|是|cn-hangzhou|镜像所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DiskDeviceMapping.N.SnapshotId|String|否|s-bp17441ohwkdca0\*\*\*\*|根据指定的快照创建自定义镜像。 |
|DiskDeviceMapping.N.Size|Integer|否|2000|DiskDeviceMapping.N云盘的大小，单位为GiB。DiskDeviceMapping.N.Size的取值和默认值和DiskDeviceMapping.N.SnapshotId有关：

 -   如果没有指定SnapshotId，Size取值以及默认值为：
    -   普通云盘：5~2000GiB，默认为5
    -   其他云盘：20~32768GiB，默认为20
-   如果指定了SnapshotId，Size取值必须大于等于SnapshotId的大小，默认为SnapshotId的大小。 |
|DiskDeviceMapping.N.Device|String|否|/dev/vdb|指定DiskDeviceMapping.N在自定义镜像中的设备名称。取值范围：

 -   其他云盘（例如SSD云盘、高效云盘和ESSD云盘）：/dev/vda~/dev/vdz
-   普通云盘：/dev/xvda~/dev/xvdz |
|DiskDeviceMapping.N.DiskType|String|否|system|指定DiskDeviceMapping.N.在新镜像中的云盘类型。您可以通过该参数使用数据盘快照做为镜像的系统盘，如果不指定，默认为快照对应的云盘类型。取值范围：

 -   system：系统盘
-   data：数据盘 |
|SnapshotId|String|否|s-bp17441ohwkdca0\*\*\*\*|根据指定的快照创建自定义镜像。 |
|InstanceId|String|否|i-bp1g6zv0ce8oghu7\*\*\*\*|实例ID。 |
|ImageName|String|否|TestCentOS|镜像名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|Description|String|否|ImageTestDescription|镜像的描述信息。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空 |
|Platform|String|否|CentOS|指定数据盘快照做镜像的系统盘后，需要通过Platform确定系统盘的操作系统发行版。取值范围：

 -   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   RedHat
-   Debian
-   CoreOS
-   Aliyun
-   Windows Server 2012
-   Windows 7
-   Customized Linux
-   Others Linux（默认） |
|Architecture|String|否|x86\_64|指定数据盘快照做镜像的系统盘后，需要通过Architecture确定系统盘的系统架构。取值范围：

 -   i386
-   x86\_64（默认） |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Tag.N.value|String|否|null|镜像的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。 |
|Tag.N.key|String|否|null|镜像的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。 |
|Tag.N.Key|String|否|KeyTest|镜像的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|ValueTest|镜像的标签值。N的取值范围：1~20。一旦传入该值，允许为空字符串。最多支持128个字符，不能以acs:开头，不能包含http://或者https://。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|自定义镜像所在的企业资源组ID。 |
|ImageFamily|String|否|hangzhou-daily-update|镜像族系名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以aliyun和acs:开头，不能包含http://或者https://。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageId|String|m-bp146shijn7hujku\*\*\*\*|镜像ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateImage
&RegionId=cn-hangzhou
&DiskDeviceMapping.1.Size=2000
&DiskDeviceMapping.1.SnapshotId=s-bp17441ohwkdca0****
&DiskDeviceMapping.1.DiskType=system
&SnapshotId=s-bp17441ohwkdca0****
&InstanceId=i-bp1g6zv0ce8oghu7****
&ImageName=TestCentOS
&ImageVersion=2017011017
&Description=ImageTestDescription
&Platform=CentOS
&Architecture=x86_64
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=KeyTest
&Tag.1.Value=ValueTest
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateImageResponse>
      <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
      <ImageId>m-bp146shijn7hujku****</ImageId>
</CreateImageResponse>
```

`JSON`格式

```
{
    "RequestId": "C8B26B44-0189-443E-9816-D951F59623A9",
    "ImageId": "m-bp146shijn7hujku****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidImageName.Malformed|The specified Image name is wrongly formed.|镜像名称格式错误。长度为2~128个字符。必须以大小字母或中文开头，不能以aliyun和acs:开头，不能包含http://或者https://。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。|
|400|InvalidImageName.Duplicated|The specified Image name has already bean used.|镜像名称已经重复。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidImageVersion.Malformed|The specified ImageVersion is wrongly formed.|无效的镜像版本号取值（或者您无权使用该快照）。|
|403|InvalidSnapshotId.NotReady|The current status of the DiskDeviceMapping.n.SnapshotId or SnapshotId does not support this operation.|指定的快照状态不支持该操作。|
|403|InvalidSnapshot.TooOld|This operation is denied because the specified snapshot by DiskDeviceMapping.n.SnapshotId or SnapshotId is created before 2013-07-15.|该操作被拒绝。因为DiskDeviceMapping.n.SnapshotId或SnapshotId指定的快照创建于2013-07-15之前。|
|403|OperationDenied|The specified snapshot is not allowed to create image.|指定快照不允许创建镜像。|
|403|QuotaExceed.Image|The Image Quota exceeds.|自定义镜像额度已用完。|
|403|OperationDenied|The specified snapshot is not from system disk.|指定的快照不是系统盘快照。|
|403|InvalidParamter.Conflict|The specified same token is trying to make requests with different parameters.|同一个Token正在请求处理两个不同的参数。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|IncorrectInstanceStatus|The current status of the instance does not support this operation.|当前实例状态不支持此操作。|
|400|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|400|InvalidDevice.Malformed|The specified parameter DiskDeviceMapping.n.Device is not valid.|指定的参数DiskDeviceMapping.n.Device不合法。|
|400|MissingParameter|The input parameter SnapshotId or InstanceId or DiskDeviceMapping that is mandatory for processing this request is not supplied.|参数SnapshotId，InstanceId和DiskDeviceMapping不得为空。|
|400|InvalidSize.ValueNotSupported|The specified parameter DiskDeviceMapping.n.Size beyond the permitted range.|指定的参数DiskDeviceMapping.n.Size超出取值范围。|
|400|InvalidDevice.InUse|The specified parameter DiskDeviceMapping.n.Device has been occupied.|指定的参数DiskDeviceMapping.n.Device已被占用。|
|400|OperationDenied|The specified parameter DiskDeviceMapping.n.SnapshotId does not contain system disk snapshot.|系统盘快照中不存在指定的DiskDeviceMapping快照ID。|
|400|OperationDenied|The specified parameter DiskDeviceMapping.n.SnapshotId contains two or more system disk snapshots.|指定的DiskDeviceMapping快照ID中已存在系统盘快照。|
|400|InvalidDiskCategory.CreateImage|The specified diskCategory is not allowed to create image.|指定的磁盘类型不允许创建镜像。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|403|UserNotInTheWhiteList|The user is not in the white list of create image by data disk snapshot.|您不能通过数据磁盘快照创建镜像，请先加入到该白名单中。|
|400|InvalidArchitecture.Malformed|The specified Architecture is wrongly formed.|参数Architecture格式错误。|
|400|InvalidPlatform.Malformed|The specified Platform is wrongly formed.|指定的镜像操作系统发行版不合法。|
|400|OperationDenied|Not support creating system image from an encrypted snapshot/disk.|被加密的磁盘和快照不允许创建系统镜像。|
|400|InvalidParameter.AllEmpty|%s|您没有输入任何参数，请输入必要的参数。|
|403|IncorrectDiskStatus.Invalid|Device status is invalid, please restart instance and try again.|设备状态无效，请重启实例后再试。|
|403|OperationDenied.InvalidSnapshotCategory|%s|该快照类型不支持此操作。|
|403|QuotaExceed.Snapshot|The snapshot quota exceeds.|快照额度超过限制，若要存储新快照，在不影响业务的情况下，请您删除已有的老快照。|
|403|IncorrectDiskStatus.Transferring|The specified device is transferring, you can retry after the process is finished.|指定磁盘正在迁移中，请在迁移完毕后重试。|
|403|IncorrectDiskStatus|The current disk status does not support this operation.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|403|InvalidSystemSnapshot.Missing|?s|无效的快照，请确认此快照是否存在。|
|403|IncorrectDiskStatus.CreatingSnapshot|A previous snapshot creation is in process.|当前磁盘有创建中的快照，请您等待创建完成再试。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|500|InternalError|The process of creating snapshot has failed due to some unknown error.|创建快照失败。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|400|InvalidDiskType.ValueNotSupported|The specified disk type is not supported.|指定的磁盘属性不支持。|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|与相同ClientToken的请求参数不符合。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

