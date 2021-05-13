# RunInstances

调用RunInstances创建一台或多台按量付费或者包年包月ECS实例。

## 接口说明

-   **准备工作**：
    -   成本估算：了解云服务器ECS的计费方式。更多详情，请参见[计费概述](~~25398~~)。
    -   产品选型：调用[DescribeInstanceTypes](~~25620~~)查看目标实例规格的性能数据，或者参见[选型配置](~~58291~~)了解如何选择实例规格。
    -   查询库存：调用[DescribeAvailableResource](~~66186~~)查看指定地域或者可用区内的资源供给情况。
    -   网络规划：您需要确保您已经有可用的安全组。更多详情，请参见[CreateSecurityGroup](~~25553~~)。创建专有网络VPC类型实例前，您需要预先在相应的阿里云地域[创建VPC](~~65430~~)。
-   **注意事项**：
    -   单次最多能创建100台实例。
    -   您可以指定参数`AutoReleaseTime`设置实例自动释放时间。
    -   创建成功后会返回实例ID列表，您可以通过[DescribeInstances](~~25506~~)查询新建实例状态。
    -   创建实例时，默认自动启动实例，直到实例状态变成运行中（`Running`）。
    -   自2020年11月27日起，创建和变配ECS实例时带宽峰值受账户限速策略影响。如需更大带宽峰值，请提交工单。具体限速策略：单个地域下，所有按使用流量计费ECS实例的实际运行带宽峰值总和不大于5 Gbit/s；所有按固定带宽计费ECS实例的实际运行带宽峰值总和不大于50 Gbit/s。
    -   与[CreateInstance](~~25499~~)相比，通过`RunInstances`创建的实例如果参数`InternetMaxBandwidthOut`的值大于0，则自动为实例分配公网IP。
    -   提交创建任务后，参数不合法或者库存不足的情况下会报错，具体的报错原因参见错误码。

