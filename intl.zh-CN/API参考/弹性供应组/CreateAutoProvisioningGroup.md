# CreateAutoProvisioningGroup

调用CreateAutoProvisioningGroup接口创建一个弹性供应组。

## 接口说明

弹性供应是一个使用抢占式实例和按量付费实例快速部署实例集群的方案，支持一键部署跨计费方式、跨可用区、跨实例规格族的实例集群。

弹性供应以供应组为载体调度和维护计算资源，您可以通过弹性供应组稳定提供计算力，缓解抢占式实例的回收机制带来的不稳定因素。

弹性供应为免费功能，但是您需要为通过弹性供应组创建出的实例资源付费，详情请参见[抢占式实例计费](~~52088~~)和[按量付费](~~40653~~)。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateAutoProvisioningGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateAutoProvisioningGroup|系统规定参数。取值：CreateAutoProvisioningGroup |
|LaunchTemplateId|String|是|lt-bp1fgzds4bdogu03\*\*\*\*|弹性供应组关联的实例启动模板的ID，您可以调用[DescribeLaunchTemplates](~~73759~~)查询可用的实例启动模板。 |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID，您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|TotalTargetCapacity|String|是|60|弹性供应组的目标总容量。取值范围：正整数

 总容量必须大于等于`PayAsYouGoTargetCapacity`（指定的按量付费实例目标容量）和`SpotTargetCapacity`（指定的抢占式实例目标容量）取值之和。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|弹性供应组所在的企业资源组ID。 |
|AutoProvisioningGroupName|String|否|apg-test|弹性供应组的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|AutoProvisioningGroupType|String|否|maintain|弹性供应组的交付类型。取值范围：

 -   request：一次性。供应组仅在启动时交付实例集群，调度失败后不再重试。
-   maintain：持续供应。供应组在启动时尝试交付实例集群，并监控实时容量，未达到目标容量则尝试继续创建ECS实例。

 默认值：maintain |
|SpotAllocationStrategy|String|否|diversified|创建抢占式实例的策略。取值范围：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   diversified：均衡可用区分布策略。在扩展启动模板指定的可用区内创建实例，均匀分布到各可用区。

 默认值：lowest-price |
|SpotInstanceInterruptionBehavior|String|否|terminate|停止了超额的抢占式实例后的下一步动作。取值范围：

 -   stop：保持停止状态
-   terminate：释放

 默认值：stop |
|SpotInstancePoolsToUseCount|Integer|否|2|在`SpotAllocationStrategy`为`lowest-price`时生效，表示弹性供应组选择价格最低的实例规格创建实例的数量。

 取值范围：低于`LaunchTemplateConfig.N`中N的取值 |
|PayAsYouGoAllocationStrategy|String|否|prioritized|创建按量付费实例的策略。取值范围：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   prioritized：优先级策略。按照`LaunchTemplateConfig.N.Priority`设定的优先级创建实例。

 默认值：lowest-price |
|ExcessCapacityTerminationPolicy|String|否|termination|弹性供应组超过目标总容量时，是否停止超额的抢占式实例。取值范围：

 -   no-termination：继续运行
-   termination：停止。停止后的下一步动作由`SpotInstanceInterruptionBehavior`指定

 默认值：no-termination |
|ValidFrom|String|否|2019-04-01T15:10:20Z|弹性供应组的启动时间，和`ValidUntil`共同确定有效时段。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 默认值：立即生效 |
|ValidUntil|String|否|2019-06-01T15:10:20Z|弹性供应组的到期时间，和`ValidFrom`共同确定有效时段。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 默认值：立即生效 |
|TerminateInstancesWithExpiration|Boolean|否|true|弹性供应组到期时，是否停止抢占式实例。取值范围：

 -   true：停止。停止后的下一步动作由`SpotInstanceInterruptionBehavior`指定
-   false：继续运行

 默认值：false |
|TerminateInstances|Boolean|否|true|删除弹性供应组时，是否释放组内实例。

 默认值：false |
|MaxSpotPrice|Float|否|2|弹性供应组内抢占式实例的最高价格。

 **说明：** 同时设置了`MaxSpotPrice`和`LaunchTemplateConfig.N.MaxPrice`时，以最低值为准。 |
|PayAsYouGoTargetCapacity|String|否|30|弹性供应组内，按量付费实例的目标容量。取值范围：小于`TotalTargetCapacity`的参数取值 |
|SpotTargetCapacity|String|否|20|弹性供应组内，抢占式实例的目标容量。取值范围：小于`TotalTargetCapacity`的参数取值 |
|DefaultTargetCapacityType|String|否|Spot|`PayAsYouGoTargetCapacity`和`SpotTargetCapacity`之和小于`TotalTargetCapacity`时，指定差额容量的计费方式。取值范围：

 -   PayAsYouGo：按量付费实例
-   Spot：抢占式实例

 默认值：Spot |
|LaunchTemplateVersion|String|否|1|弹性供应组关联的实例启动模板的版本，您可以调用[DescribeLaunchTemplateVersions](~~73761~~)查询可用的实例启动模板版本。

 默认值：启动模板的默认版本 |
|LaunchTemplateConfig.N.InstanceType|String|否|ecs.g5.large|扩展启动模板对应的实例规格，N的取值范围：1~20。取值范围：参见[实例规格族](~~25378~~) |
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

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*|弹性供应组的ID。 |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://ecs.aliyuncs.com/?Action=CreateAutoProvisioningGroup
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

`XML` 格式

```
<CreateAutoProvisioningGroupResponse>
    <CreateAutoProvisioningGroupId>apg-sn54avj8htgvtyh8****</CreateAutoProvisioningGroupId>
    <RequestId>745CEC9F-0DD7-4451-9FE7-8B752F39****</RequestId>
</CreateAutoProvisioningGroupResponse>
```

`JSON` 格式

```
{
    "CreateAutoProvisioningGroupId": "apg-sn54avj8htgvtyh8****",
    "RequestId": "745CEC9F-0DD7-4451-9FE7-8B752F39****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidFleetExcessCapacityTerminationPolicy.ValueNotSupported|The specified parameter "ExcessCapacityTerminationPolicy" is not supported.|指定的ExcessCapacityTerminationPolicy值不合法|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

