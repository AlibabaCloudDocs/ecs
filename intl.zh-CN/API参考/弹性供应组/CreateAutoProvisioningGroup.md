# CreateAutoProvisioningGroup

调用CreateAutoProvisioningGroup接口创建一个弹性供应组。

## 接口说明

-   弹性供应是一个使用抢占式实例和按量付费实例快速部署实例集群的方案，支持一键部署跨计费方式、跨可用区、跨实例规格族的实例集群。更多信息，请参见[使用弹性供应组API批量创建ECS实例](~~200772~~)。
-   弹性供应以供应组为载体调度和维护计算资源，您可以通过弹性供应组稳定提供计算力，缓解抢占式实例的回收机制带来的不稳定因素。
-   弹性供应为免费功能，但是您需要为通过弹性供应组创建出的实例资源付费，详情请参见[抢占式实例计费](~~52088~~)和[按量付费](~~40653~~)。
-   当您同时指定启动模板（`LaunchTemplateId`）与启动配置信息（`LaunchConfiguration.*`）时，系统优先使用启动模板。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateAutoProvisioningGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAutoProvisioningGroup|系统规定参数。取值：CreateAutoProvisioningGroup |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID，您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|TotalTargetCapacity|String|是|60|弹性供应组的目标总容量。取值范围：正整数

 总容量必须大于等于`PayAsYouGoTargetCapacity`（指定的按量付费实例目标容量）和`SpotTargetCapacity`（指定的抢占式实例目标容量）取值之和。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|弹性供应组所在的企业资源组ID。 |
|AutoProvisioningGroupName|String|否|apg-test|弹性供应组的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|AutoProvisioningGroupType|String|否|maintain|弹性供应组的交付类型。取值范围：

 -   request：一次性异步交付。供应组仅在启动时异步交付实例集群，调度失败后不再重试。
-   instant：一次性同步交付。供应组仅在启动时同步创建实例，并在请求响应中返回创建成功的实例列表和创建失败的原因。
-   maintain：持续供应。供应组在启动时尝试交付实例集群，并监控实时容量，未达到目标容量则尝试继续创建ECS实例。

 默认值：maintain |
|SpotAllocationStrategy|String|否|diversified|创建抢占式实例的策略。取值范围：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   diversified：均衡可用区分布策略。在扩展启动模板指定的可用区内创建实例，均匀分布到各可用区。
-   capacity-optimized：容量优化分布策略。根据库存情况，选择最优的实例规格和可用区进行创建。

 默认值：lowest-price |
|SpotInstancePoolsToUseCount|Integer|否|2|在`SpotAllocationStrategy`为`lowest-price`时生效，表示弹性供应组选择价格最低的实例规格创建实例的数量。

 取值范围：低于`LaunchTemplateConfig.N`中N的取值 |
|PayAsYouGoAllocationStrategy|String|否|prioritized|创建按量付费实例的策略。取值范围：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   prioritized：优先级策略。按照`LaunchTemplateConfig.N.Priority`设定的优先级创建实例。

 默认值：lowest-price |
|ExcessCapacityTerminationPolicy|String|否|termination|弹性供应组实时容量超过目标容量并触发缩容时，是否释放缩容的实例。取值范围：

 -   termination：释放缩容的实例。
-   no-termination：只将缩容的实例移出弹性供应组。

 默认值：no-termination |
|ValidFrom|String|否|2019-04-01T15:10:20Z|弹性供应组的启动时间，和`ValidUntil`共同确定有效时段。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 默认值：立即生效 |
|ValidUntil|String|否|2019-06-01T15:10:20Z|弹性供应组的到期时间，和`ValidFrom`共同确定有效时段。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 默认值：2099-12-31T23:59:59Z |
|TerminateInstancesWithExpiration|Boolean|否|true|弹性供应组到期时，是否释放组内实例。取值范围：

 -   true：释放组内实例。
-   false：只将组内实例移出弹性供应组。

 默认值：false |
|TerminateInstances|Boolean|否|true|删除弹性供应组时，是否释放组内实例。取值范围：

 -   true：释放组内实例。
-   false：保留组内实例。

 默认值：false |
|MaxSpotPrice|Float|否|2|弹性供应组内抢占式实例的最高价格。

 **说明：** 同时设置了`MaxSpotPrice`和`LaunchTemplateConfig.N.MaxPrice`时，以最低值为准。 |
|PayAsYouGoTargetCapacity|String|否|30|弹性供应组内，按量付费实例的目标容量。取值范围：小于`TotalTargetCapacity`的参数取值 |
|SpotTargetCapacity|String|否|20|弹性供应组内，抢占式实例的目标容量。取值范围：小于`TotalTargetCapacity`的参数取值 |
|DefaultTargetCapacityType|String|否|Spot|`PayAsYouGoTargetCapacity`和`SpotTargetCapacity`之和小于`TotalTargetCapacity`时，指定差额容量的计费方式。取值范围：

 -   PayAsYouGo：按量付费实例
-   Spot：抢占式实例

 默认值：Spot |