**说明：** 如果创建实例时返回`QuotaExceed.ElasticQuota`错误，表示您在当前地域选择的实例规格所要创建的台数超出系统限额，或者全实例规格vCPU配额超出系统限额，您可以前往[ECS管理控制台](https://ecs.console.aliyun.com/?spm=a2c8b.12215451.favorites.decs.5e3a336aMGTtzy#/privileges/quota)或[配额中心](https://quotas.console.aliyun.com/products/ecs/quotas)申请提高限额。

-   **最佳实践**：
    -   单次大批量创建ECS实例（大于100台）遇到库存不足的场景；对实例规格或可用区等资源配置无指定要求，更关注如何快速创建实例的场景；对ECS实例数量无指定要求，更关注总算力vCPU个数等场景下，阿里云推荐您使用弹性供应组。您可以通过[CreateAutoProvisioningGroup](~~122738~~)创建弹性供应组，一键式的部署跨计费方式、跨可用区、跨实例规格族的实例集群。更多信息，请参见[使用弹性供应组API批量创建ECS实例](~~200772~~)。
    -   `RunInstances`可以执行批量创建任务，为便于管理与检索，建议您为每批次启动的实例指定标签（`Tag.N.Key`和`Tag.N.Value`），并且为主机名（`HostName`）和实例名称（`InstanceName`）添加有序后缀（`UniqueSuffix`）。
    -   实例启动模板能免除您每次创建实例时都需要填入大量配置参数，您可以创建实例启动模板（[CreateLaunchTemplate](~~74686~~)）后，在`RunInstances`请求中指定`LaunchTemplateId`和`LaunchTemplateVersion`使用启动模板。
    -   您可以在[ECS管理控制台](https://ecs.console.aliyun.com/)创建ECS实例时获取`RunInstances`的最佳实践建议。确认订单时，左侧**API 工作流**罗列出`RunInstances`能使用的关联API以及请求参数的值。右侧提供面向编程语言的SDK示例，目前支持**Java**和**Python**示例。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RunInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RunInstances|系统规定参数。取值：**RunInstances**。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ImageId|String|否|aliyun\_2\_1903\_x64\_20G\_alibase\_20200324.vhd|镜像ID，启动实例时选择的镜像资源。您可以通过[DescribeImages](~~25534~~)查询您可以使用的镜像资源。如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，也不通过指定`ImageFamily`选用镜像族系最新可用的自定义镜像，则`ImageId`为必选参数。 |
|ImageFamily|String|否|hangzhou-daily-update|镜像族系名称，通过设置该参数来获取当前镜像族系内最新可用的自定义镜像来创建实例。

 -   设置了参数`ImageId`，则不能设置该参数。
-   未设置参数`ImageId`，但指定的`LaunchTemplateId`或`LaunchTemplateName`对应的启动模板设置了`ImageId`，则不能设置该参数。
-   未设置`ImageId`，且指定的`LaunchTemplateId`或`LaunchTemplateName`对应的启动模板未设置`ImageId`，则可以设置该参数。
-   未设置`ImageId`，且未设置`LaunchTemplateId`、`LaunchTemplateName`参数，则可以设置该参数。 |
|InstanceType|String|否|ecs.g6.large|实例的资源规格。如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`InstanceType`为必选参数。

 -   产品选型：参见[实例规格族](~~25378~~)或调用[DescribeInstanceTypes](~~25620~~)查看目标实例规格的性能数据，或者参见[选型配置](~~58291~~)了解如何选择实例规格。
-   查询库存：调用[DescribeAvailableResource](~~66186~~)查看指定地域或者可用区内的资源供给情况。 |
|SecurityGroupId|String|否|sg-bp15ed6xe1yxeycg7\*\*\*\*|指定新创建实例所属于的安全组ID。同一个安全组内的实例之间可以互相访问，一个安全组能容纳的实例数量视安全组类型而定，具体请参见[使用限制](~~25412~~)的安全组章节。

 **说明：** SecurityGroupId决定了实例的网络类型，例如，如果指定安全组的网络类型为专有网络VPC，实例则为VPC类型，并同时需要指定参数VSwitchId。

 如果您不指定`LaunchTemplateId`或`LaunchTemplateName`以确定启动模板，`SecurityGroupId`为必选参数。 |
|VSwitchId|String|否|vsw-bp1s5fnvk4gn2tws0\*\*\*\*|虚拟交换机ID。如果您创建的是VPC类型ECS实例，必须指定虚拟交换机ID，且安全组和虚拟交换机在同一个专有网络VPC中。您可以调用[DescribeVSwitches](~~35748~~)查询已创建的交换机的相关信息。

 **说明：** 如果您指定了`VSwitchId`参数，则指定的`ZoneId`参数必须和交换机所在的可用区保持一致。您也可以不指定`ZoneId`参数，系统将自动选择指定的交换机所在的可用区。 |
|InstanceName|String|否|k8s-node-\[1,4\]-alibabacloud|实例名称。长度为2~128个字符，必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含中文、英文、数字、半角冒号（:）、下划线（\_）、半角句号（.）或者短划线（-）。默认值为实例的`InstanceId`。

 创建多台ECS实例时，您可以批量设置有序的实例名称。具体操作，请参见[批量设置有序的实例名称或主机名称](~~196048~~)。 |
|Description|String|否|Instance\_Description|实例的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|InternetMaxBandwidthIn|Integer|否|10|公网入带宽最大值，单位为Mbit/s。取值范围：

 -   当所购公网出带宽小于等于10Mbit/s时：1~10，默认为10。
-   当所购公网出带宽大于10Mbit/s时：1~`InternetMaxBandwidthOut`的取值，默认为`InternetMaxBandwidthOut`的取值。 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位为Mbit/s。取值范围：0~100

 默认值：0 |
|HostName|String|否|k8s-node-\[1,4\]-ecshost|实例主机名称。限制说明如下：

 -   半角句号（.）和短划线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持半角句号（.），不能全是数字。允许包含大小写英文字母、数字和短划线（-）。
-   其他类型实例（Linux等）：
    -   字符长度为2~64，支持多个半角句号（.），点之间为一段，每段允许包含大小写英文字母、数字和短划线（-）。
    -   支持通过占位符`${instance_id}`将实例ID写入`HostName`参数。例如：`HostName=k8s-${instance_id}`，并且创建的ECS实例ID为`i-123abc****`，则该实例的主机名为`k8s-i-123abc****`。

 创建多台ECS实例时，您可以：

 -   批量设置有序的主机名。具体操作，请参见[批量设置有序的实例名称或主机名称](~~196048~~)。
-   通过`HostNames.N`参数，为多台实例分别设置主机名。需要注意`HostName`参数和`HostNames.N`参数不能同时设置。 |
|UniqueSuffix|Boolean|否|true|当创建多台实例时，是否为`HostName`和`InstanceName`自动添加有序后缀。有序后缀从001开始递增，最大不能超过999。取值范围：

 -   true：添加
-   false：不添加

 默认值：false

 当`HostName`或`InstanceName`按照指定排序格式设置，未设置命名后缀`name_suffix`，即命名格式为`name_prefix[begin_number,bits]`时，`UniqueSuffix`不生效，名称仅按照指定顺序排序。

 更多信息，请参见[批量设置有序的实例名称或主机名称](~~196048~~)。 |
|Password|String|否|EcsV587!|实例的密码。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号中的三类字符。特殊符号可以是：

 ```

()`~!@#$%^&*-_+=|{}[]:;'<>,.?/

```

 您需要注意：

 -   如果传入`Password`参数，建议您使用HTTPS协议发送请求，避免密码泄露。
-   Windows实例不能以正斜线（/）为密码首字符。
-   部分操作系统的实例不支持配置密码，仅支持配置密钥对。例如：Others Linux、Fedora CoreOS。 |
|PasswordInherit|Boolean|否|false|是否使用镜像预设的密码。取值范围：

 -   true：使用
-   false：不使用

 **说明：** 使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。 |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区ID，您可以调用[DescribeZones](~~25610~~)获取可用区列表。

 **说明：** 如果您指定了`VSwitchId`参数，则指定的`ZoneId`参数必须和交换机所在的可用区保持一致。您也可以不指定`ZoneId`参数，系统将自动选择指定的交换机所在的可用区。

 默认值：系统自动选择。 |
|InternetChargeType|String|否|PayByTraffic|网络计费类型。取值范围：

 -   PayByBandwidth：按固定带宽计费
-   PayByTraffic（默认）：按使用流量计费

 **说明：** **按使用流量计费**模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用**按固定带宽计费**模式。 |
|SystemDisk.Size|String|否|40|系统盘大小，单位为GiB。取值范围：20~500

 该参数的取值必须大于或者等于max\{20, ImageSize\}。

 默认值：max\{40, 参数ImageId对应的镜像大小\} |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘

 已停售的实例规格且非I/O优化实例默认值为cloud，否则默认值为cloud\_efficiency。 |
|SystemDisk.DiskName|String|否|cloud\_ssdSystem|系统盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空 |
|SystemDisk.Description|String|否|SystemDisk\_Description|系统盘的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|SystemDisk.PerformanceLevel|String|否|PL0|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万
-   PL1（默认）：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |
|SystemDisk.AutoSnapshotPolicyId|String|否|sp-bp67acfmxazb4p\*\*\*\*|系统盘采用的自动快照策略ID。 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。[已停售的实例规格](~~55263~~)实例默认值是none，其他实例规格默认值是optimized。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化 |
|UserData|String|否|ZWNobyBoZWxsbyBlY3Mh|实例自定义数据。需要以Base64方式编码，原始数据最多为16 KB。 |
|KeyPairName|String|否|KeyPair\_Name|密钥对名称。

 -   Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。 |
|RamRoleName|String|否|RAM\_Name|实例RAM角色名称。您可以使用RAM API [ListRoles](~~28713~~)查询您已创建的实例RAM角色。 |
|Amount|Integer|否|3|指定创建ECS实例的数量。取值范围：1~100

 默认值：1 |
|MinAmount|Integer|否|2|指定ECS实例最小购买数量。取值范围：1~100

 -   当ECS库存数量小于最小购买数量，会创建失败。
-   当ECS库存数量大于等于最小购买数量，按照库存数量创建。 |
|AutoReleaseTime|String|否|2018-01-01T12:05:00Z|按量付费实例的自动释放时间。按照[ISO8601](~~25696~~)标准表示，使用UTC+0时间。格式为：yyyy-MM-ddTHH:mm:ssZ。

 -   如果秒（`ss`）取值不是`00`，则自动取为当前分钟（`mm`）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。 |
|SpotStrategy|String|否|NoSpot|按量实例的抢占策略。当参数`InstanceChargeType`取值为`PostPaid`时生效。取值范围：

 -   NoSpot（默认）：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格 |
|SpotDuration|Integer|否|1|抢占式实例的保留时长，单位为小时。取值范围：0~6

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   取值为0，则为无保护期模式。

 默认值：1 |
|SpotPriceLimit|Float|否|0.97|设置实例的每小时最高价格。支持最大3位小数，参数`SpotStrategy`取值为`SpotWithPriceLimit`时生效。 |
|SpotInterruptionBehavior|String|否|Terminate|抢占实例中断模式。目前仅支持Terminate（默认）直接释放实例。 |
|SecurityEnhancementStrategy|String|否|Active|是否开启安全加固。取值范围：

 -   Active：启用安全加固，只对公共镜像生效。
-   Deactive：不启用安全加固，对所有镜像类型生效。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|HpcClusterId|String|否|hpc-bp67acfmxazb4p\*\*\*\*|实例所属的EHPC集群ID。 |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会创建实例。检查项包括是否填写了必需参数、请求格式、业务限制和ECS库存。如果检查不通过，则返回对应错误。如果检查通过，则返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后直接创建实例。 |
|DedicatedHostId|String|否|dh-bp67acfmxazb4p\*\*\*\*|是否在专有宿主机上创建ECS实例。由于专有宿主机不支持创建抢占式实例，指定`DedicatedHostId`参数后，会自动忽略请求中的`SpotStrategy`和`SpotPriceLimit`设置。

 您可以通过[DescribeDedicatedHosts](~~134242~~)查询专有宿主机ID列表。 |
|LaunchTemplateId|String|否|lt-bp1apo0bbbkuy0rj\*\*\*\*|启动模板ID。更多详情，请调用[DescribeLaunchTemplates](~~73759~~)。

 使用启动模板创建实例时，您必须指定`LaunchTemplateId`或`LaunchTemplateName`确定启动模板。 |
|LaunchTemplateName|String|否|LaunchTemplate\_Name|启动模板名称。

 使用启动模板创建实例时，您必须指定`LaunchTemplateId`或`LaunchTemplateName`确定启动模板。 |
|LaunchTemplateVersion|Long|否|3|启动模板版本。如果您指定了`LaunchTemplateId`或`LaunchTemplateName`而不指定启动模板版本号，则采用默认版本。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|实例所在的企业资源组ID。 |
|Period|Integer|否|1|购买资源的时长，单位由`PeriodUnit`指定。当参数`InstanceChargeType`取值为`PrePaid`时才生效且为必选值。一旦指定了`DedicatedHostId`，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   PeriodUnit=Month时，Period取值：\{“1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”, ”48”, ”60”\}。 |
|PeriodUnit|String|否|Month|包年包月计费方式的时长单位。取值范围：

 -   Month（默认） |
|AutoRenew|Boolean|否|true|是否要自动续费。当参数`InstanceChargeType`取值`PrePaid`时才生效。取值范围：

 -   true：自动续费
-   false（默认）：不自动续费 |
|AutoRenewPeriod|Integer|否|1|单次自动续费的续费时长。取值范围：

 -   PeriodUnit=Month时：\{“1”, “2”, “3”, “6”, “12”, "24", "36", "48", "60"\}。

 默认值：1 |
|InstanceChargeType|String|否|PrePaid|实例的付费方式。取值范围：

 -   PrePaid：包年包月
-   PostPaid（默认）：按量付费

 选择包年包月时，您必须确认自己的账号支持信用支付，否则将返回`InvalidPayMethod`的错误提示。 |
|DeploymentSetId|String|否|ds-bp1brhwhoqinyjd6\*\*\*\*|部署集ID。 |
|PrivateIpAddress|String|否|10.1.\*\*.\*\*|实例私网IP地址。

 专有网络VPC类型ECS实例设置私网IP地址时，必须从虚拟交换机（`VSwitchId`）的空闲网段中选择。

 **说明：** 设置了`PrivateIpAddress`时，`Amount`参数取值只能为1。 |
|CreditSpecification|String|否|Standard|修改突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无 |
|Ipv6AddressCount|Integer|否|1|为主网卡指定随机生成的IPv6地址数量。

 **说明：** 您不能同时指定参数`Ipv6Addresses.N`和`Ipv6AddressCount`。 |
|NetworkInterfaceQueueNumber|Integer|否|8|主网卡队列数。

 -   不能超过实例规格允许的单块网卡最大队列数。
-   实例的所有网卡累加队列数不能超过实例规格允许的队列数总配额。实例规格的单块网卡最大队列数和总配额可以通过[DescribeInstanceTypes](~~25620~~)接口查询`MaximumQueueNumberPerEni`、`TotalEniQueueQuantity`字段。 |
|DeletionProtection|Boolean|否|false|实例释放保护属性，指定是否支持通过控制台或API（[DeleteInstance](~~25507~~)）释放实例。取值范围：

 -   true：开启实例释放保护
-   false（默认）：关闭实例释放保护

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。 |
|Affinity|String|否|default|专有宿主机实例是否与专有宿主机关联。取值范围：

 -   default：实例不与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，若原专有宿主机可用资源不足，则实例被放置在自动部署资源池的其它专有宿主机上。
-   host：实例与专有宿主机关联。已开启停机不收费功能的实例，停机后再次启动时，仍放置在原专有宿主机上。若原专有宿主机可用资源不足，则实例重启失败。

 默认值：default |
|Tenancy|String|否|default|是否在专有宿主机上创建实例。取值范围：

 -   default：创建非专有宿主机实例。
-   host：创建专有宿主机实例。若您不指定`DedicatedHostId`，则由阿里云自动选择专有宿主机放置实例。

 默认值：default |
|StorageSetId|String|否|ss-bp67acfmxazb4p\*\*\*\*|存储集ID。 |
|StorageSetPartitionNumber|Integer|否|2|存储集中的最大分区数量。取值范围：大于等于2 |
|CpuOptions.Core|Integer|否|2|CPU核心数。该参数不支持自定义设置，只能采用默认值。 |
|CpuOptions.ThreadsPerCore|Integer|否|2|CPU线程数。ECS实例的vCPU数=`CpuOptions.Core`取值`CpuOptions.ThreadPerCore`取值。

 -   `CpuOptions.ThreadPerCore=1`表示关闭CPU超线程。
-   仅部分实例规格支持设置CPU线程数。 |
|CpuOptions.Numa|String|否|1|CPU Numa节点数。 |
|SecurityOptions.TrustedSystemMode|String|否|vTPM|可信系统模式。取值：vTPM

 目前，可信系统模式支持的实例规格族：g7、c7、r7以及七代安全增强型（g7t、c7t、r7t）。

 当您创建以上实例规格族的ECS实例时，需要设置该参数。具体说明如下：

 -   如果您使用阿里云可信系统，请将该参数值设置为vTPM，在实例启动时即可通过阿里云可信系统完成可信校验。
-   如果您不使用阿里云可信系统，可以不设置该参数值。

 关于可信系统的更多信息，请参见[安全增强型实例可信功能概述](~~201394~~)。 |
|HttpEndpoint|String|否|enabled|是否启用实例元数据的访问通道。取值范围：

 -   enabled：启用
-   disabled：禁用

 默认值：enabled

 **说明：** 有关实例元数据的信息，请参见[实例元数据概述](~~49122~~)。 |
|HttpTokens|String|否|optional|访问实例元数据时是否强制使用加固模式（IMDSv2）。取值范围：

 -   optional：不强制使用。
-   required：强制使用。设置该取值后，普通模式无法访问实例元数据。

 默认值：optional

 **说明：** 有关访问实例元数据的模式，请参见[实例元数据访问模式](~~150575~~)。 |
|PrivatePoolOptions.MatchCriteria|String|否|Open|实例启动的私有池容量选项。弹性保障服务或容量预定服务在生效后会生成私有池容量，供实例启动时选择。取值范围：

 -   Open：开放模式。将自动匹配开放类型的私有池容量。如果没有符合条件的私有池容量，则使用公共池资源启动。该模式下无需设置`PrivatePoolOptions.Id`参数。
-   Target：指定模式。使用指定的私有池容量启动实例，如果该私有池容量不可用，则实例会启动失败。该模式下必须指定私有池ID，即`PrivatePoolOptions.Id`参数为必填项。
-   None：不使用模式。实例启动将不使用私有池容量。

 默认值：None

 以下任一场景，实例启动的私有池容量选项只能取值`None`或不传值。

 -   创建抢占式实例。
-   创建经典网络类型的ECS实例。
-   在专有宿主机DDH上创建ECS实例。 |
|PrivatePoolOptions.Id|String|否|eap-bp67acfmxazb4\*\*\*\*|私有池ID。即弹性保障服务ID或容量预定服务ID。 |
|SchedulerOptions.DedicatedHostClusterId|String|否|dc-bp12wlf6am0vz9v2\*\*\*\*|指定ECS实例所属的专有宿主机集群，系统会自动选择该专有宿主机集群中的一台专有宿主机部署ECS实例。

 **说明：** 仅在`Tenancy`设置为`host`时生效。

 在您同时指定了专有宿主机（`DedicatedHostId`）和专有宿主机集群（`SchedulerOptions.DedicatedHostClusterId`）时：

 -   如果专有宿主机属于专有宿主机集群，则优先将ECS实例部署在指定的专有宿主机上。
-   如果专有宿主机不属于专有宿主机集群，则ECS实例创建失败。

 您可以通过[DescribeDedicatedHostClusters](~~184145~~)查询专有宿主机集群ID列表。 |
|SecurityGroupIds.N|String|否|sg-bp15ed6xe1yxeycg7\*\*\*\*|将实例同时加入多个安全组。N的取值范围与实例能够加入安全组配额有关，更多详情，请参见[安全组限制](~~101348~~)。

 **说明：** 不支持同时指定SecurityGroupId和SecurityGroupIds.N。 |
|HostNames.N|String|否|ecs-host-01|创建多台实例时，为每台实例指定不同的主机名。限制说明如下：

 -   N的个数需要和`Amount`参数值保持一致。
-   不支持同时设置`HostName`参数和`HostNames.N`参数。
-   半角句号（.）和短划线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为2~15，不支持半角句号（.），不能全是数字。允许包含大小写英文字母、数字和短划线（-）。
-   其他类型实例（Linux等）：字符长度为2~64，支持多个半角句号（.），点之间为一段，每段允许包含大小写英文字母、数字和短划线（-）。 |
|DataDisk.N.PerformanceLevel|String|否|PL1|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。N的取值必须和`DataDisk.N.Category=cloud_essd`中的N保持一致。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万
-   PL1（默认）：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |
|DataDisk.N.AutoSnapshotPolicyId|String|否|sp-bp67acfmxazb4p\*\*\*\*|数据盘采用的自动快照策略ID。 |
|DataDisk.N.Encrypted|String|否|false|数据盘N是否加密。取值范围：

 -   true：加密
-   false：不加密

 默认值：false |
|DataDisk.N.Description|String|否|DataDisk\_Description|数据盘的描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|DataDisk.N.SnapshotId|String|否|s-bp17441ohwka0yuh\*\*\*\*|创建数据盘N使用的快照。N的取值范围为1~16。

 指定参数`DataDisk.N.SnapshotId`后，参数`DataDisk.N.Size`会被忽略，实际创建的云盘大小为指定的快照的大小。不能使用早于2013年7月15日（含）创建的快照，请求会报错被拒绝。 |
|DataDisk.N.Device|String|否|null|数据盘的挂载点。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。 |
|DataDisk.N.Size|Integer|否|2000|第n个数据盘的容量大小，N的取值范围为1~16，内存单位为GiB。取值范围：

 -   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   cloud：5~2000

 该参数的取值必须大于等于参数`SnapshotId`指定的快照的大小。 |
|DataDisk.N.DiskName|String|否|cloud\_ssdData|数据盘名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角句号（.）、半角冒号（:）、下划线（\_）或者短划线（-）。

 默认值：空 |
|DataDisk.N.Category|String|否|cloud\_ssd|数据盘N的云盘种类。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘。

 对于I/O优化实例，默认值为cloud\_efficiency。对于非I/O优化实例，默认值为cloud。 |
|DataDisk.N.DeleteWithInstance|Boolean|否|true|表示数据盘是否随实例释放。取值范围：

 -   true：数据盘随实例释放。
-   false：数据盘不随实例释放。

 默认值：true |
|DataDisk.N.KMSKeyId|String|否|0e478b7a-4262-4802-b8cb-00d3fb40\*\*\*\*|数据盘对应的KMS密钥ID。 |
|NetworkInterface.N.VSwitchId|String|否|vsw-bp67acfmxazb4p\*\*\*\*|辅助弹性网卡所属的虚拟交换机ID。N的取值：1

 默认值：ECS实例所属的虚拟交换机。 |
|NetworkInterface.N.NetworkInterfaceName|String|否|Network\_Name|辅助弹性网卡名称。N的取值：1 |
|NetworkInterface.N.Description|String|否|Network\_Description|辅助弹性网卡的描述。N的取值：1。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。 |
|NetworkInterface.N.SecurityGroupId|String|否|sg-bp67acfmxazb4p\*\*\*\*|辅助弹性网卡所属的安全组ID。N的取值：1

 默认值：实例所属的安全组。 |
|NetworkInterface.N.PrimaryIpAddress|String|否|172.16.\*\*.\*\*|添加一张辅助弹性网卡并设置主IP地址。N的取值范围为1。

 **说明：** 创建ECS实例时，您最多能添加一张辅助网卡。实例创建成功后，您可以调用[CreateNetworkInterface](~~58504~~)和[AttachNetworkInterface](~~58515~~)添加更多的辅助网卡。

 默认值：从网卡所属的交换机网段中随机选择一个IP地址。 |
|NetworkInterface.N.QueueNumber|Integer|否|8|辅助弹性网卡队列数。N的取值：1

 -   不能超过实例规格允许的单块网卡最大队列数。
-   实例的所有网卡累加队列数不能超过实例规格允许的队列数总配额。实例规格的单块网卡最大队列数和总配额可以通过[DescribeInstanceTypes](~~25620~~)接口查询`MaximumQueueNumberPerEni`、`TotalEniQueueQuantity`字段。 |
|NetworkInterface.N.SecurityGroupIds.N|String|否|sg-bp15ed6xe1yxeycg7\*\*\*\*|将辅助弹性网卡同时加入多个安全组。`SecurityGroupIds.N`中N的取值范围与弹性网卡实例能够加入安全组配额有关，更多详情，请参见[使用限制](~~25412~~)。

 **说明：** 不支持同时指定`NetworkInterface.N.SecurityGroupId`和`NetworkInterface.N.SecurityGroupIds.N`。 |
|Tag.N.Key|String|否|TestKey|实例、云盘和主网卡的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。 |
|Tag.N.Value|String|否|TestValue|实例、云盘和主网卡的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |
|Ipv6Address.N|String|否|Ipv6Address.1=2001:db8:1234:1a00::\*\*\*|为主网卡指定一个IPv6地址。目前，N的取值范围仅支持1。取值示例：`Ipv6Address.1=2001:db8:1234:1a00::***`。

 **说明：** 指定了参数`Ipv6Address.N`时，`Amount`参数取值只能为1，且不能指定`Ipv6AddressCount`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|OrderId|String|1234567890|订单ID。该参数只有创建包年包月ECS实例（请求参数`InstanceChargeType=PrePaid`）时有返回值。 |
|TradePrice|Float|0.165|订单成交价。 |
|InstanceIdSets|Array of String|\["i-bp67acfmxazb4pd2\*\*\*\*", "i-bp1i43l28m7u48p1\*\*\*\*", "i-bp12yqg7jdyxl11f\*\*\*\*"\]|实例ID（`InstanceIdSet`）列表。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=RunInstances
&RegionId=cn-hangzhou
&ImageId=aliyun_2_1903_x64_20G_alibase_20200324.vhd
&InstanceType=ecs.g6.large
&SecurityGroupId=sg-bp67acfmxazb4p****
&VSwitchId=vsw-bp1s5fnvk4gn2tws0****
&SystemDisk.AutoSnapshotPolicyId=sp-bp67acfmxazb4p****
&Amount=3
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<RunInstancesResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <InstanceIdSets>
        <InstanceIdSet>i-bp67acfmxazb4pd2****</InstanceIdSet>
        <InstanceIdSet>i-bp1i43l28m7u48p1****</InstanceIdSet>
        <InstanceIdSet>i-bp12yqg7jdyxl11f****</InstanceIdSet>
    </InstanceIdSets>
    <OrderId>1234567890</OrderId>
    <TradePrice>0.165</TradePrice>
</RunInstancesResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "RequestId" : "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "InstanceIdSets" : {
    "InstanceIdSet" : [ "i-bp67acfmxazb4pd2****", "i-bp1i43l28m7u48p1****", "i-bp12yqg7jdyxl11f****" ]
  },
  "OrderId" : "1234567890",
  "TradePrice" : "0.165"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|指定的实例规格不合法（超出可选范围）。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|暂不支持指定的网络付费类型的实例，请确认相关参数是否正确。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的InternetMaxBandwidthOut参数不合法。|
|400|InvalidHostName.Malformed|The specified parameter "HostName" is not valid.|指定的HostName格式不合法。|
|400|InvalidPassword.Malformed|The specified parameter "Password" is not valid.|指定的Password参数不合法。|
|400|InvalidPasswordParam.Mismatch|The input password should be null when passwdInherit is true.|启用PasswdInherit后，用户名密码应该设置为空。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的SystemDisk.Category不合法。|
|400|InvalidDiskName.Malformed|The specified parameter "SyatemDisk.DiskName or DataDisk.n.DiskName" is not valid.|磁盘名称格式不正确。长度为2-128个字符，以英文字母或中文开头，可包含数字、英文句号（.）、下划线（\_）或连字符（-）。不能以http://和https://开头。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription" or "DataDisk.n.Description" is not valid.|参数SyatemDisk.DiskDescription或DataDisk.n.Description不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的DataDisk.n.Size超出允许范围，或者快照的容量超过指定磁盘类别的大小限制。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数DataDisk.n.Category不合法。|
|400|InvalidDataDevice.Malformed|The specified parameter "DataDisk.n.Device" is not valid.|指定的参数DataDisk.n.Device不合法。|
|400|InvalidNodeControllerId.Malformed|The specified parameter "NodeControllerId" is not valid.|指定的NodeControllerId不合法。|
|400|InvalidInnerIpAddress.Malformed|The specified parameter "InnerIpAddress" is not valid.|指定的DiskDeviceMapping.n.DiskImageSize超出最大限值。|
|400|InvalidInnerIpAddress.Unusable|The specified InnerIpAddress is already used or not found in usable ip range.|指定的InnerIpAddress不可用。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|ImageNotSupportCloudInit|The specified image does not support cloud-init.|指定的镜像不支持cloud-init。|
|400|InvalidSnapshotId.BasedSnapshotTooOld|The specified snapshot is created before 2013-07-15.|指定的快照创建于2013-07-15之前。|
|400|QuotaExceed.AfterpayInstance|Living afterpay instances quota exceeded.|活跃的按量付费实例数已达上限。|
|400|InvalidInstanceName.Malformed|The specified parameter "InstanceName" is not valid.|指定的实例名称格式不合法。长度为2-128个字符，以英文字母或中文开头，可包含数字，点号（.），下划线（\_）或连字符（-）。不能以http://和https://开头。|
|400|InvalidDiskDescription.Malformed|The specified parameter "SyatemDisk.DiskDescription or DataDisk.n.Description" is not valid.|指定的参数SystemDisk.DiskDescription或DataDisk.n.Description无效。|
|400|InvalidParameter.Conflict|The speicified region and cluster do not match.|指定的地域与指定的集群不匹配。|
|400|InvalidParameter.Mismatch|Specified security group and virtual switch are not in the same VPC.|指定的安全组与虚拟交换机不在同一专有网络中。|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetMaxBandwidthIn" or "InternetMaxBandwidthOut" conflict with instance network type.|网络类型不匹配。|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|实例的网络类型不支持指定的网络计费方式。|
|400|InvalidPrivateIpAddress|Specified private IP address is not in the CIDR block of virtual switch.|指定的私有IP地址不属于交换机的CIDR网段。|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|指定的私有IP不合法。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|400|QuotaExceeded.PrivateIpAddress|Don't have enough private IPs in this switch|虚拟交换机下的私有IP已经被使用完，请您使用其他的虚拟交换机。|
|400|QuotaExceeded|Living instances quota exceeded in this VPC.|活跃的实例已达上限。|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|指定的虚拟交换机处于pending状态，无法删除。|
|400|InvalidParameter.Mismatch|Specified virtual switch is not in the specified zone.|指定的虚拟交换机在指定的可用区里不存在。|
|400|ResourceNotAvailable|Resource you requested is not available in this region or zone.|指定的地域或可用区不支持专有网络VPC。|
|400|MissingParameter|The input parameter "VSwitchId" that is mandatory for processing this request is not supplied.|参数VSwitchId不得为空。|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|不支持的磁盘种类搭配。|
|400|MissingParamter|The specified parameter "Period" is not null.|参数Period不得为空。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|指定的磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|指定的系统盘类型无效。|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的DataDisk.n.Size超出允许范围，或者快照的容量超过了指定磁盘类别的大小限制。|
|400|InvalidInstanceType.ValueNotSupported|InternetMaxBandwidthOut should be set.|必须设置InternetMaxBandwidthOut参数。|
|400|InvalidInstanceType.ValueNotSupported|instancetype is not valid.|指定的InstanceType不合法。|
|400|InvalidClientToken.ValueNotSupported|clienttoken is not valid.|指定的ClientToken不合法。|
|400|InvalidIoOptimize.ValueNotSupported|The specified IoOptimize is not valid.|指定的I/O优化型实例无效。|
|400|InvalidSecurityGroupId.NotFound|The SecurityGroupId provided does not exist in our records.|指定的安全组在该用户账号下不存在，请您检查安全组ID是否正确。|
|400|InvalidHostName.Malformed|The specified parameter HostName is not valid.|指定的参数HostName不合法。|
|400|InvalidInternetMaxBandwidthOut.Malformed|The specified parameter internetMaxBandwidthOut is not valid.|指定的InternetMaxBandwidthOut参数不合法。|
|400|InvalidInternetMaxBandwidthIn.Malformed|The specified parameter internetMaxBandwidthIn is not valid.|指定的InternetMaxBandwidthIn参数不合法。|
|400|InvalidSnapshotId.NotFound|The specified parameter SnapshotId is not exist.|指定的快照不存在，请您检查快照是否正确。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的Tag.N.Key和Tag.N.Value不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidMinAmount.Malformed|The specified parameter MinAmount is not valid.|指定的MinAmount无效，请您检查该参数是否正确。|
|400|InvalidMaxAmount.Malformed|The specified parameter MaxAmount is not valid.|指定的MaxAmount不合法。|
|400|InvalidAutoReleaseTime.Malformed|The specified parameter AutoReleaseTime is not valid.|自动释放格式错误。请您按照ISO8601标准表示，并需要使用UTC时间，格式为：yyyy-MM-ddTHH:mm:ssZ。|
|400|InvalidPrivateIpAddress.Malformed|The specified parameter PrivateIpAddress is not valid.|指定的PrivateIpAddress不合法。|
|400|InvalidInnerIpAddress.Malformed|The specified parameter InnerIpAddress is not valid.|指定的InnerIpAddress参数不合法。|
|400|OperationDenied.NoVlan|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|指定的VlanId不合法，或已超出最大IP地址数限制。|
|400|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|资源标签已达上限。|
|400|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|400|InvalidUserData.SizeExceeded|The specified parameter "UserData" exceeds the size.|指定的UserData超过大小限制。|
|400|InvalidUserData.NotSupported|The specified parameter "UserData" only support the vpc and IoOptimized Instance.|指定的UserData仅支持VPC和I/O优化型实例。|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|400|InvalidSpotStrategy|The specified SpotStrategy is not valid.|指定的SpotStrategy参数无效。|
|400|InvalidSpotPriceLimit|The specified SpotPriceLimitis not valid.|指定的SpotPriceLimit参数有误。|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|指定的SpotDuration参数有误。|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|指定的SpotDuration参数值未获得授权。|
|400|InvalidSpotPrepaid|The specified Spot type is not support PrePay Instance.|指定的抢占式实例不支持包年包月的付费方式。|
|400|InvalidSpotAliUid|The specified UID is not authorized to use SPOT instance.|用户账户未获得创建抢占式实例的权限。|
|400|InvalidParameter.Bandwidth|%s|指定的带宽无效，请检查参数是否正确。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|指定的数据磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|当前操作不支持此系统磁盘类型。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|暂不支持指定的网络计费方式，请确认相关参数是否正确。|
|400|InvalidInstanceType.ValueNotSupported|%s|该操作暂不支持指定的实例类型。|
|400|RegionUnauthorized|%s|该地域未被授权。|
|400|Zone.NotOnSale|%s|该可用区暂时关闭了售卖。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|当前操作不支持设置的系统盘大小。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|指定的数据盘容量无效。|
|400|InvalidInstanceType.ValueNotSupported|The specified parameter "KeyPairName" only support IoOptimized Instance.|非I/O优化实例不支持设置密钥对。|
|400|InvalidInstanceType.ElasticNetworkInterfaceNotSupported|The specified instance type does not support Elastic Network Interface, you can not attach Elastic Network Interface to generation I instances.|指定的实例规格不支持弹性网卡。|
|400|InvalidParameter.EncryptedIllegal|%s|您输入的参数无效，请确认您的加密是否合法。|
|400|InvalidParameter.EncryptedNotSupported|%s|您输入的参数无效，暂时不支持您的加密操作。|
|400|InvalidSpotPriceLimit.LowerThanPublicPrice|The specified parameter "spotPriceLimit" can't be lower than current public price.|指定的参数sotPriceLimit不能低于目前的公开价格。|
|400|InvalidRelationResource.NotFound|The relation resource has been deleted.|关联的资源无效，该资源已经被删除。|
|400|IncorrectRecycleBinStatus|The operation is not permitted due to resource status.|当前资源的状态不支持此操作。|
|400|InvalidHpcClusterId.Unnecessary|The specified HpcClusterId is unnecessary|无需指定参数HpcClusterId。|
|400|InvalidVSwitchId.Necessary|The VSwitchId is necessary|参数VSwitchId不能为空。|
|400|InvalidHpcClusterId.Necessary|The HpcClusterId is necessary|参数HpcClusterId不能为空。|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found|指定的参数HpcClusterId不存在。|
|400|InvalidSecurityGroup.NotInDefaultVpc|%s|该安全组不在默认专有网络下，请确认安全组参数是否正确。|
|400|VpcNotFound|Vpc is not found according to the specified VSwitch or the vpc does not belong to you.|根据指定的Vswitch找不到对应的VPC，或该VPC不属于您。|
|400|InvalidSystemDiskSize.ImageNotSupportResize|The specified image does not support resize.|指定的镜像不支持扩容。|
|400|InvalidSpotInterruptionBehavior|%s|SpotInterruptionBehavior不支持。|
|400|InvalidDeploymentOnHost|%s|该实例不能部署在指定的部署集上。|
|400|InvalidInstanceChargeType.NotSupport|The Dedicated host not support the specified Instance charge type.|此专有宿主机不支持指定的付费类型的实例。|
|400|InvalidNetworkType.NotSupported|The classic networkType not support create ECS on dedicatedHost|专有宿主机不支持经典网络类型的实例。|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机不存在。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|专有宿主机当前的状态不支持此操作。|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|当前资源的状态不支持此操作。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed|包年包月的实例无法添加到按量付费的专有宿主机上。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例过期日期不能超过专有宿主机的过期日期。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorize.|您没有使用该实例规格的权限。|
|400|DedicatedHostType.Unmatched|The specified DedicatedHostType doesn?t match the instance type.|指定的专有宿主机类型与实例类型不匹配。|
|400|MissingParameter|The input parameter ImageId that is mandatory for processing this request is not supplied.|参数ImageId不能为空。|
|400|MissingParameter|The input parameter InstanceType that is mandatory for processing this request is not supplied.|参数InstanceType不能为空。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|包年包月的实例无法添加到按量付费的专有宿主机上。|
|400|InvalidParam.NetworkInterface|%s|您输入的参数无效，请检查输入的参数是否与接口对应。|
|400|InvalidParameter.CreditSpecification|The specified CreditSpecification is not supported in this region.|该地区不支持指定的信贷规范。|
|400|IncorrectVpcStatus|Current VPC status does not support this operation.|当前专有网络VPC的状态无法支持这个操作。|
|400|InvalidInstanceType.NotSupported|The specified instanceType is not supported by the deployment set.|当前部署集不支持您指定的实例规格，请选择其它实例规格。|
|400|InvalidVpcZone.NotSupported|The specified operation is not allowed in the zone to which your VPC belongs, please try in other zones.|您的VPC所属的区域中不允许进行指定的操作，请在其他区域中尝试。|
|400|IncorrectDefaultVpcStatus|The status of the default VPC is invalid.|默认VPC的状态无效。|
|400|InvalidAutoRenewPeriod.ValueNotSupported|The specified autoRenewPeriod is invalid.|指定的自动续费时长无效。|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|暂不支持该市场镜像的付费类型。|
|400|InvalidPeriodType.ValueNotSupported|The specified parameter PeriodType is invalid.|指定的单价无效。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|400|OperationDenied|The current user does not support this operation.|您使用的账号暂不支持此操作。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|您指定的参数Tenancy无效。|
|400|IncorrectVpcStatus|The current status of vpc does not support this operation.|当前VPC的状态不支持该操作。|
|400|InvalidParameter.EncryptedIllegal|The specified parameter Encrypted must be true when kmsKeyId is not empty.|设置参数KMSKeyId后，您必须开启加密属性。|
|400|IoOptimized.NotSupported|The specified instance must be IoOptimized instance when kmsKeyId is not empty.|设置KMSKeyId后，您必须使用I/O优化实例。|
|400|Duplicate.TagKey|The Tag.N.Key contain duplicate key.|标签中存在重复的键，请保持键的唯一性。|
|400|JoinedGroupLimitExceed|%s|指定资源所能加入的安全组数量达到上限。具体信息请参见错误信息%s占位符的实际返回结果。|
|400|InvalidHttpEndpoint.NotSupported|The specified HttpEndpoint not supported, you can use enabled\(default\) or disabled.|指定的参数HttpEndpoint值非法，请使用enabled（默认）或者disabled。|
|400|InvalidHttpTokens.NotSupported|The specified HttpTokens not supported, you can use optional\(default\) or required.|指定的参数HttpTokens值非法，请使用optional（默认）或者required。|
|400|InvalidHttpPutResponseHopLimit.NotSupported|The specified HttpPutResponseHopLimit not supported, more than 1 and less than 64 is reasonable.|指定的参数HttpPutResponseHopLimit值非法，取值范围必须大于等于1且小于等于64。|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|该VPC开启了高阶特性，不能创建低规格的ECS。|
|400|MissingParameter.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id should not be null.|指定的PrivatePoolOptions.Id参数不能为空。|
|400|Invalid.PrivatePoolOptionsId|The specified PrivatePoolOptions.Id is invalid.|指定的PrivatePoolOptions.Id参数无效。|
|400|Invalid.PrivatePoolOptionsId|The parameter PrivatePoolOptions.Id should be null when PrivatePoolOptions.MatchCriteria is not Target.|当PrivatePoolOptions.MatchCriteria参数取值不为Target时，PrivatePoolOptions.Id参数需要为空。|
|401|InvalidRamRole.NotEcsRole|The specified ram role is not authorized for ecs, please check your role policy.|指定的RAM角色无权使用ECS，请检查您的角色策略。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidParams.InstanceNameExceed|The uniqueSuffix takes three naming places, please shorten your InstanceName.|UniqueSuffix参数会占用三个命名空间，请缩短您的实例名称。|
|403|InvalidParams.HostnameExceed|The uniqueSuffix takes three naming places, please shorten your Hostname.|UniqueSuffix参数会占用三个命名空间，请缩短您的实例主机名。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘类别未经授权。|
|403|InvalidSnapshotId.NotReady|The specified snapshot has not completed yet.|指定的快照未完成。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|InvalidDevice.InUse|The specified device has been occupied.|指定的设备已经挂载了磁盘。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的市场镜像不可用，或者指定的用户定义镜像包含产品代码，因为它基于从市场订购的镜像，并且市场中包含完全相同的产品代码的镜像已被删除。|
|403|CategoryNotSupported|The specified zone does not offer the specified disk category.|指定的可用区没有提供该磁盘种类。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|403|SecurityGroupInstanceLimitExceed|Exceeding the allowed amount of instances of a security group.|安全组的实例数已达上限。|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|节点控制器暂不可用。|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|用户未被授权在指定的地域创建实例。|
|403|CategoryNotSupported|The specified Zone or cluster does not offer the specified disk category.|指定的可用区或集群没有提供该磁盘种类。|
|403|InvalidSnapshotId.NotDataDiskSnapshot|The specified snapshot is system disk snapshot.|指定的快照为系统磁盘快照。|
|403|CategoryNotSupported|The specified cluster does not offer the specified disk category.|指定的集群没有提供该磁盘种类。|
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|403|DeleteWithInstance.Conflict|The specified disk is not a portable disk and cannot be set to DeleteWithInstance attribute.|指定的磁盘不是可卸载磁盘，不支持随实例释放。|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持I/O优化型实例。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|指定的磁盘容量小于快照容量。|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|不支持的磁盘种类搭配。|
|403|IoOptimized.NotSupported|Vpc is not support IoOptimized instance.|该VPC不支持I/O优化型实例。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|指定的磁盘种类不支持该实例规格。|
|403|QuotaExceed.BuyImage|The specified image is from the image market?You have not bought it or your quota has been exceeded.|尚未从镜像市场购买指定的镜像，或已达上限。|
|403|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|指定的资源ID不支持标记。|
|403|OperationDenied|The specified RegionId does not support the creation of the network type ECS instance.|指定的地域ID不支持创建网络类型的ECS实例，请您确认该网络类型在此地域有库存。|
|403|OperationDenied.ImageNotValid|The specified Image is disabled or is deleted.|指定的镜像不存在。|
|403|OperationDenied.SnapshotNotValid|The specified snapshot is not allowed to create disk.|指定的快照不支持创建磁盘。|
|403|OperationDenied.SnapshotNotAllowed|The specified snapshot is not allowed to create disk.|指定的快照不支持创建磁盘。|
|403|OperationDenied.ZoneNotAllowed|The creation of Instance to the specified Zone is not allowed.|指定的可用区不支持创建实例。|
|403|OperationDenied.ZoneSystemCategoryNotMatch|The specified Zone or cluster does not offer the specified disk category or the speicified zone and cluster do not match.|指定的可用区或集群中不存在指定磁盘类别，或指定的可用区与集群不匹配。|
|403|OperationDenied.ResourceControl|The specified region is in resource control, please try later.|指定的区域处于资源控制中，请稍后再试。|
|403|OperationDenied.NoStock|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|403|OperationDenied.SnapshotParamsNotValid|The capacity of snapshot exceeds the size limit of the specified disk category or the specified category is not authorizied.|快照容量已达上限或用户未被授权指定类别。|
|403|OperationDenied.DiskTypeNotSupport|The type of the disk does not support the operation|制定操作不合法。|
|403|InvalidUserData.Forbidden|User not authorized to input the parameter "UserData", please apply for permission "UserData"|您没有操作UserData的权限，或者权限不足，请先申请权限。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|Zone.NotOnSale|The resource in the specified zone is no longer available for sale. Please try other regions and zones.|该可用区暂不售卖指定的资源。请尝试其他类型，或选择其他可用区和地域。|
|403|InvalidClusterId.NotFound|The specified clusterId does not exist.|指定的ClusterId不存在。|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|指定的资源在指定可用区中无货。请尝试其他类型，或选择其他可用区和地域。|
|403|InvalidInstanceType.ZoneNotSupported|The specified zone does not support this instancetype.|指定的可用区里不支持指定的InstanceType。|
|403|InstanceType.Offline|%s|实例规格因停售、供货不足等原因，不支持该操作。|
|403|DependencyViolation.WindowsInstance|The instance creating is window, cannot use ssh key pair to login.|指定的实例是Windows操作系统，此类实例不支持SSH密钥对登录。|
|403|InvalidUser.PassRoleForbidden|The RAM user does not have the privilege to pass a RAM role.|该RAM用户无权传递RAM角色。|
|403|Forbidden.RiskControl|This operation is forbidden by Aliyun RiskControl system.|该操作被风险控制系统禁止。|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|您的帐户尚未通过实名认证，请先实名认证后再操作。|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|不支持指定的InstanceType。|
|403|InvalidPayMethod|The specified pay method is not valid.|没有可用的付费方式。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|ImageNotSupportInstanceType|The specified image does not support the specified InstanceType.|指定的镜像不支持指定的实例规格。|
|403|OperationDenied.InvalidNetworkType|%s|该网络类型不支持此操作。|
|403|InvalidSpotInterruptionBehavior.ClassicNetworkNotSupport|The specified SpotInterruptionBehavior does not support Classic network Instance.|该操作不支持经典网络类型的实例。|
|403|InvalidSpotInterruptionBehavior.LocalDiskNotSupport|The specified SpotInterruptionBehavior does not support local disk instance.|该操作不支持有本地磁盘的实例。|
|403|OperationDenied.ImageNotValid|%s|当前镜像不支持此操作。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|InvalidParameter.NotMatch|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|OperationDenied.LocalDiskUnsupported|The configuration change is not allowed when the specified instance has local disks mounted.|实例挂载本地盘后不支持规格变配。|
|403|OperationDenied.InconsistentNetwork|The specified security group and vswitch are not in the same vpc.|指定的安全组和交换机没有在同一个VPC下。|
|403|OperationDenied|If the network segment of the vswitch is the same as that of its VPC. Therefore, the VPC cannot create other vswitchs across the region.|VPC与虚拟交换机的网段相同，无法在多可用区内创建其他交换机。|
|403|DefaultVswitch.Existed|The default vswitch for VPC already exists.|当前VPC中已经有了默认交换机。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|请求的资源在指定的可用区已售完，请您更换实例规格或者可用区重试，调用 DescribeZones 接口可以获得库存结果。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|挂载有本地磁盘的实例不支持升降配。|
|403|ResourcesNotInSameZone|The specified instance and dedicated host are not in the same zone.|指定的实例和专有宿主机不在同一个地域下。|
|403|InvalidDisk.SystemDiskSize|The specified SystemDiskSize beyond the permitted range.|系统盘大小超出最大允许值。|
|403|InsufficientBalance|Your account does not have enough balance.|账户余额不足，请先充值再操作。|
|403|MaxEniIpv6IpsCountExceeded|%s|该弹性网卡挂载的IPv6个数达到上限。|
|403|InvalidIp.IpRepeated|%s|指定的IP重复。|
|403|InvalidIp.IpAssigned|%s|指定的IP已被分配。|
|403|InvalidIp.Address|%s|指定的IPv6地址无效。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6NotSupport|%s|IPv6不支持当前操作。|
|403|InvalidVSwitch.Ipv6NotTurnOn|%s|您当前使用的交换机没有开启IPv6功能，请先开启此功能后重试。|
|403|InvalidParam.Amount|%s|指定的参数Amount无效。|
|403|InvalidVSwitchId.IpInvalid|%s|指定的私网IP无效。|
|403|Forbidden.RegionId|%s|当前地域暂时没有提供该服务。|
|403|QuotaExceed.DeploymentSetInstanceQuotaFull|instance quota in one deployment set exceeded.|当前部署集内的实例数量已满额。|
|403|InvalidRegion.NotSupport|The specified region does not support byok.|该地域不支持BYOK。|
|403|UserNotInTheWhiteList|The user is not in byok white list.|您不在byok白名单中，请加入白名单后重试。|
|403|InvalidParameter.KMSKeyId.CMKNotEnabled|The CMK needs to be enabled.|加密云盘设置了KMSKeyId后，CMK必须处于启用状态。您可以调用密钥管理服务的DescribeKey接口查询指定CMK的相关信息。|
|403|InvalidParameter.KMSKeyId.KMSUnauthorized|ECS service have no right to access your KMS.|ECS服务无权访问您的KMS。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|我们检测到您的默认信用卡或借记卡存在安全风险。请通过电子邮件中的链接进行验证。|
|403|QuotaExceed.Tags|%s|标签数超过可以配置的最大数量。|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您的全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您在当前地域选择的实例规格所要创建的台数超出系统限额，或者全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|
|403|InvalidParameter.InvalidEniQueueNumber|%s|弹性网卡队列数有误，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.MaxEniQueueNumberExceeded|%s|弹性网卡队列数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|
|403|InvalidOperation.ExceedInstanceTypeQueueNumber|%s|弹性网卡队列总数超过上限，具体信息请参见错误信息%s占位符的实际返回结果。|
|404|InvalidSecurityGroupId|The specified SecurityGroupId is invalid or does not exist.|指定的安全组ID无效或者不存在。|
|404|InvalidDataDiskSnapshotId.NotFound|The specified parameter "DataDisk.n.SnapshotId" is not valid.|指定的参数DataDisk.n.SnapshotId不合法。|
|404|InvalidClusterId.NotFound|The ClusterId provided does not exist in our records.|指定的ClusterId不存在。|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|指定的虚拟交换机ID不存在。|
|404|InvalidVSwitchId.NotFound|%s|指定的交换机不存在。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|指定的实例规格不支持I/O优化。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例计费方式不存在。|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为I/O优化实例，请您检查实例规格是否正确。|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|账户尚未注册支付方式。|
|404|HOSTNAME\_ILLEGAL|hostname is not valid.|指定的主机名不合法。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数SystemDisk.Size小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the min size.|指定的系统盘小于最低容量。|
|404|OperationDenied.CreatingConflict|Another Instance has been creating|不允许创建新的实例。|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|指定的可用区ID不存在。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|指定的RAM角色不存在。|
|404|InvalidLaunchTemplate.NotFound|%s|没有找到指定的启动模版，请检查参数是否正确。|
|404|InvalidLaunchTemplateVersion.NotFound|%s|没有找到该版本的启动模版，请检查参数是否正确。|
|404|InvalidVSwitchId.NotExist|%s|指定的交换机不存在。|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|指定的市场镜像不存在，请更改参数后重试。|
|404|DeploymentSet.NotFound|The specified deployment set does not exist.|指定的部署集不存在。|
|404|InvalidParameter.KMSKeyId.NotFound|The specified KMSKeyId does not exist.|指定的参数KMSKeyId不存在。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

