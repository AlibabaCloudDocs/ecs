# ModifyAutoProvisioningGroup

调用ModifyAutoProvisioningGroup接口修改一个弹性供应组的设置。

## 接口说明

修改弹性供应组前，请注意：

-   如果修改了供应组容量或者容量相关设置，供应组会在修改完成后执行一次调度任务。
-   如果供应组处于删除中状态，无法修改供应组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyAutoProvisioningGroup&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyAutoProvisioningGroup|系统规定参数。取值：ModifyAutoProvisioningGroup |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|AutoProvisioningGroupId|String|否|apg-bp67acfmxazb4ph\*\*\*\*|弹性供应组的ID。 |
|ExcessCapacityTerminationPolicy|String|否|no-termination|弹性供应组实时容量超过目标容量并触发缩容时，是否释放缩容的实例。取值范围：

 -   termination：释放缩容的实例。
-   no-termination：只将缩容的实例移出弹性供应组。 |
|DefaultTargetCapacityType|String|否|Spot|PayAsYouGoTargetCapacity和SpotTargetCapacity之和小于TotalTargetCapacity时，指定差额容量的计费方式。取值范围：

 -   PayAsYouGo：按量付费实例
-   Spot：抢占式实例 |
|TerminateInstancesWithExpiration|Boolean|否|false|弹性供应组到期时，是否释放组内实例。取值范围：

 -   true：释放组内实例。
-   false：只将组内实例移出弹性供应组。 |
|MaxSpotPrice|Float|否|0.5|弹性供应组内抢占式实例的最高价格。

 **说明：** 同时设置了MaxSpotPrice和LaunchTemplateConfig.N.MaxPrice时，以最低值为准。LaunchTemplateConfig.N.MaxPrice在创建弹性供应组时设置，且不可修改。 |
|TotalTargetCapacity|String|否|70|弹性供应组的目标总容量。取值范围：正整数

 总容量必须大于等于PayAsYouGoTargetCapacity（指定的按量付费实例目标容量）和SpotTargetCapacity（指定的抢占式实例目标容量）取值之和。 |
|PayAsYouGoTargetCapacity|String|否|30|弹性供应组内，按量付费实例的目标容量。取值范围：小于TotalTargetCapacity的参数取值。 |
|SpotTargetCapacity|String|否|30|弹性供应组内，抢占式实例的目标容量。取值范围：小于TotalTargetCapacity的参数取值。 |
|AutoProvisioningGroupName|String|否|apg-test|弹性供应组的名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|LaunchTemplateConfig.N.InstanceType|String|否|ecs.g5.large|扩展启动模板对应的实例规格，N的取值范围：1~20。取值范围：请参见[实例规格族](~~25378~~)。 |
|LaunchTemplateConfig.N.MaxPrice|Double|否|3|扩展启动模板中，抢占式实例的价格上限。 |
|LaunchTemplateConfig.N.VSwitchId|String|否|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|扩展启动模板中，ECS实例加入的虚拟交换机的ID。扩展模板中启动的ECS实例的可用区由虚拟交换机决定。 |
|LaunchTemplateConfig.N.WeightedCapacity|Double|否|2|扩展启动模板中，实例规格的权重。取值越高，单台实例满足计算力需求的能力越大，所需的实例数量越小。取值范围：大于0

 您可以根据指定实例规格的计算力和集群单节点最低计算力得出权重值。假设单节点最低计算力为8 vCPU、60 GiB，则：

 -   8 vCPU、60 GiB的实例规格权重可以设置为1
-   16 vCPU、120 GiB的实例规格权重可以设置为2 |
|LaunchTemplateConfig.N.Priority|Integer|否|1|扩展启动模板的优先级，取值为0时优先级最高。取值范围：大于0 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://ecs.aliyuncs.com/?Action=ModifyAutoProvisioningGroup
&RegionId=cn-hangzhou
&AutoProvisioningGroupId=apg-bp67acfmxazb4ph****
&TotalTargetCapacity=70
&MaxSpotPrice=0.5
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyAutoProvisioningGroupResponse>
    <RequestId>928E2273-5715-46B9-A730-238DC996****</RequestId>
</ModifyAutoProvisioningGroupResponse>
```

`JSON`格式

```
{
    "RequestId": "B48A12CD-1295-4A38-A8F0-0E92C937****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|您没有操作此资源的权限，或者此 API 不支持 RAM 角色。|
|400|OperationDenied|%s|拒绝操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

