# DescribeRenewalPrice

You can call this operation to query the renewal price of subscription ECS instances. This operation is in internal preview.

You must [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to apply for using DescribeRenewalPrice. Otherwise, InvalidAction is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeRenewalPrice&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeRenewalPrice|The operation that you want to perform. Set the value to DescribeRenewalPrice. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|ResourceId|String|Yes|i-bp1f2o4ldh8l29zv\*\*\*\*|The ID of the specified resource whose renewal price is to be queried. When the ResourceType parameter is set to instance, the Resource ID is the value of the InstanceId parameter. |
|ResourceType|String|No|instance|The type of the specified resource whose renewal price is to be queried. Set the value to instance.

Default value: instance. |
|Period|Integer|No|1|The renewal period. The valid values of this parameter depend on the value specified for the PriceUnit parameter. Valid values:

-   Valid values when PriceUnit is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9
-   Valid values when PriceUnit is set to Year: 1, 2, and 3.

Default value: 1. |
|PriceUnit|String|No|Month|The unit of the renewal period. Valid values:

-   Month
-   Year

Default value: Month. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PriceInfo|Struct| |Details about the PriceInfo data, including the price and discount rules. |
|Price|Struct| |The price. |
|Currency|String|CNY|The currency unit. |
|DetailInfos|Array| |Details about the resource prices. |
|ResourcePriceModel| | | |
|DiscountPrice|Float|655.2|The discount. |
|OriginalPrice|Float|4368|The original price. |
|Resource|String|instance|The name of the resource corresponding to the price. |
|SubRules|Array| |Details about the pricing rules. |
|Rule| | | |
|Description|String|Receive a 15% discount on a 1-year subscription|The description of the pricing rule. |
|RuleId|Long|1234567890|The ID of the pricing rule. |
|TradePrice|Float|3712.8|The transaction price. |
|DiscountPrice|Float|655.2|The discount. |
|OriginalPrice|Float|4368|The original price. |
|TradePrice|Float|3712.8|The transaction price, which is equal to the original price minus the discount. |
|Rules|Array| |Details about the promotion rules. |
|Rule| | | |
|Description|String|Receive a 15% discount on a 1-year subscription|The description of the promotion rule. |
|RuleId|Long|1234567890|The ID of the promotion. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeRenewalPrice
&RegionId=cn-hangzhou
&ResourceId=i-bp1f2o4ldh8l29zv****
&Period=1
&PriceUnit=Month
&<Common request parameters>
```

Sample success responses

`XML` format

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
                        <Description>Receive a 15% discount on a 1-year subscription. </Description>
                        <RuleId>ONE_YEAR_85_PERCENT</RuleId>
                  </Rule>
            </Rules>
      </PriceInfo>
</DescribeRenewalPriceResponse>
```

`JSON` format

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
          "Description":"Receive a 15% discount on 1-year subscription",
          "Code": "ONE_YEAR_85_PERCENT"
        }
      ]
    }
  }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError|%s|The error message returned because an internal error has occurred.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|
|400|InvalidResourceType.ValueNotSupported|The specified parameter ResourceType is not valid.|The error message returned because the specified ResourceType parameter is invalid.|
|400|InvalidPeriod|The specified period is not valid.|The error message returned because the specified Period parameter is invalid.|
|400|InvalidPriceUnit.ValueNotSupported|The specified parameter PriceUnit is not valid.|The error message returned because the specified PriceUnit parameter is invalid.|
|400|Throttling|Request was denied due to request throttling.|The error message returned because the request is denied due to throttling. Try again later.|
|403|ChargeTypeViolation|The operation is not permitted due to charge type of the instance.|The error message returned because the operation is not supported while the instance uses the current billing method.|
|400|InternalError|The request processing has failed due to some unknown error.|The error message returned because an internal error has occurred. Try again later. If the error persists, submit a ticket.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

