# PurchaseReservedInstancesOffering

调用PurchaseReservedInstancesOffering购买一张预留实例券。预留实例券可以自动匹配对应的ECS实例，抵扣按量付费实例账单。

## 接口说明

-   请确保在使用该接口前，您已充分了解预留实例券的计费方式。详情请参见[预留实例券计费方式](~~100371~~)。
-   购买预留实例券前，您可以调用[DescribeAvailableResource](~~66186~~)查询可用实例资源。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=PurchaseReservedInstancesOffering&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PurchaseReservedInstancesOffering|系统规定参数。取值： PurchaseReservedInstancesOffering |
|InstanceType|String|是|ecs.g5.large|实例的资源规格。更多详情，请参见[实例规格族](~~25378~~)。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Scope|String|否|Zone|预留实例券的范围。取值范围：

 -   Region：地域级别
-   Zone：可用区级别

 默认值：Region |
|ZoneId|String|否|cn-hangzhou-g|实例所属的可用区编号，当`Scope`为`Zone`时必填。更多详情，请参见[DescribeZones](~~25610~~)获取可用区列表。 |
|InstanceAmount|Integer|否|3|预留实例券可以同时匹配同规格按量付费实例的数量。取值范围：1~50

 例如，实例规格设置为ecs.g5.large，预留实例数量设置为3时，该预留实例券就可以同时匹配3台规格为ecs.g5.large的按量付费实例。 |
|Platform|String|否|Linux|实例使用的镜像的操作系统类型。取值范围：

 -   Windows：Windows Server类型的操作系统。
-   Linux（默认）：Linux及类Unix类型的操作系统。 |
|PeriodUnit|String|否|Year|购买预留实例券的时长单位。取值范围：Year |
|Period|Integer|否|1|购买预留实例券的时长。取值范围：\{1, 3\}

 默认值：1 |
|OfferingType|String|否|All Upfront|预留实例券的付款类型。取值范围：

 -   No Upfront：零预付
-   Partial Upfront：部分预付
-   All Upfront（默认）：全预付 |
|ReservedInstanceName|String|否|testReservedInstanceName|预留实例券的名称。长度为2~128个英文或中文字符。必须以大小写字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 |
|Description|String|否|testDescription|预留实例券的描述。长度为2~256个英文或中文字符，不能以http://和https://开头。

 默认值：空 |
|ResourceGroupId|String|否|rg-bp199lyny9b3\*\*\*\*|资源组ID。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|Tag.N.Key|String|否|TestKey|预留实例券的标签键。 |
|Tag.N.Value|String|否|TestValue|预留实例券的标签值。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8C314443-AF0D-4766-9562-C83B7F1A3C8B|请求ID。 |
|ReservedInstanceIdSets|List|ecsri-2ze53qonjqxg7r\*\*\*\*|预留实例券ID列表。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=PurchaseReservedInstancesOffering
&RegionId=cn-hangzhou
&Scope=Zone
&ZoneId=cn-hangzhou-a
&ReservedInstanceName=test
&InstanceType=ecs.g5.2xlarge
&InstanceAmount=1
&OfferingType=AllUpfront
&Period=1
&PeriodUnit=Year
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<PurchaseReservedInstancesOfferingResponse>
      <RequestId>8C314443-AF0D-4766-9562-C83B7F1A3C8B</RequestId>
      <ReservedInstanceIdSets>
            <ReservedInstanceId>ecsri-2ze53qonjqxg7r****</ReservedInstanceId>
      </ReservedInstanceIdSets>
</PurchaseReservedInstancesOfferingResponse>
```

`JSON`格式

```
{
    "ReservedInstanceIdSets":{
        "ReservedInstanceId":[
            "ecsri-2ze53qonjqxg7r****"
        ]
    },
    "RequestId":"8C314443-AF0D-4766-9562-C83B7F1A3C8B"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidDescription.Malformed|The specified parameter "Description" is not valid.|指定的资源描述格式不合法。长度为2-256个字符，不能以http://和https://开头。|
|400|InvalidParameter.Conflict|The specified region and cluster do not match.|指定的地域与指定的集群不匹配。|
|400|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|指定的标签键参数有误。|
|400|RegionUnauthorized|%s|该地域未被授权。|
|400|Zone.NotOnSale|%s|该可用区暂时关闭了售卖。|
|400|InvalidPeriodUnit.ValueNotSupported|The specified parameter PeriodUnit is not valid.|参数PeriodUnit无效。|
|400|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|指定的标签值参数有误。|
|400|InvalidChargeType.ValueNotSupported|ChargeType is not valid|付费类型无效。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType beyond the permitted range.|指定的实例规格不合法（超出可选范围）。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|403|OperationDenied|The creation of Host to the specified Zone is not allowed.|无法在指定可用区创建专用宿主机。|
|403|OperationDenied.NoStock|The requested resource is sold out in the specified zone; try other types of resources or other regions and zones.|库存不足。|
|403|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|指定的地域暂时关闭了此资源的售卖，请稍后重试。|
|403|NodeControllerUnavailable|The Node Controller is temporarily unavailable.|节点控制器暂不可用。|
|403|OperationDenied|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|指定的ResourceOwnerAccount不合法。|
|403|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|用户未被授权购买指定的可用区的资源。|
|403|Zone.NotOnSale|The specified zone is not available for purchase.|指定可用区已经售罄，请您更换实例规格或者更换地域创建。|
|403|InvalidParameter.NotMatch|%s|您输入的参数无效，请检查参数之间是否冲突。|
|403|Account.Arrearage|Your account has been in arrears.|账户余额不足，请先充值再操作。|
|404|PaymentMethodNotFound|No payment method has been registered on the account.|账户尚未注册支付方式。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|%s|内部错误。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

