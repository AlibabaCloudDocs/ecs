# ModifyDiskChargeType

调用ModifyDiskChargeType修改1台ECS实例上挂载的1块或最多16块云盘的计费方式。

## 接口说明

更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数AutoPay置为false，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。

使用该接口时，请注意：

-   包年包月云盘转换为按量付费云盘时，适用于包年包月实例上挂载的包年包月云盘。
-   按量付费云盘转换为包年包月云盘时，适用于包年包月实例上挂载的按量付费数据盘，或者按量付费实例上挂载的按量付费数据盘。
-   挂载的实例不能为欠费停机状态。
-   每块云盘更换计费方式的次数不能超过三次，即价格差退款不会超过三次。
-   更换计费方式前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   每块云盘成功修改计费方式一次，五分钟内不能再次修改。
-   开启多重挂载特性的云盘，仅支持按量付费的计费方式，不能转换为包年包月的计费方式。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyDiskChargeType&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyDiskChargeType|系统规定参数。取值：ModifyDiskChargeType |
|DiskIds|String|是|\[“d-bp67acfmxazb4ph\*\*\*\*”, “d-bp67acfmxazb4pi\*\*\*\*”, … “d-bp67acfmxazb4pj\*\*\*\*”\]|云盘ID列表，一个带有格式的JSON Array，最多支持16个ID，用半角逗号（,）隔开。 |
|InstanceId|String|是|i-bp1i778bq705cvx1\*\*\*\*|云盘挂载的实例ID。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|AutoPay|Boolean|否|true|是否自动支付。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。如果您的账户余额不足，会生成正常的未支付订单，此订单可登录ECS控制台支付。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|DiskChargeType|String|否|PostPaid|云盘计费方式。取值范围：

 -   PrePaid（默认）：按量付费数据盘转换为包年包月数据盘。
-   PostPaid：包年包月数据盘转换为按量付费数据盘。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|1234567890|生成的订单ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyDiskChargeType
&DiskIds=[“d-bp67acfmxazb4ph****”, “d-bp67acfmxazb4pi****”, … “d-bp67acfmxazb4pj****”]
&InstanceId=i-bp1i778bq705cvx1****
&RegionId=cn-hangzhou
&AutoPay=true
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&DiskChargeType=PostPaid
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyDiskChargeType>
        <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
        <Order>1234567890</Order>
</ModifyDiskChargeType>
```

`JSON`格式

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
    "Order": "1234567890"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType is not supported.|当前不支持您指定的实例规格，请选择其它实例规格。|
|400|MissingParameter.RegionId|RegionId should not be null.|参数RegionId不得为空。|
|400|MissingParameter.InstanceIdNotSupported|InstanceId should not be null.|参数InstanceId不能为空。|
|400|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InvalidInstanceId.Released|The specified Instance is not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidInstance.PurchaseNotFound|The specified Instance has no purchase.|指定的实例无法购买。|
|400|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|400|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|400|Idempotence.SignatureMismatch|There is a idempotence signature mismatch between this and last request.|作为和上一个幂等参数相同的请求，其他参数也必须完全相匹配。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not Supported.|您没有操作此实例规格的权限。|
|400|OrderCreationFailed|Create Order failed, please check your parameters and try it later.|创建订单失败，请检查您的参数，然后再试。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|您当前的请求被流控，请5分钟后重试。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|您的实例降配已超额度，无法进行此操作。|
|400|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|订单正在处理中，稍后重试。|
|400|InvalidAction.WithActiveElasticUpgrade|The instance has active Elastic Upgrade.|指定的实例为临时升级中（即调用ModifyPrepayInstanceSpec时设置了EndTime参数）的实例，暂不支持查询。|
|403|Forbidden|%s|您未被授权使用指定的资源。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidInstanceChargeType.NotFound|The chargeType of the instance does not support this operation.|该付费类型的实例不支持该操作。|
|403|InvalidOperation.MultiAttachDisk|Multi attach disk does not support this operation.|开启多重挂载特性的云盘不支持该操作。|
|404|InvalidRegionId.NotFound|The RegionId provided does not exist.|指定的地域不存在，请确认该参数是否正确。|
|404|PaymentMethodNotFound|No billing method has been registered on the account.|您未注册任何计费方式，请注册后重试。|
|404|InvalidRamRole.NotFound|The specified parameter "RAMRoleName" does not exist.|指定的RAM角色不存在。|
|404|InvalidDiskIds.NotFound|Some of the specified data disks do not exist.|参数DiskIds中的一些数据盘，不存在。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|
|404|InvalidDataDiskSize.ValueNotSupported|The specified parameter "Size" is not supported.|指定的数据盘大小不支持。|
|404|InvalidAction.NotSupported|The specified action is not supported.|不支持指定的API操作。|
|404|InvalidInstanceStatus.NotSupported|The status of the specified instance is invalid.|当前实例的状态不支持此操作。|
|404|InvalidInstanceId.NOT\_FOUND|The specified instance is not exist.|指定的实例不存在。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

