# CreateLaunchTemplate

调用CreateLaunchTemplate创建一个ECS实例启动模板，简称模板。实例启动模板能免除您每次创建实例时都需要填入大量配置参数。

## 接口说明

实例启动模板中包含用于创建实例的相关配置，例如实例所属地域、镜像ID、实例规格、安全组ID和公网带宽等。如果模板中没有指定某一实例配置，您需要在创建实例时为实例指定该配置。

创建模板（`CreateLaunchTemplate`）后，模板的初始版本为1，您可以后续基于该版本创建多个模板版本（`CreateLaunchTemplateVersion`），版本号从1开始顺序递增。如果您在创建实例（[RunInstances](~~63440~~)）时不指定模板版本号，会采用默认版本。

调用该接口时，您需要注意：

-   您最多能在一个地域内创建30个实例启动模板，且每个模板最多能有30个版本。
-   实例启动模板的参数大多数为可选参数。创建模板时，阿里云不会验证模板中参数取值的存在性和有效性。只会在真正创建实例时校验参数取值的有效性。
-   如果实例启动模板中设置了某一配置，创建实例（[RunInstances](~~63440~~)）时就无法过滤掉该配置。例如，如果模板设置了`HostName=LocalHost`，`RunInstances`中`HostName`取值为空时，实例的主机名依然是`LocalHost`。如果您想覆盖`HostName=LocalHost`这一配置，可以在`RunInstances`中取`HostName=MyHost`或其他参数值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateLaunchTemplate&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateLaunchTemplate|系统规定参数。取值：CreateLaunchTemplate |
|LaunchTemplateName|String|是|testLaunchTemplateName|实例启动模板名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|TemplateTag.N.Key|String|否|TestKey|启动模板的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|TemplateTag.N.Value|String|否|TestValue|启动模板的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|VersionDescription|String|否|testVersionDescription|实例启动模板版本描述。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|ImageId|String|否|win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20170915.vhd|镜像ID，启动实例时选择的镜像资源。您可以通过[DescribeImages](~~25534~~)查询您可以使用的镜像资源。 |
|ImageOwnerAlias|String|否|system|镜像来源。取值范围：

 -   system：阿里云提供的公共镜像。
