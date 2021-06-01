# CreateCapacityReservation

调用CreateCapacityReservation创建容量预定服务。

## 接口说明

您可以通过容量预定服务，指定可用区、实例规格等属性，系统会以私有池的方式预留属性相匹配的资源。更多信息，请参见[立即生效容量预定概述](~~193633~~)。

-   资源保障服务正在邀测中。如需使用，请[提交工单](https://workorder-intl.console.aliyun.com/console.htm)。
-   目前服务仅支持立即生效模式。购买立即生效容量预定服务后，实例规格即开始遵循按量付费标准计费，不论是否实际创建了按量付费实例，直至您自行手动释放或到期系统自动释放立即生效容量预订。
    -   您可以通过[CreateInstance](~~25499~~)或[RunInstances](~~63440~~)创建实例时设置私有池容量选项，或者通过[ModifyInstanceAttachmentAttributes](~~190006~~)修改实例的私有池容量选项。实例成功匹配私有池容量后，将根据您的实例配置收取实例规格、云盘、公网带宽等相关资源费用。
    -   未实际创建按量付费实例时，仅收取实例规格的费用。
-   立即生效容量预定的匹配的实例和未使用的容量账单支持通过节省计划、地域级预留实例券抵扣小时账单，不支持通过可用区级预留实例券抵扣小时账单。推荐您先购买预留实例券或节省计划，在预留实例券或节省计划的覆盖下使用立即生效容量预定服务，可以免费获取资源的确定性保障。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateCapacityReservation&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateCapacityReservation|系统规定参数。取值：CreateCapacityReservation |
|InstanceType|String|是|ecs.g6.xlarge|实例规格。目前仅支持为一个实例规格设置容量预定服务。 |
|InstanceAmount|Integer|是|2|在一个实例规格内，需要预留的实例的总数量。 |
|RegionId|String|是|cn-hangzhou|容量预定服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId.N|RepeatList|是|cn-hangzhou-h|容量预定服务所属地域下的可用区ID。目前仅支持在一个可用区下创建容量预定服务。 |
|ClientToken|String|否|0c593ea1-3bea-11e9-b96b-88e9fe637760|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。`ClientToken`只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|PrivatePoolOptions.Name|String|否|crpTestName|容量预定服务的名称。长度为2~128个英文或中文字符。必须以大小写字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|This is description.|容量预定服务的描述信息。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |
|PrivatePoolOptions.MatchCriteria|String|否|Open|容量预定服务生效后生成的私有资源池的类型。取值范围：

 -   Open：开放模式。
-   Target：专用模式。

 默认值：Open |
|StartTime|String|否|Now|容量预定服务的生效方式。用于设置非立即生效的指定生效时间或立即生效。目前仅支持设置为立即生效，且参数无需传值。

 **说明：** 该参数不传值即表示设置为立即生效。 |
|EndTimeType|String|否|Unlimited|容量预定服务的失效方式。取值范围：

 -   Limited：指定时间释放。必须同时指定`EndTime`参数。
-   Unlimited：手动释放。不限制时间。 |
|EndTime|String|否|2021-10-30T06:32:00Z|容量预定服务的失效时间。时间格式以ISO8601为标准，并需要使用UTC +0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。更多信息，请参见[ISO8601](~~25696~~)。 |
|Platform|String|否|Linux|实例使用的镜像的操作系统类型。该参数与地域级预留实例券的`Platform`参数对应。如果容量预定服务和地域级预留实例券的操作系统类型相匹配，则可以使用地域级预留实例券来抵扣容量预定服务中的未使用容量的账单。取值范围：

 -   Windows：Windows Server类型的操作系统。
-   Linux：Linux及类Unix类型的操作系统。

 默认值：Linux

 **说明：** 该参数暂未开放使用。 |
|Tag.N.Key|String|否|TestKey|容量预定服务的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://`。 |
|Tag.N.Value|String|否|TestValue|容量预定服务的标签值。N的取值范围：1~20。一旦传入该值，允许为空字符串。最多支持128个字符，不能以`acs:`开头，不能包含`http://`或者`https://`。 |
|ResourceGroupId|String|否|rg-bp67acfmxazb4p\*\*\*\*|容量预定服务所在的企业资源组ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PrivatePoolOptionsId|String|crp-bp67acfmxazb4\*\*\*\*|容量预定服务ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateCapacityReservation
&RegionId=cn-hangzhou
&InstanceType=ecs.g6.xlarge
&InstanceAmount=2
&ZoneId.1=cn-hangzhou-h
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateCapacityReservationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PrivatePoolOptionsId>crp-bp67acfmxazb4****</PrivatePoolOptionsId>
</CreateCapacityReservationResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PrivatePoolOptionsId": "crp-bp67acfmxazb4****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|400|InvalidStartTime.NotSupported|The specified StartTime should be within 180 calendar days from the current date, and you must specify a precision to hour.|指定的StartTime参数不在有效取值范围内。|
|400|InvalidStartTime.MalFormed|The specified StartTime is out of the permitted range.|指定的StartTime参数超出了最大有效取值。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|OperationDenied|The specified InstanceType or Zone is not available or not authorized.|指定的实例规格或可用区不可用或者未授权。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|OperationDenied.NoStock|The resource is out of stock in the specified zone. Please try other types, or choose other regions and zones.|指定的资源在指定可用区中无货。请尝试其他类型，或选择其他可用区和地域。|
|403|InvalidInstanceType.NotSupported|The specified InstanceType is invalid.|指定的参数“InstanceType”无效。|
|404|InvalidZoneId.NotFound|The specified zoneId does not exist.|指定的可用区ID不存在。|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|指定可用区已经售罄，请您更换实例规格或者更换地域创建。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

