# DescribeAutoProvisioningGroups

调用DescribeAutoProvisioningGroups查询一个或多个弹性供应组。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroups&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAutoProvisioningGroups|系统规定参数。取值：DescribeAutoProvisioningGroups |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID。 |
|AutoProvisioningGroupId.N|RepeatList|否|apg-sn54avj8htgvtyh8\*\*\*\*|弹性供应组的ID。N的取值范围：1~20 |
|AutoProvisioningGroupName|String|否|testAutoProvisioningGroupName|弹性供应组的名称。 |
|PageSize|Integer|否|2|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |
|PageNumber|Integer|否|1|分页查询时设置的列表页码。

 起始值：1

 默认值：1 |
|AutoProvisioningGroupStatus.N|RepeatList|否|active|弹性供应组的状态，取值范围：

 -   submitted：完成创建，但弹性供应组尚未开始执行调度任务。
-   active：弹性供应组已开始执行调度任务。
-   deleted：弹性供应组已删除。
-   delete-running：弹性供应组删除中。
-   modifying：弹性供应组修改中。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroups|Array of AutoProvisioningGroup| |弹性供应组的详细信息。 |
|AutoProvisioningGroup| | | |
|AutoProvisioningGroupId|String|apg-sn54avj8htgvtyh8\*\*\*\*|弹性供应组ID。 |
|AutoProvisioningGroupName|String|EcsDocTest|弹性供应组的名称。 |
|AutoProvisioningGroupType|String|maintain|交付类型。可能值：

 -   request：一次性。供应组仅在启动时交付实例集群，调度失败后不再重试。
-   maintain：持续供应。供应组在启动时尝试交付实例集群，并监控实时容量，未达到目标容量则尝试继续创建ECS实例。 |
|CreationTime|String|2019-04-01T15:10:20Z|创建时间。 |
|ExcessCapacityTerminationPolicy|String|termination|弹性供应组实时容量超过目标容量并触发缩容时，是否释放缩容的实例。可能值：

 -   termination：释放缩容的实例。
-   no-termination：只将缩容的实例移出弹性供应组。 |
|LaunchTemplateConfigs|Array of LaunchTemplateConfig| |扩展启动模板的详细信息。 |
|LaunchTemplateConfig| | | |
|InstanceType|String|ecs.g5.large|扩展启动模板对应的实例规格。 |
|MaxPrice|Float|3|扩展启动模板对应实例规格的价格上限。 |
|Priority|Float|1|扩展启动模板对应的实例规格的优先级，取值为0时最高。 |
|VSwitchId|String|vsw-sn5bsitu4lfzgc5o7\*\*\*\*|扩展启动模板对应的虚拟交换机的ID。 |
|WeightedCapacity|Float|2|扩展启动模板对应的实例规格的权重。 |
|LaunchTemplateId|String|lt-bp1fgzds4bdogu03\*\*\*\*|关联的实例启动模板的ID。 |
|LaunchTemplateVersion|String|1|关联的实例启动模板的版本。 |
|MaxSpotPrice|Float|2|抢占式实例的最高价格。

 **说明：** 同时设置了MaxSpotPrice和LaunchTemplateConfig.N.MaxPrice时，以最低值为准。

 LaunchTemplateConfig.N.MaxPrice在创建弹性供应组时设置，且不可修改。 |
|PayAsYouGoOptions|Struct| |按量付费实例相关的策略。 |
|AllocationStrategy|String|prioritized|创建按量付费实例的策略。可能值：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   prioritized：优先级策略。按照LaunchTemplateConfig.N.Priority设定的优先级创建实例。

 **说明：** LaunchTemplateConfig.N.Priority在创建弹性供应组时设置，且不可修改。 |
|RegionId|String|cn-hangzhou|所在地域的ID。 |
|SpotOptions|Struct| |抢占式实例相关的策略。 |
|AllocationStrategy|String|diversified|创建抢占式实例的策略。可能值：

 -   lowest-price：成本优化策略。选择价格最低的实例规格。
-   diversified：均衡可用区分布策略。在扩展启动模板指定的可用区内创建实例，均匀分布到各可用区。 |
|InstanceInterruptionBehavior|String|stop|停止了超额的抢占式实例后的下一步动作。可能值：

 -   stop：保持停止状态。
