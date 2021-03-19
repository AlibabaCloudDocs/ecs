# RenewInstance

调用RenewInstance续费一台包年包月ECS实例。

## 接口说明

请确保在使用该接口前，您已充分了解[云服务器ECS](https://www.alibabacloud.com/product/ecs#pricing)的计费方式和产品定价。

调用该接口时，您需要注意：

-   仅支持为包年包月ECS实例续费时长或者续费至统一到期日。
-   续费实例的时长和续费实例至统一到期日的操作不能同步执行，即续费时长参数（`Period`、`PeriodUnit`）与统一到期日参数（`ExpectedRenewDay`）必须指定其中之一，但不能同时设置。
-   您的账号必须支持信用支付。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=RenewInstance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RenewInstance|系统规定参数。取值：RenewInstance |
|InstanceId|String|是|i-bp67acfmxazb4p\*\*\*\*|需要续费的实例ID。 |
|Period|Integer|否|1|包年包月续费时长。一旦指定了`DedicatedHostId`，则取值范围不能超过专有宿主机的订阅时长。取值范围：

 -   参数`PeriodUnit`值为`Month`。`Period`取值为：1~12, 24, 36, 48, 60

 **说明：** 您必须指定续费时长参数（`Period`、`PeriodUnit`）或统一到期日参数（`ExpectedRenewDay`）的其中一个，但不能同时设置。 |
|PeriodUnit|String|否|Month|续费时长的时间单位，即参数Period的单位。取值范围：

 -   Month（默认） |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|ExpectedRenewDay|Integer|否|5|统一到期日。该参数值必须与您已设置的统一到期日保持一致，否则将调用失败。指定该参数后，您的实例将续费至统一到期日。取值范围：1~28。

 关于统一到期日功能的限制说明，请参见[统一实例到期日](~~108486~~)。

 **说明：** 您必须指定续费时长参数（`Period`、`PeriodUnit`）或统一到期日参数（`ExpectedRenewDay`）的其中一个，但不能同时设置。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|1234567890|订单ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=RenewInstance
&InstanceId=i-bp67acfmxazb4p****
&Period=1
&PeriodUnit=Month
&ClientToken=0c593ea1-3bea-11e9-b96b-88e9fe637760
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<RenewInstanceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <OrderId>1234567890</OrderId>
</RenewInstanceResponse>
```

`JSON`格式

```
{
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"OrderId": "1234567890"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|暂不支持指定的网络付费类型的实例，请确认相关参数是否正确。|
|400|InvalidInstanceType.NotSupported|The specified InstanceType is not Supported.|不支持指定的InstanceType。|
|400|InvalidParameter|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的InternetMaxBandwidthOut参数不合法。|
|400|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|指定的实例计费方式不存在。|
|400|InvalidRebootTime.ValueNotSupported|The specified RebootTime is out of the permitted range.|指定的重启时间超出取值范围。|
|400|IdempotenceParamNotMatch|Request uses a client token in a previous request but is not identical to that request.|与相同ClientToken的请求参数不符合。|
|400|InvalidClientToken.ValueNotSupported|The ClientToken provided is invalid.|指定的ClientToken不合法。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|403|Diskcategory.Mismatch|The disk specified to convert to portable is not allowed due to the disk category does not support.|由于磁盘种类限制，指定的磁盘不能转换为可卸载磁盘。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|400|InvalidInstanceType.codeUnauthorized|The specified InstanceType is not authorized.|指定的InstanceType不合法。|
|400|InvalidInternetChargeType.InstanceNotSupported|The specified instance which is in vpc is not support the parameter InternetChargeType.|指定的VPC网络实例不支持指定的网络计费方式。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|400|MissingParamter|The specified parameter "Period" is not null.|参数Period不得为空。|
|403|InstanceSpecModification.NotEffective|The specified instance has been reserved for making a spec modification and not taken effective in the current contract period.|指定的实例因规格调整被保留，在当前合同期内无法生效。|
|400|Upgrade.NotSupported|Upgrade operation is not supported.|升级操作不合法。|
|403|LastTokenProcessing|The last token request is processing.|正在处理上一条令牌请求，请您稍后再试。|
|403|Instance.UnPaidOrder|The specified instance has unpaid order.|该实例有未完成的账单。|
|400|OperationDenied|Specified instance is in VPC.|指定实例存在于VPC。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidParameter|The specified parameter " InternetMaxBandwidthOut " is not valid.|指定的参数InternetMaxBandwidthOut无效。|
|403|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|实例被安全锁定，指定的操作无法完成。|
|403|InvalidDisk.NotAllowed|The specified disk is not allowed to be converted to portable.|指定的磁盘不允许转换为可卸载磁盘。|
|400|DependencyViolation.InstanceType|Current instancetype cannot be changed to the specified one.|当前实例规格不能更改为指定规格。|
|403|InstanceTypeNotSupported|The specified zone does not offer the specified instancetype.|指定的可用区不支持指定的实例规格。|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|参数PeriodUnit无效。|
|400|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist.|指定的专有宿主机不存在。|
|400|InvalidDedicatedHostStatus.NotSupport|Operation denied due to dedicated host status.|专有宿主机当前的状态不支持此操作。|
|400|IncorrectDedicatedHostStatus|The current status of the resource does not support this operation.|当前资源的状态不支持此操作。|
|400|InvalidPeriod.ExceededDedicatedHost|Instance expired date can't exceed dedicated host expired date.|实例过期日期不能超过专有宿主机的过期日期。|
|400|InvalidStatus.Upgrading|The instance is upgrading; please try again later.|实例正在升级，请稍后重试。|
|400|InvalidPeriod.ExceededMaximumExpirationDate|The specified renewal period cannot exceed the maximum expiration date. We recommend you try shortening the renewal period at next attempt.|指定的续订期限不能超过最大有效期限。我们建议您尝试在下次尝试时缩短续订时间。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|LastOrderProcessing|The previous order is still processing, please try again later.|订单正在处理中，稍后重试。|
|400|Idempotence.Processing|The previous request is still processing, please try again later.|请求正在处理中，稍后重试。|
|403|InvalidChargeType.NotSupported|The chargeType of the instance does not support this operation.|该付费类型的实例不支持该操作。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone, try other types of resources or other regions and zones.|请求的资源在指定的可用区已售罄，请您更换实例规格或者可用区重试。|
|403|OperationDenied.NoStock|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|400|OperationDenied|The current user does not support this operation.|您使用的账号暂不支持此操作。|
|403|InvalidPeriod.StarterPackage|This instance was created by using a Starter Package plan and can only be renewed monthly, not yearly.|参加了入门级套餐活动的实例，只能设置成每月自动续费。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

