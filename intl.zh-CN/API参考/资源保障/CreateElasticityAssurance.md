# CreateElasticityAssurance

调用CreateElasticityAssurance创建弹性保障服务。

## 接口说明

弹性保障服务为您提供了兼顾灵活性和确定性的全新的资源购买和使用方式，是一种能够向计费方式为按量付费的ECS实例，提供确定性保障的资源预定服务。更多信息，请参见[弹性保障概述](~~193630~~)。

-   资源保障服务正在邀测中。如需使用，请[提交工单](https://workorder-intl.console.aliyun.com/console.htm)。
-   购买弹性保障服务后，不支持退款。
-   弹性保障服务只能创建计费方式为按量付费的ECS实例。
-   目前弹性保障次数只开放了无限次的模式，即`AssuranceTimes`参数只支持设置为`Unlimited`。无限次模式的弹性保障服务在保障生效后，将自动启动。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateElasticityAssurance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateElasticityAssurance|系统规定参数。取值：CreateElasticityAssurance |
|RegionId|String|是|cn-hangzhou|弹性保障服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId.N|RepeatList|是|cn-hangzhou-h|弹性保障服务所属地域下的可用区ID。目前仅支持在一个可用区下创建弹性保障服务。 |
|InstanceType.N|RepeatList|是|ecs.c6.xlarge|实例规格。目前仅支持为一个实例规格设置弹性保障服务。 |
|Period|Integer|否|1|购买时长。时长单位由`PeriodUnit`参数确定。取值范围：

 -   当`PeriodUnit`参数值为`Month`时，该参数的取值：\{“1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”\}。
-   当`PeriodUnit`参数值为`Year`时，该参数的取值：\{“1”, “2”, “3”, “4”, “5”\}。

 默认值：1 |
|PeriodUnit|String|否|Year|时长单位。取值范围：

 -   Month：月
-   Year：年

 默认值：Year |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。`ClientToken`只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|PrivatePoolOptions.Name|String|否|eapTestName|弹性保障服务的名称。长度为2~128个英文或中文字符。必须以大小写字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|This is description.|弹性保障服务的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |
|PrivatePoolOptions.MatchCriteria|String|否|Open|弹性保障服务的匹配模式。取值范围：

 -   Open：开放模式的弹性保障服务。
-   Target：指定模式的弹性保障服务。

 默认值：Open |
|AssuranceTimes|String|否|Unlimited|弹性保障的总次数。取值：Unlimited，目前仅支持在服务生效期内的无限次模式。

 默认值：Unlimited |
|InstanceAmount|Integer|否|2|在一个实例规格内，需要预留的实例的总数量。 |
|StartTime|String|否|2020-10-30T06:32:00Z|弹性保障服务生效时间。默认为调用该接口创建服务的时间。时间格式以ISO8601为标准，需要使用UTC +0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。更多信息，请参见[ISO8601](~~25696~~)。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|弹性保障服务所在的企业资源组ID。 |
|Tag.N.Key|String|否|TestKey|弹性保障服务的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|TestValue|弹性保障服务的标签值。N的取值范围：1~20。一旦传入该值，允许为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|1234567890|生成的订单ID。 |
|PrivatePoolOptionsId|String|eap-bp67acfmxazb4\*\*\*\*|弹性保障服务ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateElasticityAssurance
&RegionId=cn-hangzhou
&InstanceType.1=ecs.c6.xlarge
&ZoneId.1=cn-hangzhou-h
&InstanceAmount=2
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateElasticityAssuranceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PrivatePoolOptionsId>eap-bp67acfmxazb4****</PrivatePoolOptionsId>
      <OrderId>1234567890</OrderId>
</CreateElasticityAssuranceResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PrivatePoolOptionsId": "eap-bp67acfmxazb4****",
    "OrderId": "1234567890"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|400|InvalidStartTime.NotSupported|The specified StartTime should be within 180 calendar days from the current date, and you must specify a precision to hour.|指定的StartTime参数不在有效取值范围内。|
|400|InvalidStartTime.MalFormed|The specified StartTime is out of the permitted range.|指定的StartTime参数超出了最大有效取值。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|指定的实例规格或可用区不可用或者未授权。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|指定的资源在指定可用区中无货。请尝试其他类型，或选择其他可用区和地域。|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is invalid.|指定的参数“InstanceType”无效。|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|指定的可用区ID不存在。|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|指定可用区已经售罄，请您更换实例规格或者更换地域创建。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

