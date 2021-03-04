# ModifyInstanceDeployment

调用ModifyInstanceDeployment修改ECS实例的部署集，或迁移ECS实例至专有宿主机。支持在迁移ECS实例的同时变更实例规格。

## 接口说明

迁移ECS实例至专有宿主机，或在迁移实例同时变更ECS实例规格时，必须满足以下条件：

-   ECS实例必须处于**已停止**（Stopped）状态，迁移后实例自动重启。
-   只支持专有网络VPC类型的ECS实例。
-   ECS实例与专有宿主机必须属于同一账号、同一地域和可用区。
-   按量付费ECS实例可以迁移到包年包月专有宿主机上。包年包月ECS实例只能在包年包月专有宿主机之间迁移，且实例到期时间不能超过目标专有宿主机的到期时间。
-   将ECS实例从共享宿主机迁移至专有宿主机时，实例的计费方式只能是按量付费，不支持包年包月实例和抢占式实例。
-   ECS实例可以指定专有宿主机集群重新部署。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceDeployment&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceDeployment|系统规定参数。取值：ModifyInstanceDeployment |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*|实例ID。 |
|RegionId|String|是|cn-hangzhou|实例所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DeploymentSetId|String|否|ds-bp67acfmxazb4ph\*\*\*\*|部署集ID。

 将ECS实例加入一个部署集，或调整ECS实例的部署集时，该参数为必填参数。

 **说明：** 修改专有宿主机的相关参数（`Tenancy`、`Affinity`和`DedicatedHostId`）时，不可同时修改部署集。 |
|Force|Boolean|否|false|是否强制更换实例宿主机。取值范围：

 -   true：允许。允许重启**运行中**（Running）、**已停止**（Stopped）状态的ECS实例。已停止状态的实例不包括开启停机不收费功能的按量付费ECS实例。

**说明：** 如果您指定的ECS实例搭载了本地盘，则本地盘也会允许强制更换，这可能导致在更换宿主机时本地盘数据丢失，请谨慎操作。

-   false：不允许。只在当前宿主机上加入部署集。这可能导致更换部署集失败。

 默认值：false |
|DedicatedHostId|String|否|dh-bp67acfmxazb4ph\*\*\*\*|专有宿主机ID。调用[DescribeDedicatedHosts](~~134242~~)查看可以使用的专有宿主机。

 修改ECS实例宿主机（即将ECS实例从共享宿主机迁移至专有宿主机，或在不同专有宿主机间迁移ECS实例）时：

 -   若将实例迁移至指定专有宿主机上，必须设置该参数。
-   若将实例迁移至系统自动为您选择的专有宿主机上，必须将该参数设置为空，并将参数`Tenancy`设置为host。

 自动部署功能详情，请参见[专有宿主机功能特性](~~118938~~)。 |
|Tenancy|String|否|host|实例是否在专有宿主机上部署。取值：host，仅支持实例在专有宿主机上部署。 |
|Affinity|String|否|host|实例是否与专有宿主机关联。取值范围：

 -   host：关联。已开启停机不收费功能的实例停机后再次启动时，仍部署在原专有宿主机上。
-   default：不关联。已开启停机不收费功能的实例停机后再次启动时，若原专有宿主机资源不足，可迁移至自动部署资源池中的其它专有宿主机上。

 实例从共享宿主机迁移至专有宿主机。默认值：default |
|MigrationType|String|否|live|是否先停止实例，再迁移到目标专有宿主机。取值范围：

 -   reboot：先停止实例再迁移。
-   live：不停止实例，直接迁移。此时，您必须指定参数DedicatedHostId。该取值不支持在迁移ECS实例的同时变更实例规格。

 默认值：reboot |
|InstanceType|String|否|ecs.c6.large|ECS实例要变更的目标实例规格。调用[DescribeInstanceTypes](~~25620~~)接口可获取最新实例规格列表。

 修改ECS实例宿主机时，可同时变更ECS实例规格。目标实例规格必须与指定专有宿主机的规格相匹配，详情请参见[宿主机规格](~~68564~~)。

 -   变更实例规格时，必须指定专有宿主机ID，即设置参数`DedicatedHostId`的值。
-   使用自动部署功能迁移ECS实例时，不能变更实例规格。 |
|DedicatedHostClusterId|String|否|dc-bp67acfmxazb4ph\*\*\*\*|专有宿主机集群ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|04F0F334-1335-436C-A1D7-6C044FE73368|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceDeployment
&InstanceId=i-bp67acfmxazb4ph****
&RegionId=cn-hangzhou
&DedicatedHostId=dh-bp67acfmxazb4ph****
&Tenancy=host
&MigrationType=live
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyInstanceDeploymentResponse>
	  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceDeploymentResponse>
```

`JSON`格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机不存在。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|OperationDenied.UnstoppedInstance|Operation denied due to unstopped instance.|当前操作无效，请确认实例是否已停止。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|专有宿主机当前的状态不支持此操作。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例过期日期不能超过专有宿主机的过期日期。|
|404|InvalidInstanceNetworkType.NotSupport|The specified Instance network type not support.|当前实例的网络类型不支持此操作。|
|404|InvalidInstanceType.NotSupport|The Dedicated host not support the specified instance type.|当前宿主机不支持指定的实例规格。|
|403|IncorrectInstanceStatus|%s|当前实例的状态不支持此操作。|
|400|InvalidParam.Tenancy|The specified Tenancy is invalid.|您指定的参数Tenancy无效。|
|403|OperationDenied.NoStock|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|400|ChargeTypeViolation.PostPaidDedicatedHost|Prepaid instance onto postpaid dedicated host is not allowed.|包年包月的实例无法添加到按量付费的专有宿主机上。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

