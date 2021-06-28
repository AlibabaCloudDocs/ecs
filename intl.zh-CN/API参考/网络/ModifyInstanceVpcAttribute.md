# ModifyInstanceVpcAttribute

调用ModifyInstanceVpcAttribute修改一台专有网络类型ECS实例的专有网络VPC、私网IP地址或虚拟交换机。

## 接口说明

调用接口时，ECS实例的状态必须是**已停止**（`Stopped`）。

-   当您使用该接口修改实例的私网IP地址或虚拟交换机时，请注意：
    -   新建的ECS实例必须经过重启才能调用该接口。
    -   成功修改一次后，ECS实例必须经过重启才能继续调用该接口。
-   当您使用该接口修改实例的专有网络VPC时，请注意：
    -   **实例：**
        -   不支持已关联负载均衡实例的ECS实例。
        -   实例的状态不能为已锁定、等待释放、已过期、过期回收中、欠费回收中。更多信息，请参见[实例生命周期介绍](~~25380~~)。
        -   实例不能在其它云服务中被使用。例如，实例不能在迁移中、不能已在更换VPC或实例内部署的数据库不能被DTS服务管理等。
    -   **网络：**
        -   不支持配置了EIP网卡可见模式或多EIP网卡可见模式的实例。
        -   不支持绑定高可用虚拟IP（HaVip）的实例。
        -   不支持交换机绑定了自定义路由表的实例。
        -   不支持开通了全球加速（GA）的实例。
        -   不支持绑定辅助网卡的实例。
        -   不支持已分配IPv6地址的实例。
        -   不支持主网卡有多IP的实例。
        -   传入的虚拟交换机必须属于目标VPC。
        -   修改前后虚拟交换机可用区必须一致。
        -   如果指定主网卡私网IP，则IP必须在虚拟交换机地址段内且可用。如果不指定则随机分配，且目标虚拟交换机的可用IP数充足。
        -   如果目标VPC开启了高级网络特性，则需要注意部分实例规格族不支持该特性。更多信息，请参见[不支持VPC高阶特性的实例规格族](~~163466~~)。
        -   目标VPC的所有者账号（资源所有者），不能将该目标VPC共享给其他账号（资源使用者）使用。
    -   **安全组（SecurityGroupId.N）：**
        -   安全组列表必须属于同一种类型。
        -   安全组的配额与实例能够加入安全组的限制有关。更多信息，请参见[使用限制](~~25412~~)。
        -   安全组所属的VPC必须与目标VPC一致。
        -   支持切换安全组的类型。

            当ECS实例跨类型切换安全组时，您需要充分了解两种安全组规则的配置区别，避免影响实例网络。更多信息，请参见[安全组概述](~~25387~~)。


## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceVpcAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceVpcAttribute|系统规定参数。取值：ModifyInstanceVpcAttribute |
|InstanceId|String|是|i-bp1iudwa5b1tqag1\*\*\*\*|实例ID。 |
|VSwitchId|String|是|vsw-bp1s5fnvk4gn3tw12\*\*\*\*|虚拟交换机ID。

 -   传入的ID为实例的当前虚拟交换机时，表明实例不变更虚拟交换机。
-   传入的ID为一台新的虚拟交换机，并且参数`VpcId`为空时，新旧虚拟交换机必须属于同一个可用区、同一个专有网络VPC。
-   当参数`VpcId`不为空时，该参数传入的虚拟交换机ID必须属于VpcId，并且和原虚拟交换机属于同一个可用区。 |
|PrivateIpAddress|String|否|172.17.\*\*.\*\*|新的私网IP地址。

 **说明：** `PrivateIpAddress`依赖于`VSwitchId`，指定的IP地址必须在虚拟交换机子网网段中。

 默认值：当不传该值时，从虚拟交换机子网网段中随机分配。 |
|VpcId|String|否|vpc-bp1vwnn14rqpyiczj\*\*\*\*|目标VPC ID。 |
|SecurityGroupId.N|RepeatList|否|sg-o6w9l8bc8dgmkw87\*\*\*\*|实例修改VPC后加入的安全组ID。当且仅当传入`VpcId`参数时，需要同时传入该参数。

 -   安全组类型必须一致。
-   指定实例修改后加入的安全组列表，可以是一个或者多个。参数中N的取值范围与实例能够加入安全组的限制有关。更多信息，请参见[使用限制](~~25412~~)。
-   专有网络类型ECS实例的安全组必须属于`VpcId`所在的VPC。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceVpcAttribute
&InstanceId=i-bp1iudwa5b1tqag1****
&VSwitchId=vsw-bp1s5fnvk4gn3tw12****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyInstanceAttributeResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|指定的私有IP不合法。|
|400|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicated.|指定的私网IP已经被使用，请您更换IP再重试。|
|400|IncorrectVSwitchStatus|The current status of virtual switch does not support this operation.|指定的虚拟交换机处于pending状态，无法删除。|
|404|InvalidVSwitchId.NotFound|Specified virtual switch does not exist.|指定的虚拟交换机ID不存在。|
|400|IncorrectInstanceStatus|The current status of instance does not support this operation.|目前实例状态不支持此类操作。|
|400|OperationDenied|Specified operation is denied as your instance is not in VPC.|该实例不是VPC实例。|
|400|InvalidVSwitchId.Mismatch|Specified instance and virtual switch are not in the same zone.|指定的实例和指定的虚拟交换机不属于同一个可用区。|
|400|InvalidPrivateIpAddress.Mismatch|Specified private IP address is not in the CIDR block of virtual switch.|指定的私网IP不在指定虚拟交换机的网段中。|
|404|InvalidVSwitchId.NotFound|Specified virtual switch is not found in current VPC.|当前VPC中不存在指定的虚拟交换机。|
|400|InvalidPrivateIp.Changing|Previous action is not finished yet.|实例修改私网IP未完成，不能再进行在修改。|
|404|NoSuchResource|The specified resource is not found.|指定的资源不存在。|
|400|InvalidPrivateIpAddress.Duplicated|error new ip is the same with old ip|新的IP地址必须不同于旧的IP地址。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|OperationDenied|%s|拒绝操作。|
|404|InvalidVSwitch.NotBelongToVpc|%s|指定的VSwitchId不属于指定的VPC。请检查参数值是否正确。|
|403|SecurityGroupInstanceLimitExceed|%s|该安全组内已有的实例数量已达到最大限制。|
|404|InvalidSecurityGroupId.NotFound|%s|指定的安全组ID不存在。|
|404|InvalidSecurityGroupType.NotSupportClassic|The specified SecurityGroupIds have classic group type.|指定的安全组的网络类型为经典网络。请检查SecurityGroupIds参数值是否正确。|
|404|InvalidSecurityGroupVpc.NotBelongToOneVpc|The specified SecurityGroupIds are belong to different vpc.|指定的安全组ID属于不同的VPC。请检查SecurityGroupIds参数值是否正确。您可以调用DescribeSecurityGroups查询指定安全组所属的VPC。|
|404|EnterpriseGroupLimited.MutliGroupType|The specified instance can not join multi SecurityGroup types.|指定的实例不能同时加入普通安全组和企业安全组。您可以调用DescribeSecurityGroups查询指定安全组的类型。|
|403|InvalidOperation.ResourceManagedByCloudProduct|%s|云产品托管的安全组不支持修改操作。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

