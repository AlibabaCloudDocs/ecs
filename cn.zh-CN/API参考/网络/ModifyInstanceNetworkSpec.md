# ModifyInstanceNetworkSpec

调用ModifyInstanceNetworkSpec修改ECS实例的带宽配置。当实例现有网络规格不满足要求时，可以通过修改实例的带宽配置提高网络性能。

## 接口说明

调用该接口时，您需要注意：

-   自2020年11月27日起，创建和变配ECS实例时带宽峰值受账户限速策略影响。如需更大带宽峰值，请提交工单。具体限速策略如下：
    -   单个地域下，所有按使用流量计费ECS实例的实际运行带宽峰值总和不大于5 Gbit/s。
    -   单个地域下，所有按固定带宽计费ECS实例的实际运行带宽峰值总和不大于50 Gbit/s。
-   修改包年包月（PrePaid）实例的带宽配置时，公网出带宽（InternetMaxBandwidthOut）从0 Mbit/s升级到一个非零值时会自动分配一个公网IP。
-   修改按量付费（PostPaid）实例的带宽配置时，公网出带宽（InternetMaxBandwidthOut）从0 Mbit/s升级到一个非零值时不会自动分配公网IP。您需要调用[AllocatePublicIpAddress](~~25544~~)为实例分配公网IP。
-   对于经典网络（Classic）类型实例，当公网出带宽（InternetMaxBandwidthOut）从0 Mbit/s升级到一个非零值时，实例必须处于已停止（Stopped）状态。
-   升级带宽后，默认自动扣费。您需要确保支付方式余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数AutoPay置为false，此时会生成正常的未支付订单，您可以登录ECS管理控制台支付。
-   每台包年包月实例降低公网带宽的次数不能超过三次，即价格差退款不会超过三次。
-   修改带宽配置前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   单个实例每成功操作一次，五分钟内不能继续操作。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceNetworkSpec&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceNetworkSpec|系统规定参数。取值：ModifyInstanceNetworkSpec |
|InstanceId|String|是|i-bp67acfmxazb4\*\*\*\*|需要修改网络配置的实例ID。 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位：Mbit/s（Megabit per second）。取值范围：0~100 |
|InternetMaxBandwidthIn|Integer|否|10|设置公网入带宽最大值，单位：Mbit/s（Megabit per second）。取值范围：

 -   当所购公网出带宽小于等于10 Mbit/s时：1~10，默认为10。
-   当所购公网出带宽大于10 Mbit/s时：1~`InternetMaxBandwidthOut`的取值，默认为`InternetMaxBandwidthOut`的取值。 |
|NetworkChargeType|String|否|PayByTraffic|转换网络计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费。
-   PayByTraffic：按使用流量计费。

 **说明：** **按使用流量计费**模式下的出入带宽峰值都是带宽上限，不作为业务承诺指标。当出现资源争抢时，带宽峰值可能会受到限制。如果您的业务需要有带宽的保障，请使用**按固定带宽计费**模式。 |
|AllocatePublicIp|Boolean|否|false|是否分配公网IP地址。

 默认值：false |
|StartTime|String|否|2017-12-05T22:40Z|临时带宽升级开始时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC+0时间，格式为yyyy-MM-ddThh:mmZ。精确到**分钟**（mm）。 |
|EndTime|String|否|2017-12-06T22Z|临时带宽升级结束时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC+0时间，格式为yyyy-MM-ddThhZ。精确到**小时**（hh）。

 **说明：** 临时升级带宽的结束时间和开始时间的间隔必须大于或等于3小时。 |
|AutoPay|Boolean|否|true|是否自动支付。取值范围：

 -   true：变更带宽配置后，自动扣费。当您将参数Autopay置为true时，您需要确保账户余额充足，如果账户余额不足会生成异常订单，此订单暂时不支持通过ECS控制台支付，只能作废。
-   false：变更带宽配置后，只生成订单不扣费。如果您的支付方式余额不足，可以将参数Autopay置为false，即取消自动支付，此时调用该接口会生成正常的未支付订单，此订单可登录[ECS管理控制台](https://ecs.console.aliyun.com)支付。

 默认值：true |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|123457890|生成的订单ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceNetworkSpec
&InstanceId=i-bp67acfmxazb4p****
&InternetMaxBandwidthOut=10
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyInstanceNetworkSpecResponse>
        <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
        <OrderId>123457890</OrderId>
</ModifyInstanceNetworkSpecResponse>
```

`JSON` 格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "OrderId": "123457890"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidInternetMaxBandwidthIn.ValueNotSupported|The specified InternetMaxBandwidthIn is beyond the permitted range.|指定的公网入方向最大带宽超出允许值。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified InternetMaxBandwidthOut is beyond the permitted range.|指定的公网出方向最大带宽超出允许值。|
|403|IncorrectInstanceStatus|The current status of the instance does not support this operation.|当前实例状态不支持此操作。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|ChargeTypeViolation|The operation is not permitted due to billing method of the instance.|实例的计费方式不支持该操作。|
|403|OperationDenied|The operation is denied due to the instance is PrePaid.|包年包月的实例不支持此操作。|
|400|OperationDenied|Specified instance is in VPC.|指定实例存在于VPC。|
|400|InvalidParameter.Bandwidth|%s|指定的带宽无效，请检查参数是否正确。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|InvalidStartTime.ValueNotSupported|%s|结束时间不能早于开始时间。|
|400|Account.Arrearage|Your account has an outstanding payment.|您的账号存在未支付的款项。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is invalid.|指定的参数InternetChargeType无效。|
|400|DecreasedBandwidthNotAllowed|%s|降低带宽操作无效。|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|该实例已经绑定EIP，不能进行临时升级。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|您当前的请求被流控，请5分钟后重试。|
|400|InvalidAction|Specified action is not valid.|该操作无效。|
|400|IpAllocationError|Allocate public ip failed.|公网IP地址分配失败。|
|400|InvalidParam.AllocatePublicIp|The specified param AllocatePublicIp is invalid.|指定的AllocatePublicIp无效。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|您的实例降配已超额度，无法进行此操作。|
|400|InvalidBandwidth.ValueNotSupported|Instance upgrade bandwidth of temporary not allow less then existed.|临时宽带升级带宽不能低于已有带宽。|
|403|InvalidInstance.InstanceNotSupported|The special vpc instance with eip not need bandwidth.|VPC类型实例绑定EIP后不需要指定公网带宽。|
|400|InvalidInstanceStatus|The specified instance status does not support this action.|实例的当前状态不支持该操作。|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|当前实例的状态不支持此操作。|
|400|InvalidInstance.UnPaidOrder|Unpaid order exists in your account, please complete or cancel the payment in the expense center.|您的账号里有未支付的订单，请处理后重试。|
|400|OperationDenied|After downgrade, you cannot upgrade or downgrade your instances again in the remaining time of the current billing cycle.|降配后，您将无法在当前结算周期的剩余时间内再次升级或降级实例配置。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|暂不支持指定的网络计费方式，请确认相关参数是否正确。|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|订单正在处理中，稍后重试。|
|400|OperationDenied|The current user does not support this operation.|您使用的账号暂不支持此操作。|
|403|NAT\_PUBLIC\_IP\_BINDING\_FAILED|Binding nat public ip failed|公网IP绑定网关失败。|
|403|InvalidInstance.EipNotSupport|The specified instance with eip is not supported, please unassociate eip first.|已绑定EIP的实例不支持该操作，请先解绑此EIP。|
|403|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|指定的网络类型不合法。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