-   terminate：释放。 |
|InstancePoolsToUseCount|Integer|2|弹性供应组选择价格最低的实例规格创建实例的数量。

 **说明：** 该参数在创建弹性供应组时被设置，且不可修改。 |
|State|String|fulfilled|弹性供应组整体调度的执行状态。可能值：

 -   fulfilled：已成功完成调度任务。
-   pending-fulfillment：创建实例中。
-   pending-termination：移除实例中。
-   error：调度时发生异常，未能交付实例集群。 |
|Status|String|submitted|弹性供应组的状态。可能值：

 -   submitted：完成创建，但弹性供应组尚未开始执行调度任务。
-   active：弹性供应组已开始执行调度任务。
-   deleted：弹性供应组已删除。
-   delete-running：弹性供应组删除中。
-   modifying：弹性供应组修改中。 |
|TargetCapacitySpecification|Struct| |弹性供应组的目标容量设置。 |
|DefaultTargetCapacityType|String|Spot|PayAsYouGoTargetCapacity和SpotTargetCapacity之和小于TotalTargetCapacity时，指定的差额容量的计费方式。可能值：

 -   PayAsYouGo：按量付费实例
-   Spot：抢占式实例 |
|PayAsYouGoTargetCapacity|Float|30|按量付费实例的目标容量。 |
|SpotTargetCapacity|Float|20|抢占式实例的目标容量。 |
|TotalTargetCapacity|Float|60|弹性供应组的目标总容量，由以下三个部分组成：

 -   PayAsYouGoTargetCapacity
-   SpotTargetCapacity
-   PayAsYouGoTargetCapacity和SpotTargetCapacity之外的差额容量 |
|TerminateInstances|Boolean|false|删除弹性供应组时，是否释放组内实例。可能值：

 -   true：释放组内实例。
-   false：保留组内实例。 |
|TerminateInstancesWithExpiration|Boolean|true|弹性供应组到期时，是否释放组内实例。可能值：

 -   true：释放组内实例。
-   false：只将组内实例移出弹性供应组。 |
|ValidFrom|String|2019-04-01T15:10:20Z|弹性供应组的启动时间，和`ValidUntil`结合确定有效时段。 |
|ValidUntil|String|2019-06-01T15:10:20Z|弹性供应组的到期时间，和`ValidFrom`结合确定有效时段。 |
|PageNumber|Integer|1|页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|745CEC9F-0DD7-4451-9FE7-8B752F39\*\*\*\*|请求ID。 |
|TotalCount|Integer|10|查询到的弹性供应组的个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroups
&AutoProvisioningGroupId.1=apg-sn54avj8htgvtyh8****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeAutoProvisioningGroups>
    <PageNumber>1</PageNumber>
    <TotalCount>1</TotalCount>
    <PageSize>10</PageSize>
    <RequestId>85331AC9-82C0-4604-9A14-048865BE****</RequestId>
    <AutoProvisioningGroups>
        <AutoProvisioningGroup>
            <TerminateInstancesWithExpiration>false</TerminateInstancesWithExpiration>
            <TerminateInstances>false</TerminateInstances>
            <ValidFrom>2019-06-17T15:22Z</ValidFrom>
            <AutoProvisioningGroupType>maintain</AutoProvisioningGroupType>
            <PayAsYouGoOptions>
                <AllocationStrategy>lowest-price</AllocationStrategy>
            </PayAsYouGoOptions>
            <AutoProvisioningGroupName>test61****</AutoProvisioningGroupName>
            <CreationTime></CreationTime>
            <ExcessCapacityTerminationPolicy>no-termination</ExcessCapacityTerminationPolicy>
            <Status>active</Status>
            <MaxSpotPrice>5</MaxSpotPrice>
            <LaunchTemplateVersion>1</LaunchTemplateVersion>
            <ValidUntil>2100-01-01T07:59Z</ValidUntil>
            <TargetCapacitySpecification>
                <SpotTargetCapacity>180</SpotTargetCapacity>
                <TotalTargetCapacity>300</TotalTargetCapacity>
                <PayAsYouGoTargetCapacity>120</PayAsYouGoTargetCapacity>
                <DefaultTargetCapacityType>PayAsYouGo</DefaultTargetCapacityType>
            </TargetCapacitySpecification>
            <State>fulfilled</State>
            <LaunchTemplateId>lt-uf657o6auob6aivd****</LaunchTemplateId>
            <RegionId>cn-shanghai</RegionId>
            <AutoProvisioningGroupId>apg-uf6c7pl7b30t4m98****</AutoProvisioningGroupId>
            <SpotOptions>
                <InstancePoolsToUseCount>1</InstancePoolsToUseCount>
                <InstanceInterruptionBehavior>terminate</InstanceInterruptionBehavior>
                <AllocationStrategy>lowest-price</AllocationStrategy>
            </SpotOptions>
            <LaunchTemplateConfigs>
                <LaunchTemplateConfig>
                    <MaxPrice>3</MaxPrice>
                    <WeightedCapacity>1</WeightedCapacity>
                    <VSwitchId>vsw-uf6qbjwokzl67uqqf****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.c5.xlarge</InstanceType>
                </LaunchTemplateConfig>
                <LaunchTemplateConfig>
                    <MaxPrice>2</MaxPrice>
                    <WeightedCapacity>2</WeightedCapacity>
                    <VSwitchId>vsw-uf6n6iy1ib39eqvph****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.g5.large</InstanceType>
                </LaunchTemplateConfig>
                <LaunchTemplateConfig>
                    <MaxPrice>1</MaxPrice>
                    <WeightedCapacity>3</WeightedCapacity>
                    <VSwitchId>vsw-uf6gs8uerj5osels4****</VSwitchId>
                    <Priority>1</Priority>
                    <InstanceType>ecs.hfc5.large</InstanceType>
                </LaunchTemplateConfig>
            </LaunchTemplateConfigs>
        </AutoProvisioningGroup>
    </AutoProvisioningGroups>
