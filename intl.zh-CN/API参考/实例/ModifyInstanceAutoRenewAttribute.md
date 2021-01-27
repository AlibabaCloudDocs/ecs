# ModifyInstanceAutoRenewAttribute

调用ModifyInstanceAutoRenewAttribute设置一台或多台包年包月实例的自动续费状态。为了减少您的资源到期维护成本，包年包月ECS实例可以设置自动续费。

## 接口说明

请确保在使用该接口前，您已充分了解[云服务器ECS](https://www.alibabacloud.com/product/ecs#pricing)的计费方式和产品定价。

-   自动续费扣款日为实例到期前第9天，扣费在北京时间（UTC +8）08:00:00开始执行。
-   如果前一日执行自动扣费失败，将会继续下一日定时继续执行，直到扣费成功或者9天之后实例到期锁定。您只需要保证自己的账号的余额或者信用额度充足即可。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceAutoRenewAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ModifyInstanceAutoRenewAttribute|系统规定参数。取值：ModifyInstanceAutoRenewAttribute |
|InstanceId|String|是|i-bp67acfmxazb4ph\*\*\*\*,i-bp67acfmxazb4pi\*\*\*\*|实例ID。支持批量设置最多100个包年包月实例，多个实例ID以英文逗号分隔。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Duration|Integer|否|1|设置实例自动续费时长。

 -   `PeriodUnit`为`Year`（年）时，`Duration`的取值范围为：\{"1", "2", "3"\}
-   `PeriodUnit`为`Month`（月）时，`Duration`的取值范围为：\{"1", "2", "3", "6", "12"\} |
|AutoRenew|Boolean|否|true|实例到期前是否自动续费。

 默认值：false |
|RenewalStatus|String|否|AutoRenewal|实例的自动续费状态。取值范围：

 -   AutoRenewal：设置为自动续费。
-   Normal：取消自动续费。
-   NotRenewal：不再续费。传入该值后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的ECS实例可以更改成待续费（`Normal`）后，再自行续费或设置为自动续费。

 **说明：** 参数`RenewalStatus`的优先级高于参数`AutoRenew`。如果不传入参数`RenewalStatus`，则默认以参数`AutoRenew`为准。 |
|PeriodUnit|String|否|Month|续费时长的时间单位，即参数`Duration`的单位。取值范围：

 -   Month（默认）
-   Year |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-bp67acfmxazb4ph****,i-bp67acfmxazb4pi****
&Duration=1
&PeriodUnit=Month
&AutoRenew=true
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<ModifyInstanceAutoRenewAttributeResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceAutoRenewAttributeResponse>
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
|403|MissingParameter.InstanceId|InstanceId should not be null.|参数InstanceId不能为空。|
|403|InvalidParameter.ToManyInstanceIds|InstanceId should be less than 100.|实例数应小于100。|
|403|InvalidParameter.InvalidInstanceId|%s|指定的参数InstanceId无效。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|403|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|按量付费实例不支持该操作，检查实例的付费类型是否与该操作冲突。|
|403|InvalidParameter.Duration|%s|参数Duration无效。|
|403|InvalidParameter.RenewalStatus|%s|指定的参数RenewalStatus无效。|
|403|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|参数PeriodUnit无效。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidPeriod.StarterPackage|This instance was created by using a Starter Package plan and can only be renewed monthly, not yearly.|参加了入门级套餐活动的实例，只能设置成每月自动续费。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

