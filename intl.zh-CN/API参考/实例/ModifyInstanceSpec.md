# ModifyInstanceSpec

调用ModifyInstanceSpec调整一台按量付费ECS实例的实例规格和公网带宽大小。

## 接口描述

更多有关资源变配的Python SDK示例信息，请参见[查询可用的变配资源](~~109517~~)。

调用该接口时，您需要注意：

-   账号必须处于无欠费状态。
-   实例状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`）时才能调节公网带宽大小。
-   升级或者降低按量付费实例规格前，您可以通过[DescribeResourcesModification](~~66187~~)查询当前实例支持变配的实例规格。
-   实例状态必须为**已停止**（`Stopped`）时才能变更实例规格。
-   单次只能升级单项配置，即单次只能修改实例规格，或者只能调整公网带宽大小。
-   自2020年11月27日起，创建和变配ECS实例时带宽峰值受账户限速策略影响。如需更大带宽峰值，请提交工单。具体限速策略如下：
    -   单个地域下，所有按使用流量计费ECS实例的实际运行带宽峰值总和不大于5 Gbit/s。
    -   单个地域下，所有按固定带宽计费ECS实例的实际运行带宽峰值总和不大于50 Gbit/s。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceSpec&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceSpec|系统规定参数。取值：ModifyInstanceSpec |
|InstanceId|String|是|i-bp67acfmxazb4p\*\*\*\*|指定的实例ID。 |
|InstanceType|String|否|ecs.g6.large|实例的目标规格。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位为Mbit/s（Megabit per second）。取值范围：0~100

 **说明：** **按使用流量计费**模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用**按固定带宽计费**模式。 |
|InternetMaxBandwidthIn|Integer|否|10|公网入带宽最大值，单位为Mbit/s（Megabit per second）。取值范围：

 -   当所购公网出带宽小于等于10 Mbit/s时：1~10，默认为10。
-   当所购公网出带宽大于10 Mbit/s时：1~`InternetMaxBandwidthOut`的取值，默认为`InternetMaxBandwidthOut`的取值。

 **说明：** **按使用流量计费**模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用**按固定带宽计费**模式。 |
|Async|Boolean|否|false|是否提交异步请求。

 默认值：false |
|AllowMigrateAcrossZone|Boolean|否|false|是否支持跨集群升级实例规格。

 默认值：false

 当参数`AllowMigrateAcrossZone`取值为true时，一旦您根据返回信息升级了云服务器，请留意以下注意事项：

 经典网络类型实例：

 -   对于[已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，实例私网IP地址、磁盘设备名和软件授权码会发生变化。对于Linux实例，普通云盘（`cloud`）会被识别为**xvda**或者**xvdb**等，高效云盘（`cloud_efficiency`）和SSD云盘（`cloud_ssd`）会被识别为**vda**或者**vdb**等。
-   对于[正常售卖的实例规格族](~~25378~~)，实例的私网IP地址会发生变化。

 专有网络VPC类型实例：对于[已停售的实例规格](~~55263~~)，非I/O优化实例变配到I/O优化实例时，云服务器磁盘设备名和软件授权码会发生变化。Linux实例的普通云盘（`cloud`）会被识别为**xvda**或者**xvdb**等，高效云盘（`cloud_efficiency`）和SSD云盘（`cloud_ssd`）会被识别为**vda**或者**vdb**等。 |
|SystemDisk.Category|String|否|cloud\_ssd|更换系统盘类型。该参数只有在从[已停售的实例规格](~~55263~~)升级到[正常售卖的实例规格族](~~25378~~)，并将非I/O优化实例规格升级为I/O优化实例规格时有效。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceSpec
&InstanceId=i-bp67acfmxazb4p****
&InstanceType=ecs.g6.large
&InternetMaxBandwidthOut=10
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyInstanceSpecResponse>
     <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceSpecResponse>
```

`JSON` 格式