</DescribeAutoProvisioningGroups>
```

`JSON`格式

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "85331AC9-82C0-4604-9A14-048865BE****",
    "AutoProvisioningGroups": {
        "AutoProvisioningGroup": {
            "TerminateInstancesWithExpiration": false,
            "TerminateInstances": false,
            "ValidFrom": "2019-06-17T15:22Z",
            "AutoProvisioningGroupType": "maintain",
            "PayAsYouGoOptions": {
                "AllocationStrategy": "lowest-price"
            },
            "AutoProvisioningGroupName": "test61****",
            "CreationTime": "",
            "ExcessCapacityTerminationPolicy": "no-termination",
            "Status": "active",
            "MaxSpotPrice": 5,
            "LaunchTemplateVersion": 1,
            "ValidUntil": "2100-01-01T07:59Z",
            "TargetCapacitySpecification": {
                "SpotTargetCapacity": 180,
                "TotalTargetCapacity": 300,
                "PayAsYouGoTargetCapacity": 120,
                "DefaultTargetCapacityType": "PayAsYouGo"
            },
            "State": "fulfilled",
            "LaunchTemplateId": "lt-uf657o6auob6aivd****",
            "RegionId": "cn-shanghai",
            "AutoProvisioningGroupId": "apg-uf6c7pl7b30t4m98****",
            "SpotOptions": {
                "InstancePoolsToUseCount": 1,
                "InstanceInterruptionBehavior": "terminate",
                "AllocationStrategy": "lowest-price"
            },
            "LaunchTemplateConfigs": {
                "LaunchTemplateConfig": [
                    {
                        "MaxPrice": 3,
                        "WeightedCapacity": 1,
                        "VSwitchId": "vsw-uf6qbjwokzl67uqqf****",
                        "Priority": 1,
                        "InstanceType": "ecs.c5.xlarge"
                    },
                    {
                        "MaxPrice": 2,
                        "WeightedCapacity": 2,
                        "VSwitchId": "vsw-uf6n6iy1ib39eqvph****",
                        "Priority": 1,
                        "InstanceType": "ecs.g5.large"
                    },
                    {
                        "MaxPrice": 1,
                        "WeightedCapacity": 3,
                        "VSwitchId": "vsw-uf6gs8uerj5osels4****",
                        "Priority": 1,
                        "InstanceType": "ecs.hfc5.large"
                    }
                ]
            }
        }
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

