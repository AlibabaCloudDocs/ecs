# CreateDisk

调用CreateDisk创建一块按量付费或包年包月数据盘。云盘类型包括普通云盘、高效云盘、SSD云盘和ESSD云盘。

## 接口说明

-   创建云盘需要通过实名认证。请前往会员信息中[实名认证](https://account.console.aliyun.com/#/auth/home)。
-   创建云盘会涉及到资源计费，建议您提前了解云服务器ECS的计费方式。更多信息，请参见[计费概述](~~25398~~)。
-   创建云盘时，默认在删除云盘时删除其自动快照，即`DeleteAutoSnapshot`取值为`true`，可以通过[ModifyDiskAttribute](~~25517~~)修改该参数。
-   创建ESSD云盘时，如果您不设置云盘性能等级，默认为PL1等级。您可以通过[ModifyDiskSpec](~~123780~~)修改云盘性能等级。
-   创建的云盘默认的计费方式为按量付费，即默认`Portable`属性为`true`。
-   创建云盘时支持开启多重挂载特性（`MultiAttach`）。建议您先了解该特性及使用限制，更多信息，请参见[ESSD云盘支持NVMe](~~256487~~)以及[使用多重挂载功能](~~262105~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateDisk&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDisk|系统规定参数。取值：CreateDisk |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|否|cn-hangzhou-g|在指定可用区内创建一块按量付费云盘。

 -   如果您不设置InstanceId，则ZoneId为必填参数。
-   您不能同时指定ZoneId和InstanceId。 |
|SnapshotId|String|否|s-bp67acfmxazb4p\*\*\*\*|创建云盘使用的快照。2013年7月15日及以前的快照不能用来创建云盘。

 `SnapshotId`参数和`Size`参数存在以下限制：

 -   如果`SnapshotId`参数对应的快照容量大于设置的`Size`参数值，实际创建的云盘大小为指定快照的大小。
-   如果`SnapshotId`参数对应的快照容量小于设置的`Size`参数值，实际创建的云盘大小为指定的`Size`参数值。 |
|DiskName|String|否|testDiskName|云盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。

 默认值：空 |
|Size|Integer|否|2000|容量大小。单位：GiB。您必须为该参数传入参数值。取值范围：

 -   cloud：5~2,000
-   cloud\_efficiency：20~32,768
-   cloud\_ssd：20~32,768
-   cloud\_essd：
    -   PL0：40~32,768
    -   PL1：20~32,768
    -   PL2：461~32,768
    -   PL3：1,261~32,768

 如果您指定了`SnapshotId`参数，`SnapshotId`参数和`Size`参数存在以下限制：

 -   如果`SnapshotId`参数对应的快照容量大于设置的`Size`参数值，实际创建的云盘大小为指定快照的大小。
-   如果`SnapshotId`参数对应的快照容量小于设置的`Size`参数值，实际创建的云盘大小为指定的`Size`参数值。 |
|DiskCategory|String|否|cloud\_ssd|数据盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘

 默认值：cloud |
|Description|String|否|testDescription|云盘描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |
|Encrypted|Boolean|否|false|是否加密云盘。默认值：false |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|InstanceId|String|否|i-bp18pnlg1ds9rky4\*\*\*\*|创建一块包年包月云盘，并自动挂载到指定的包年包月实例（InstanceId）上。

 -   设置实例ID后，会忽略您设置的ResourceGroupId、Tag.N.Key、Tag.N.Value、ClientToken和KMSKeyId参数。
-   您不能同时指定ZoneId和InstanceId。

 默认值：空，代表创建的是按量付费云盘，云盘所属地由RegionId和ZoneId确定。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|云盘所在的企业资源组ID。 |
|KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40826X|云盘使用的KMS密钥ID。 |
|PerformanceLevel|String|否|PL1|创建一块ESSD云盘时，设置云盘的性能等级。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万
-   PL1：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 默认值：PL1

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |
|StorageSetId|String|否|ss-bp67acfmxazb4p\*\*\*\*|存储集ID。 |
|StorageSetPartitionNumber|Integer|否|3|存储集分区数。 |
|DedicatedBlockStorageClusterId|String|否|dbsc-f8zfynww0vzuhg4w\*\*\*\*|专属块存储集群ID。如果您需要在指定的专属块存储集群中创建云盘，需要指定此参数。 |
|MultiAttach|String|否|Disabled|是否开启多重挂载特性。取值范围：

 -   Disabled: 不开启。
-   Enabled : 开启。目前仅ESSD云盘支持设置为`Enabled`。

 默认值：Disabled

 **说明：** 开启多重挂载特性的云盘只支持按量付费的计费方式。因此`MultiAttach=Enabled`时，不能同时设置`InstanceId`参数。您可以在创建云盘后调用[AttachDisk](~~25515~~)进行挂载，但需要注意开启多重挂载功能的云盘只能作为数据盘进行挂载。

 多重挂载功能正在邀测中，如需使用，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)。 |
|Tag.N.Key|String|否|TestKey|云盘的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|TestValue|云盘的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskId|String|d-bp131n0q38u3a4zi\*\*\*\*|云盘ID。 |
|OrderId|String|20413515388\*\*\*\*|生成的订单ID。

 **说明：** 仅在创建包年包月云盘时会返回订单ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateDisk
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-g
&SnapshotId=s-bp67acfmxazb4p****
&DiskName=testDiskName
&Size=2000
&DiskCategory=cloud_ssd
&Description=testDescription
&Encrypted=false
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateDiskResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <DiskId>d-bp131n0q38u3a4zi****</DiskId>
</CreateDiskResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "DiskId": "d-bp131n0q38u3a4zi****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSize.ValueNotSupported|The specified parameter Size is not valid.|指定的Size不合法。|
|400|InvalidDiskName.Malformed|The specified disk name is wrongly formed.|磁盘名称格式不正确。长度为2-128个字符，以英文字母或中文开头，可包含数字，点号（.），下划线（\_）或连字符（-）。 不能以http://和https://开头。|
|400|InvalidDescription.Malformed|The specified description is wrongly formed.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|MissingParameter|The input parameter either "SnapshotId" or "Size" should be specified.|参数SnapshotId或Size至少一项不得为空。|
|400|InvalidDiskCategory.NotSupported|The specified disk category is not support.|不支持的磁盘种类。|
|400|Account.Arrearage|Your account has an outstanding payment.|您的账号存在未支付的款项。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|指定的数据磁盘类型无效。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|RegionUnauthorized|%s|该地域未被授权。|
|400|Zone.NotOnSale|%s|该可用区暂时关闭了售卖。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|指定的数据盘容量无效。|
|400|OperationDenied|The specified Zone is not available or not authorized.|指定的可用区不可用或未授权。|
|400|InvalidDiskSize.NotSupported|The specified parameter size is not valid.|指定的磁盘容量无效。|
|400|InvalidDiskSizeOrCategory|The specified disk category or size is invalid.|指定的磁盘类别或大小无效。|
|400|InvalidParameter.EncryptedIllegal|%s|您输入的参数无效，请确认您的加密是否合法。|
|400|InvalidParameter.EncryptedNotSupported|%s|您输入的参数无效，暂时不支持您的加密操作。|
|400|EncryptedOption.Conflict|%s|参数不支持（加密盘）。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置参数KMSKeyId后，您必须开启加密属性。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|400|InvalidPerformanceLevel.Malformed|The specified parameter PerformanceLevel is not valid.|指定的参数PerformanceLevel无效。|
|400|InvalidInstance.NotFoundSystemDisk|The specified instance has no system disk.|指定的实例没有挂载系统盘。请确保指定的实例已挂载了系统盘。您可以调用DescribeInstances查询指定实例的信息。|
|403|InvalidDataDiskCategory.NotSupported|Specified disk category is not supported.|不支持指定的磁盘种类。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|InvalidSnapshot.NotReady|The specified snapshot creation is not completed yet.|指定快照未创建。|
|403|InvalidSnapshot.TooOld|This operation is forbidden because the specified snapshot is created before 2013-07-15.|指定磁盘的源快照创建于2013年7月15日（含）之前，不能重新初始化。|
|403|InvalidSnapshot.TooLarge|The capacity of snapshot exceeds 2000GB.|快照容量超过2000 GB。|
|403|OperationDenied|The specified snapshot is not allowed to create disk.|指定快照不支持创建磁盘。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|403|InvalidDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘种类未经授权。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|指定的快照为系统磁盘快照。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot.|指定的磁盘容量小于快照容量。|
|403|OperationDenied|The type of the disk does not support the operation.|此磁盘种类不支持指定的操作。|
|403|InvalidDataDiskCategory.NotSupported|%s|指定的数据磁盘类型无效。|
|403|InvalidDiskSize.NotSupported|disk size is not supported.|磁盘大小不合法。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidAccountStatus.SnapshotServiceUnavailable|Snapshot service has not been opened yet.|快照服务未开通，操作无法执行。|
|403|InvalidPayMethod|The specified pay method is not valid.|没有可用的付费方式。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|指定的云盘类型不支持当前操作。|
|403|InvalidDiskSize.NotSupported|The specified disk size is not supported.|暂不支持您设置的磁盘容量。|
|403|UserNotInTheWhiteList|The user is not in disk white list.|您不在磁盘白名单中，请加入白名单后重试。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您不在byok白名单中，请加入白名单后重试。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|我们检测到您的默认信用卡或借记卡存在安全风险。请通过电子邮件中的链接进行验证。|
|403|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|实例正在升级，请稍后重试。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|403|OperationDenied.SnapshotNotAllowed|The specified snapshot is not allowed to create disk.|指定的快照不支持创建磁盘。|
|403|LastTokenProcessing|The last token request is processing.|正在处理上一条令牌请求，请您稍后再试。|
|403|InvalidParameter.MultiAttach|The specified param MultiAttach is not valid.|MultiAttach参数的取值有误。|
|403|InvalidParameter.MultiAttachAndInstanceIdConflict|The parameter MultiAttach and InstanceId are conflict.|不支持同时设置MultiAttach参数和InstanceId参数。|
|403|InvalidParameter.DiskCategoryAndMultiAttachConflict|The specified disk category does not support multi attach set.|共享块存储不支持设置MultiAttach参数。|
|403|InvalidParameter.DiskCategoryAndMultiAttachNotMatch|The specified disk category does not support multi attach enabled.|要创建的云盘类型不支持开启多重挂载。|
|403|OperationDenied.ZoneNotSupportMultiAttachDisk|The specified zone does support multi attach disk.|指定的可用区不支持创建开启多重挂载特性的云盘。|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|指定的可用区ID不存在。|
|404|InvalidSnapshotId.NotFound|The specified SnapshotId does not exist.|指定的快照不存在，请您检查快照是否正确。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数KMSKeyId不存在。|
|404|InvalidInstanceId.NotFound|The InstanceId provided does not exist in our records.|指定的实例不存在，请您检查实例ID是否正确。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