```
{
   "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|暂不支持指定的网络付费类型的实例，请确认相关参数是否正确。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的InternetMaxBandwidthOut参数不合法。|
|400|InvalidParameter.Mismatch|Too many parameters in one request.|请求中包含的参数过多。|
|403|CategoryViolation|The specified instance does not support this operation because of its disk category.|挂载有本地磁盘的实例不支持升降配。|
|403|InvalidStatus.ValueNotSupported|The current status of the resource does not support this operation.|当前资源的状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|403|OperationDenied|The specified instance is out of usage.|指定的实例库存不足。|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|该实例已经绑定EIP，不能进行临时升级。|
|404|MissingTemporary.StartTime|Temporary.StartTime is not specified.|未指定临时升级开始时间。|
|404|MissingTemporary.EndTime|Temporary.EndTime is not specified.|未指定临时升级结束时间。|
|400|InvalidTemporary.StartTime|The specifed Temporary.StartTime is not valid.|指定的临时升级开始时间无效。|
|400|InvalidTemporary.EndTime|The specifed Temporary.EndTime is not valid.|指定的临时升级结束时间无效。|
|403|LastTokenProcessing|The last token request is processing.|正在处理上一条令牌请求，请您稍后再试。|
|400|Downgrade.NotSupported|Downgrade operation is not supported.|不支持降配。|
|403|InstanceSpecModification.NotEffective|The specified instance has been reserved for making a spec modification and not taken effective in the current contract period.|指定的实例因规格调整被保留，在当前合同期内无法生效。|
|400|DependencyViolation.InstanceType|The current InstanceType cannot be changed to the specified InstanceType.|当前实例的规格不能变更到指定的规格。|
|403|InvalidInstanceType.ValueNotSupported|The specified zone does not offer the specified instancetype.|指定的区域不提供此类型的实例。|
|403|ImageNotSupportInstanceType|The specified image do not support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|400|Account.Arrearage|Your account has an outstanding payment.|您的账号存在未支付的款项。|
|400|InvalidParameter.Bandwidth|The specified parameter Bandwidth is not valid.|指定的Bandwidth不合法。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|InvalidParameter.AllowMigrateAcrossZone|The specified parameter CanMigrateAcrossZone is not valid.|指定的参数CanMigrateAcrossZone无效。|
|400|InvalidParam.SystemDiskCategory|The specified param SystemDisk.Category is not valid.|指定的系统盘类型参数无效。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|您当前的请求被流控，请5分钟后重试。|
|400|InvalidInstanceStatus.NotStopped|The specified Instance status is not stopped.|指定实例的状态不是已停止。|
|403|InstanceType.Offline|The specified InstanceType has been offline|您指定的实例规格已下线，请选择其它规格的实例。|
|400|InvalidAction|Specified action is not valid.|该操作无效。|
|400|IdempotenceParamNotMatch|There is a idempotence signature mismatch between this and last request.|该请求与上一个请求的ClientToken参数一致，但其它请求参数不一致。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|400|Price.PricePlanResultNotFound|The internetMaxBandwidthIn or internetMaxBandwidthOut provided is invalid.|提供的internetMaxBandwidthIn或internetMaxBandwidthOut无效。|
|403|InvalidParameter.NotMatch|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|已绑定EIP的实例不支持该操作，请先解绑此EIP。|
|400|InvalidAction.NotSupport|The ecs on dedicatedHost not support modify instanceType.|专用宿主机上的实例不支持变更实例规格。|
|400|InvalidMarketImageStatus.NotSupported|The status of specified market image does not support this operation.|指定的市场镜像的状态不支持该操作。|
|403|OperationDenied.NoStock|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|OperationDenied|%s|拒绝操作。|
|403|InvalidOperation.Ipv4CountExceeded|%s|IPv4数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6CountExceeded|%s|IPv6数量达到上限，导致该操作无效。|
|403|InvalidOperation.Ipv6NotSupport|%s|IPv6不支持当前操作。|
|403|InvalidOperation.InstanceWithEipNotSupport|The special instance with eip not support operate, please unassociate eip first.|已绑定EIP的实例不支持该操作，请优先解绑EIP。|
|403|SecurityRisk.3DVerification|We have detected a security risk with your default credit or debit card. Please proceed with verification via the link in your email.|我们检测到您的默认信用卡或借记卡存在安全风险。请通过电子邮件中的链接进行验证。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例计费方式不存在。|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您的全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您在当前地域选择的实例规格所要创建的台数超出系统限额，或者全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|400|InvalidOperation.VpcHasEnabledAdvancedNetworkFeature|The specified vpc has enabled advanced network feature.|该VPC开启了高阶特性，不能创建低规格的ECS。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