|LaunchTemplateId|String|否|lt-bp1fgzds4bdogu03\*\*\*\*|弹性供应组关联的实例启动模板的ID，您可以调用[DescribeLaunchTemplates](~~73759~~)查询可用的实例启动模板。同时指定启动模板与启动配置信息（`LaunchConfiguration.*`）时，优先使用启动模板。 |
|LaunchTemplateVersion|String|否|1|弹性供应组关联的实例启动模板的版本，您可以调用[DescribeLaunchTemplateVersions](~~73761~~)查询可用的实例启动模板版本。

 默认值：启动模板的默认版本 |
|LaunchTemplateConfig.N.InstanceType|String|否|ecs.g5.large|扩展启动模板对应的实例规格，N的取值范围：1~20。取值范围：请参见[实例规格族](~~25378~~)。 |
|LaunchTemplateConfig.N.MaxPrice|Double|否|3|扩展启动模板中，抢占式实例的价格上限。

 **说明：** 设置了`LaunchTemplateConfig`后，`LaunchTemplateConfig.N.MaxPrice`为必选参数。 |
|LaunchTemplateConfig.N.VSwitchId|String|否|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|扩展启动模板中，ECS实例加入的虚拟交换机的ID。扩展模板中启动的ECS实例的可用区由虚拟交换机决定。

 **说明：** 设置了`LaunchTemplateConfig`后，`LaunchTemplateConfig.N.VSwitchId`为必选参数。 |
|LaunchTemplateConfig.N.WeightedCapacity|Double|否|2|扩展启动模板中，实例规格的权重。取值越高，单台实例满足计算力需求的能力越大，所需的实例数量越小。取值范围：大于0

 您可以根据指定实例规格的计算力和集群单节点最低计算力得出权重值。假设单节点最低计算力为8 vCPU、60GiB，则：

 -   8 vCPU、60GiB的实例规格权重可以设置为1
-   16 vCPU、120GiB的实例规格权重可以设置为2 |
|LaunchTemplateConfig.N.Priority|Integer|否|1|扩展启动模板的优先级，取值为0时优先级最高。取值范围：0 ~ +∞ |
|Description|String|否|testDescription|弹性供应组的描述信息。 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。ClientToken只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|LaunchConfiguration.ImageId|String|否|m-bp1g7004ksh0oeuc\*\*\*\*|镜像ID。启动实例时选择的镜像资源，您可以调用[DescribeImages](~~25534~~)查询可以使用的镜像资源。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg\*\*\*\*|实例所属的安全组ID。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.IoOptimized|String|否|optimized|是否为I/O优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 已停售的实例规格实例默认值是none，其他实例规格默认值是optimized。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.Size|Integer|否|20|第N个数据盘的容量大小，N的取值范围为1~16，单位为GiB。取值范围：

 -   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   cloud：5~2000

 **说明：** 该参数的取值必须大于等于参数`LaunchConfiguration.DataDisk.N.SnapshotId`指定的快照的大小。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.Category|String|否|cloud\_ssd|数据盘N的云盘类型。N的取值范围为1~16。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘。

 对于I/O优化实例，默认值为cloud\_efficiency。对于非I/O优化实例，默认值为cloud。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.PerformanceLevel|String|否|PL1|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。N的取值必须和`LaunchConfiguration.DataDisk.N.Category`中的N保持一致。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万
-   PL1（默认）：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.Device|String|否|/dev/vd1|数据盘的挂载点。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuh\*\*\*\*|创建数据盘N使用的快照。N的取值范围为1~16。

 指定该参数后，参数`LaunchConfiguration.DataDisk.N.Size`会被忽略，实际创建的云盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.DeleteWithInstance|Boolean|否|true|数据盘是否随实例释放。取值范围：

 -   true：数据盘随实例释放。
-   false：数据盘不随实例释放。

 默认值：true

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.Encrypted|Boolean|否|false|数据盘N是否加密。取值范围：

 -   true：加密
-   false：不加密

 默认值：false

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.KmsKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥ID。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、英文句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DataDisk.N.Description|String|否|DataDisk\_Description|数据盘的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.InternetChargeType|String|否|PayByTraffic|网络计费类型。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按使用流量计费

 **说明：** 按使用流量计费模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用按固定带宽计费模式。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.InternetMaxBandwidthIn|Integer|否|10|公网入带宽最大值，单位为Mbit/s。取值范围：

 -   当公网出带宽小于等于10Mbit/s时：1~10，默认为10。
-   当公网出带宽大于10Mbit/s时：1~`LaunchConfiguration.InternetMaxBandwidthOut`的取值，默认为`LaunchConfiguration.InternetMaxBandwidthOut`的取值。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位为Mbit/s。取值范围：0~100

 默认值：0

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.InstanceName|String|否|k8s-node-\[1,4\]-alibabacloud|实例名称。长度为2~128个字符，必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、英文句号（.）或者短划线（-）。默认值为实例的`InstanceId`。

 创建多台ECS实例时，您可以批量设置有序的实例名称。具体操作，请参见[批量设置有序的实例名称或主机名称](~~196048~~)。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.HostName|String|否|k8s-node-\[1,4\]-ecshost|实例主机名称。

 -   英文句号（.）和短划线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持英文句号（.），不能全是数字。允许大小写英文字母、数字和短划线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个英文句号（.），点之间为一段，每段允许大小写英文字母、数字和短划线（-）。

 创建多台ECS实例时，您可以批量设置有序的主机名。具体操作，请参见[批量设置有序的实例名称或主机名称](~~196048~~)。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.InstanceDescription|String|否|Instance\_Description|实例描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.KeyPairName|String|否|KeyPair\_Name|密钥对名称。

 -   Windows实例，忽略该参数。默认为空。
