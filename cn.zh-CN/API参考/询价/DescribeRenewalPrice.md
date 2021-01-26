# DescribeRenewalPrice

调用DescribeRenewalPrice查询云服务器ECS资源的续费价格。仅支持查询包年包月资源的续费价格。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeRenewalPrice&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeRenewalPrice|系统规定参数。取值：DescribeRenewalPrice |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ResourceId|String|是|i-bp1f2o4ldh8l29zv\*\*\*\*|查询续费价格的资源ID。参数`ResourceType`取值为`instance`时，`ResourceId`可以理解为`InstanceId`。 |
|ResourceType|String|否|instance|查询续费价格的资源类型。取值：instance

 默认值：instance |
|Period|Integer|否|1|指定续费时长。取值范围：

 -   当参数`PriceUnit`取值为`Month`时：1~9
-   当参数`PriceUnit`取值为`Year`时：1~3

 默认值：1 |
|PriceUnit|String|否|Month|指定续费周期。取值范围：

 -   Month：续费周期为一个月。
-   Year：续费周期为一年。

 默认值：Month |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PriceInfo|Struct| |价格信息类型（PriceInfo）组成的数据类型，包括价格和优惠规则信息。 |
|Price|Struct| |价格。 |
|Currency|String|CNY|货币单位。 |
|DetailInfos|Array of ResourcePriceModel| |资源定价详情。 |
|ResourcePriceModel| | | |
|DiscountPrice|Float|655.2|折扣价。 |
|OriginalPrice|Float|4368|原价。 |
|Resource|String|instance|价格对应的资源名称。 |
|SubRules|Array of Rule| |定价规则子集。 |
|Rule| | | |
|Description|String|买满1年，立享官网价格8.5折优惠。|定价规则描述。 |
|RuleId|Long|1234567890|定价规则ID。 |
|TradePrice|Float|3712.8|成交价。 |
|DiscountPrice|Float|655.2|折扣。 |
|OriginalPrice|Float|4368|原价。 |
|TradePrice|Float|3712.8|最终价，为原价减去折扣。 |
|Rules|Array of Rule| |活动规则。 |
|Rule| | | |
|Description|String|买满1年，立享官网价格8.5折优惠。|活动规则描述。 |
|RuleId|Long|1234567890|活动ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeRenewalPrice
&RegionId=cn-hangzhou
&ResourceId=i-bp1f2o4ldh8l29zv****
&Period=1
&PriceUnit=Month
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeRenewalPriceResponse>
      <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
      <PriceInfo>
            <Price>
                  <Currency>CNY</Currency>
                  <DiscountPrice>655.2</DiscountPrice>
                  <OriginalPrice>4368</OriginalPrice>
                  <TradePrice>3712.8</TradePrice>
            </Price>
            <Rules>
                  <Rule>
                        <Description>买满1年，立享官网价格8.5折优惠。</Description>
                        <RuleId>ONE_YEAR_85_PERCENT</RuleId>
                  </Rule>
            </Rules>
      </PriceInfo>
</DescribeRenewalPriceResponse>
```

`JSON`格式

```
{
  "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368",
  "PriceInfo": {
    "Price": {
      "Currency": "CNY",
      "DiscountPrice": 655.2,
      "OriginalPrice": 4368,
      "TradePrice": 3712.8
    },
    "Rules": {
      "Rule": [
        {
          "Description": "买满1年，立享官网价格8.5折优惠。",
          "Code": "ONE_YEAR_85_PERCENT"
        }
      ]
    }
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|%s|内部错误。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|400|InvalidResourceType.ValueNotSupported|The specified parameter ResourceType is not valid.|指定的资源类型不合法。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|400|InvalidPriceUnit.ValueNotSupported|The specified parameter PriceUnit is not valid.|指定的单价不合法。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|付费方式不支持该操作，请您检查实例的付费类型是否与该操作冲突。|
|400|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|403|InvalidAction.Unauthorized|The specified action is not valid.|指定的操作无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