-   self：您创建的自定义镜像。
-   others：其他阿里云用户共享给您的镜像。
-   marketplace：[镜像市场](https://market.aliyun.com/)提供的镜像。您查询到的云市场镜像可以直接使用，无需提前订阅。您需要自行留意云市场镜像的收费详情。

 默认值：空，空表示返回取值为system、self以及others的结果。 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。

 **说明：** 使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。 |
|InstanceType|String|否|ecs.g5.large|实例的资源规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。 |
|SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg\*\*\*\*|指定新创建实例所属于的安全组ID。同一个安全组内的实例之间可以互相访问，一个安全组最多能管理1000台实例。

 **说明：** 不支持同时指定`SecurityGroupId`和`SecurityGroupIds.N`。 |
|VpcId|String|否|vpc-bp12433upq1y5scen\*\*\*\*|专有网络VPC ID。 |
|VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|创建VPC类型实例时需要指定虚拟交换机ID。 |
|InstanceName|String|否|testInstanceName|实例名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|testECSDescription|实例描述。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|InternetMaxBandwidthIn|Integer|否|10|公网入带宽最大值，单位为Mbit/s。取值范围：

 -   当所购公网出带宽小于等于10Mbit/s时：1~10，默认为10。
-   当所购公网出带宽大于10Mbit/s时：1~`InternetMaxBandwidthOut`的取值，默认为`InternetMaxBandwidthOut`的取值。 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位为Mbit/s。取值范围：0~100 |
|HostName|String|否|testHostName|云服务器的主机名。

 -   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。 |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区ID。 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。取值范围：

 -   cloud：普通云盘。
-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。您可以通过参数`SystemDisk.PerformanceLevel`设置云盘的性能等级。

 已停售的实例规格且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。 |
|SystemDisk.Size|Integer|否|40|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。 |
|SystemDisk.DiskName|String|否|testSystemDiskName|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|SystemDisk.Description|String|否|testSystemDiskDescription|系统盘描述。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|SystemDisk.PerformanceLevel|String|否|PL0|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。取值范围：

 -   PL0（默认）：单盘最高随机读写IOPS 1万。
-   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |
|SystemDisk.DeleteWithInstance|Boolean|否|true|系统盘是否随实例释放。取值范围：

 -   true：随实例释放
-   false：不随实例释放

 默认值：true |
|DataDisk.N.Size|Integer|否|2000|第n个数据盘的容量大小，n的取值范围为1~16，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768

 该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。 |
|DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuh\*\*\*\*|创建数据盘n使用的快照。n的取值范围为1~16。指定参数`DataDisk.N.SnapshotId`后，参数`DataDisk.N.Size`会被忽略，实际创建的云盘大小为指定的快照的大小。

 不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘n的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘

 I/O优化实例的默认值为cloud\_efficiency，非I/O优化实例的默认值为cloud。 |
|DataDisk.N.Encrypted|String|否|false|数据盘是否加密。 |
|DataDisk.N.DiskName|String|否|testDataDiskName|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|DataDisk.N.Description|String|否|testDataDiskDescription|数据盘描述。长度为2~256个英文或中文字符，不能以http://和https://开头。 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|表示数据盘是否随实例释放。取值范围：

 -   true：随实例释放
-   false：不随实例释放

 默认值：true |
|DataDisk.N.PerformanceLevel|String|否|PL1|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。N的取值必须和`DataDisk.N.Category=cloud_essd`中的N保持一致。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万。
-   PL1（默认）：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 100万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化 |
|NetworkInterface.N.PrimaryIpAddress|String|否|192.168.\*\*.\*\*|辅助弹性网卡的主私有IP地址。`NetworkInterface.N`的N取值不能大于1。 |
|NetworkInterface.N.VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|辅助弹性网卡所属的虚拟交换机ID。实例与弹性网卡必须在同一VPC的同一可用区中，可以分属于不同交换机。`NetworkInterface.N`的N取值不能大于1。 |
|NetworkInterface.N.SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg\*\*\*\*|辅助弹性网卡所属安全组的ID。辅助弹性网卡的安全组和实例的安全组必须在同一个VPC下。`NetworkInterface.N`的N取值不能大于1。

 **说明：** 不支持同时指定`NetworkInterface.N.SecurityGroupId`和`NetworkInterface.N.SecurityGroupIds.N`。 |
|NetworkInterface.N.NetworkInterfaceName|String|否|testEniName|辅助弹性网卡名称。`NetworkInterface.N`的N取值不能大于1。 |
|NetworkInterface.N.Description|String|否|testEniDescription|辅助弹性网卡描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。`NetworkInterface.N`的N取值不能大于1。 |
|NetworkInterface.N.SecurityGroupIds.N|RepeatList|否|sg-bp67acfmxazb4p\*\*\*\*|辅助弹性网卡加入的一个或多个安全组。安全组和辅助弹性网卡必须在同一个专有网络VPC中。`SecurityGroupIds.N`的N取值范围与辅助弹性网卡能够加入安全组配额有关。更多信息，请参见[使用限制](~~25412~~)。`NetworkInterface.N`的N取值不能大于1。

 **说明：** 不支持同时指定`NetworkInterface.N.SecurityGroupId`和`NetworkInterface.N.SecurityGroupIds.N`。 |
|InstanceChargeType|String|否|PrePaid|实例的计费方式。取值范围：

 -   PrePaid：包年包月。选择该类付费方式时，您必须确认自己的账号支持余额支付和信用支付，否则将返回`InvalidPayMethod`的错误提示。
-   PostPaid：按量付费。 |
|Period|Integer|否|1|购买资源的时长，单位为：月。当创建实例时，参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{“1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”, ”48”, ”60”\} |
|InternetChargeType|String|否|PayByTraffic|网络计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按使用流量计费

 **说明：** **按使用流量计费**模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用**按固定带宽计费**模式。 |
|EnableVmOsConfig|Boolean|否|false|是否启用实例操作系统配置。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。 |
|NetworkType|String|否|vpc|实例网络类型。取值范围：

 -   classic
-   vpc |
|UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据，需要以Base64方式编码，原始数据最多为16KB。 |
|KeyPairName|String|否|testKeyPairName|密钥对名称。

 -   Windows实例，忽略该参数。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。 |
|RamRoleName|String|否|testRamRoleName|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。 |
|AutoReleaseTime|String|否|2018-01-01T12:05:00Z|自动释放时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 -   如果秒（`ss`）取值不是`00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。 |
|SpotStrategy|String|否|NoSpot|按量实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：

 -   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|SpotPriceLimit|Float|否|0.97|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy`取值为`SpotWithPriceLimit`时生效。 |
|SpotDuration|Integer|否|1|抢占式实例的保留时长，单位为小时。取值范围：0~6

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   取值为0，则为无保护期模式。

 默认值：1 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|实例、块存储和弹性网卡所在的企业资源组ID。 |
|TemplateResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|启动模板所在的企业资源组ID。 |
|SecurityEnhancementStrategy|String|否|Deactive|是否为操作系统开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |
|Tag.N.Key|String|否|TestKey|实例、块存储和弹性网卡的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|Tag.N.Value|String|否|TestValue|实例、块存储和弹性网卡的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。 |
|SecurityGroupIds.N|RepeatList|否|sg-bp15ed6xe1yxeycg7\*\*\*\*|实例加入的一个或多个安全组。N的取值范围与实例能够加入安全组配额有关，更多详情，请参见[使用限制](~~25412~~)。

 **说明：** 不支持同时指定`SecurityGroupId`和`SecurityGroupIds.N`。 |
|PrivateIpAddress|String|否|10.1.\*\*.\*\*|实例私网IP地址。

 专有网络VPC类型ECS实例设置私网IP地址时，必须从虚拟交换机（`VSwitchId`）的空闲网段中选择。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|LaunchTemplateId|String|lt-m5eiaupmvm2op9d\*\*\*\*|实例启动模板ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplate
&LaunchTemplateName=testLaunchTemplateName
&RegionId=cn-hangzhou
&TemplateTag.1.Key=TestKey
&TemplateTag.1.Value=TestValue
&VersionDescription=testVersionDescription
&ImageId=win2008r2_64_ent_sp1_en-us_40G_alibase_20170915.vhd
&InstanceType=ecs.g5.large
&SecurityGroupId=sg-bp15ed6xe1yxeycg****
&VpcId=vpc-bp12433upq1y5scen****
&VSwitchId=vsw-bp1s5fnvk4gn2tws03****
&InstanceName=testInstanceName
&Description=testECSDescription
&InternetMaxBandwidthIn=10
&InternetMaxBandwidthOut=10
&HostName=testHostName
&ZoneId=cn-hangzhou-g
&SystemDisk.Category=cloud_ssd
&SystemDisk.Size=40
&SystemDisk.DiskName=testSystemDiskName
&SystemDisk.Description=TestDisk
&DataDisk.1.Size=2000
&DataDisk.1.SnapshotId=s-bp17441ohwka0yuh****
&DataDisk.1.Category=cloud_ssd
&DataDisk.1.Encrypted=false
&DataDisk.1.DiskName=testDataDiskName
&DataDisk.1.Description=testDataDiskDescription
&DataDisk.1.DeleteWithInstance=true
&IoOptimized=optimized
&NetworkInterface.1.PrimaryIpAddress=192.168.**.**
&NetworkInterface.1.VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&NetworkInterface.1.SecurityGroupId=sg-bp15ed6xe1yxeycg****
&NetworkInterface.1.NetworkInterfaceName=testEniName
&NetworkInterface.1.Description=testEniDescription
&PrivateIpAddress=10.1.**.**
&InstanceChargeType=PrePaid
&Period=1
&InternetChargeType=PayByTraffic
&NetworkType=vpc
&UserData=ZWNobyBoZWxsbyBlY3Mh
&RamRoleName=testRamRoleName
&AutoReleaseTime=2018-01-01T12:05:00Z
&SpotStrategy=NoSpot
&SpotPriceLimit=0.97
&SecurityEnhancementStrategy=Deactive
&Tag.1.Key=TestKey
&Tag.1.Value=TestValue
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CreateLaunchTemplateResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <LaunchTemplateId>lt-m5eiaupmvm2op9d****</LaunchTemplateId>
</CreateLaunchTemplateResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "LaunchTemplateId": "lt-m5eiaupmvm2op9d****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegion.NotExist|%s|指定的地域不存在，请确认参数是否正确。|
|403|LaunchTemplateLimitExceed|%s|超出启动模版限制。|
|403|LaunchTemplateName.Duplicated|%s|指定的启动模版名称已经存在。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidLaunchTemplateName.Malformed|The specified parameter LaunchTemplateName is not valid.|指定的参数LaunchTemplateName无效。|
|400|InvalidDescription.Malformed|The specified parameter "VersionDescription" is not valid.|指定的参数VersionDescription无效。|
|400|InvalidUserData.SizeExceeded|%s|您设置的数据大小超过了允许的最大值。|
|400|InvalidUserData.Base64FormatInvalid|%s|您设置的数据格式不正确，请选择规定的格式数据。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