-   Linux实例的密码登录方式会被初始化成禁止。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.RamRoleName|String|否|RAM\_Name|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SecurityEnhancementStrategy|String|否|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.Tag.N.Key|String|否|TestKey|实例的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含`http://`或`https://`。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.Tag.N.Value|String|否|TestValue|实例的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以acs:开头，不能包含`http://`或者`https://`。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据。需要以Base64方式编码，原始数据最多为16 KB。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SystemDiskCategory|String|否|cloud\_ssd|系统盘的云盘种类。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘

 已停售的实例规格且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SystemDiskSize|Integer|否|40|系统盘大小。单位为GiB，取值范围：20~500。该参数的取值必须大于或者等于max\{20, LaunchConfiguration.ImageId对应的镜像大小\}。

 默认值：max\{40, 参数LaunchConfiguration.ImageId对应的镜像大小\}

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SystemDiskName|String|否|cloud\_ssdSystem|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、英文句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SystemDiskDescription|String|否|SystemDisk\_Description|系统盘的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.SystemDiskPerformanceLevel|String|否|PL0|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。取值范围：

 -   PL0（默认）：单盘最高随机读写IOPS 1万
-   PL1：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.PasswordInherit|Boolean|否|true|是否使用镜像预设的密码。取值范围：

 -   true：使用
-   false：不使用

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|实例所在的企业资源组ID。同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.CreditSpecification|String|否|Standard|修改突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无

 同时指定启动模板与启动配置信息时，优先使用启动模板。 |
|LaunchConfiguration.DeploymentSetId|String|否|ds-bp1frxuzdg87zh4p\*\*\*\*|部署集ID。 |
|SystemDiskConfig.N.DiskCategory|String|否|cloud\_ssd|实例系统盘类型。您可通过该参数指定多种候选磁盘类型，指定顺序作为各磁盘类型的优先级顺序，当某一种磁盘不可用时，自动更换磁盘类型。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘 |
|DataDiskConfig.N.DiskCategory|String|否|cloud\_efficiency|实例数据盘类型。您可通过该参数指定多种候选磁盘类型，指定顺序作为各磁盘类型的优先级顺序，当某一种磁盘不可用时，自动更换磁盘类型。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*|弹性供应组的ID。 |
|LaunchResults|Array of LaunchResult| |弹性供应组创建的实例组成的集合。该集合值仅当弹性供应组的交付类型为一次性同步交付（`instant`）时返回。 |
|LaunchResult| | | |
|ErrorCode|String|InvalidParameter|当实例创建失败时，返回的错误码。 |
|ErrorMsg|String|Specific parameter is not valid.|当实例创建失败时，返回的错误信息。 |
|InstanceIds|List|\["i-bp67acfmxazb4p\*\*\*\*"\]|成功创建的实例ID列表。 |
|InstanceType|String|ecs.g5.large|实例规格。 |
|SpotStrategy|String|NoSpot|按量实例的抢占策略。可能值：

 -   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格。 |
|ZoneId|String|cn-hangzhou-g|实例所在的可用区ID。 |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateAutoProvisioningGroup
&LaunchTemplateId=lt-bp1fgzds4bdogu03****
&RegionId=cn-hangzhou
&TotalTargetCapacity=60
&SpotInstancePoolsToUseCount=2
&ExcessCapacityTerminationPolicy=termination
&TerminateInstancesWithExpiration=true
&TerminateInstances=false
&PayAsYouGoTargetCapacity=30
&SpotTargetCapacity=20
&DefaultTargetCapacityType=Spot
&LaunchTemplateConfig.1.InstanceType=ecs.g5.large
&LaunchTemplateConfig.1.MaxPrice=3
&LaunchTemplateConfig.1.VSwitchId=vsw-sn5bsitu4lfzgc5o7****
&LaunchTemplateConfig.1.WeightedCapacity=2
&LaunchTemplateConfig.1.Priority=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateAutoProvisioningGroupResponse>
    <AutoProvisioningGroupId>apg-sn54avj8htgvtyh8****</AutoProvisioningGroupId>
    <RequestId>745CEC9F-0DD7-4451-9FE7-8B752F39****</RequestId>
</CreateAutoProvisioningGroupResponse>
```

`JSON`格式

```
{
    "AutoProvisioningGroupId": "apg-sn54avj8htgvtyh8****",
    "RequestId": "745CEC9F-0DD7-4451-9FE7-8B752F39****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidFleetExcessCapacityTerminationPolicy.ValueNotSupported|The specified parameter "ExcessCapacityTerminationPolicy" is not supported.|指定的ExcessCapacityTerminationPolicy值不合法。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

