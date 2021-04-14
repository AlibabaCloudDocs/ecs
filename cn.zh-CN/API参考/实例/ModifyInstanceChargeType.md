# ModifyInstanceChargeType

调用ModifyInstanceChargeType更换一台或者多台ECS实例的计费方式。支持在按量付费实例和包年包月实例间相互转换，同时可以将实例挂载的所有按量付费云盘转换为包年包月云盘。

## 接口说明

请确保在使用该接口前，您已充分了解[云服务器ECS](https://www.aliyun.com/price/product#/ecs/detail)的计费方式和产品定价。

调用该接口时，您需要注意：

-   目标实例的状态必须为**运行中**（`Running`）或者**已停止**（`Stopped`），并且无欠费的情况下才能修改计费方式。
-   更换计费方式后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数`AutoPay`置为`false`，此时会生成正常的未支付订单，您可以登录[ECS管理控制台](https://ecs.console.aliyun.com/)支付。
-   **包年包月转按量付费**：
    -   是否支持包年包月转按量付费功能，是根据您的云服务器使用情况而定的。
    -   包年包月实例转按量实例的时候，新计费方式将覆盖实例的整个生命周期。您会收到修改前后的实例计费的价格差退款，退还到您的原付款渠道中，已使用的代金券将不退回。
    -   **退款规则**：您在一个月内能自由操作的退款额度有限且不累计，消耗完退款额度后，只能等待次月转换计费方式。一次转换计费消耗的退款额度公式为**vCPU数\*（退款天数\*24±浮动小时数）**。
-   **按量付费转包年包月**：
    -   支持将实例挂载的所有按量付费数据盘同时转换为包年包月数据盘。
    -   如果按量付费实例已经设置了释放时间，则不能调用该接口。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceChargeType&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceChargeType|系统规定参数。取值：ModifyInstanceChargeType |
|InstanceIds|String|是|\["i-bp67acfmxazb4p\*\*\*\*","i-bp67acfmxazb4d\*\*\*\*"\]|实例ID。取值可以由多台实例ID组成一个JSON数组，最多支持20个ID，ID之间用半角逗号（,）隔开。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Period|Integer|否|1|包年包月续费时长。如果ECS实例的宿主机为专有宿主机DDH，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   `PeriodUnit=Week`时，`Period`取值：\{"1", "2", "3", "4"\}
-   `PeriodUnit=Month`时，`Period`取值：\{ "1", "2", "3", "4", "5", "6", "7", "8", "9", "12", "24", "36","48","60"\} |
|PeriodUnit|String|否|Month|续费时长的时间单位，即参数`Period`的单位。取值范围：

 -   Week
-   Month（默认） |
|IncludeDataDisks|Boolean|否|false|是否将实例挂载的所有按量付费数据盘一起转换为包年包月数据盘。

 默认值：false |
|DryRun|Boolean|否|false|是否只预检此次请求。取值范围：

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false（默认）：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。 |
|AutoPay|Boolean|否|false|是否自动支付。取值范围：

 -   true（默认）：自动支付。您需要确保账户余额充足，如果账户余额不足会生成异常订单，只能作废订单。
-   false：只生成订单不扣费。

 **说明：** 如果您的支付方式余额不足，可以将参数AutoPay置为false，此时会生成未支付订单，您可以登录ECS管理控制台自行支付。 |
|InstanceChargeType|String|否|PrePaid|实例需要修改的目标计费方式。取值范围：

 -   PrePaid（默认）：将按量付费实例转换为包年包月实例。
-   PostPaid：将包年包月实例转换为按量付费实例。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|IsDetailFee|Boolean|否|false|包年包月转换为按量计费时，是否返回订单费用详情。

 默认值：false |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|FeeOfInstances|Array of FeeOfInstance| |订单费用详情。 |
|FeeOfInstance| | | |
|Currency|String|CNY|账单费用货币单位。 |
|Fee|String|0|费用数值。 |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|实例ID。 |
|OrderId|String|20413515388\*\*\*\*|生成的订单ID。 |
|RequestId|String|B61C08E5-403A-46A2-96C1-F7B1216DB10C|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceChargeType
&RegionId=cn-hangzhou
&InstanceIds=["i-bp67acfmxazb4p****","i-bp67acfmxazb4d****"]
&Period=1
&PeriodUnit=Month
&AutoPay=false
&IncludeDataDisks=false
&ClientToken=123e4567-e89b-12d3-a456-426655440000
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ModifyInstanceChargeTypeResponse>
      <RequestId>B61C08E5-403A-46A2-96C1-F7B1216DB10C</RequestId>
      <OrderId>20413515388****</OrderId>
      <FeeOfInstances>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
            <FeeOfInstance>
                  <Fee>0</Fee>
                  <InstanceId>i-bp67acfmxazb4d****</InstanceId>
                  <Currency>CNY</Currency>
            </FeeOfInstance>
      </FeeOfInstances>
</ModifyInstanceChargeTypeResponse>
```

`JSON`格式

```
{
    "RequestId":"B61C08E5-403A-46A2-96C1-F7B1216DB10C",
    "OrderId":"20413515388****",
    "FeeOfInstances":
    {
        "FeeOfInstance":[
            {
                "Fee":"0",
                "InstanceId":"i-bp67acfmxazb4p****",
                "Currency":"CNY"
            },
            {
                "Fee":"0",
                "InstanceId":"i-bp67acfmxazb4d****",
                "Currency":"CNY"
            }
        ]
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.InstanceIds|The specified InstanceIds are invalid.|指定的实例无效。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidStatus.ValueNotSupported|%s|该资源当前的状态不支持此操作。|
|400|InvalidInstanceChargeType.ValueNotSupported|%s|暂不支持此付款类型，请核对相关信息后重试。|
|400|ExpiredInstance|The specified instance has expired.|指定的实例已过期。|
|403|InvalidInstance.TempBandwidthUpgrade|Cannot switch to Pay-As-You-Go during the period of temporary bandwidth upgrade.|实例在临时带宽升级期间不能转换为按量付费。|
|400|InstancesIdQuotaExceed|The maximum number of Instances is exceeded.|超过了实例数的上限。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|暂不支持指定的网络计费方式，请确认相关参数是否正确。|
|403|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|403|InstanceType.Offline|%s|实例规格因停售、供货不足等原因，不支持该操作。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|ReleaseTimeHaveBeenSet|The specified instance has been set released time.|指定的实例已设置释放时间。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|Account.Arrearage|Your account has an outstanding payment.|您的账号存在未支付的款项。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|您当前的请求被流控，请5分钟后重试。|
|403|InvalidParameter.NotMatch|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|InvalidAction|%s|操作无效。|
|400|Throttling|%s|请求被流控。|
|400|QuotaExceed.AfterpayInstance|The maximum number of Pay-As-You-Go instances is exceeded: %s|按量付费的实例库存不足，请减少创建数量。|
|400|InvalidParameter.Bandwidth|%s|指定的带宽无效，请检查参数是否正确。|
|400|QuotaExceed.RufundVcpu|The maximum number of refund vcpu is exceeded: %s|退款规则中vCPU配额超过了最大数量限制，具体限制请参见错误信息中%s占位符的实际信息。|
|400|InvalidPeriod.UnitMismatch|The specified Period must be correlated with the PeriodUnit.|指定的时长必须与PeriodUnit关联。|
|400|InvalidImageType.NotSupported|%s|指定的镜像类型无效，请查询本地域是否支持此镜像类型。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例过期日期不能超过专有宿主机的过期日期。|
|400|InvalidMarketImageChargeType.NotSupport|The specified chargeType of marketImage is unsupported.|暂不支持该市场镜像的付费类型。|
|403|QuotaExceed.PostPaidDisk|Living postPaid disks quota exceeded.|按量付费磁盘数量已超出允许数量。|
|403|ImageNotSupportInstanceType|The specified instanceType is not supported by instance with marketplace image.|指定的市场镜像不支持该实例规格。|
|403|InvalidInstanceType.PhasedOut|This instanceType is no longer offered.|您指定的实例规格已下线不再出售。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|当前操作不支持此系统磁盘类型。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|RealNameAuthenticationError|Your account has not passed the real-name authentication yet.|您的帐户尚未通过实名认证，请先实名认证后再操作。|
|400|InvalidInstance.NotFoundSystemDisk|The specified instance has no system disk.|指定的实例没有挂载系统盘。请确保指定的实例已挂载了系统盘。您可以调用DescribeInstances查询指定实例的信息。|
|403|QuotaExceed.ElasticQuota|No additional quota is available for the specified ECS instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type.|您在当前地域选择的实例规格所要创建的台数超出系统限额，您可以选择其他地域、实例规格或减少台数重新购买，也可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您的全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|403|QuotaExceed.ElasticQuota|The number of the specified ECS instances has exceeded the quota of the specified instance type, or the number of vCPUs assigned to the ECS instances has exceeded the quota in the zone.|您在当前地域选择的实例规格所要创建的台数超出系统限额，或者全实例规格vCPU配额超出系统限额，您可以前往ECS管理控制台或配额中心申请提高限额。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

