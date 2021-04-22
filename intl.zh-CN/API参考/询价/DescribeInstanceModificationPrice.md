# DescribeInstanceModificationPrice

调用DescribeInstanceModificationPrice查询未到期的包年包月ECS实例升配时目标实例规格的价格信息、新增包年包月数据盘的价格信息。

## 接口说明

-   仅支持查询未到期的包年包月ECS实例升配的价格信息，暂不支持查询实例降配的价格信息。
-   不支持查询按量付费ECS实例变配时的价格信息。由于按量付费ECS实例变配后的价格与新购实例的价格一致，因此您可以直接调用[DescribePrice](~~107829~~)查询ECS实例的最新价格。
-   实例升配前，建议您先调用[DescribeResourcesModification](~~66187~~)查询指定可用区内可升配的实例规格信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceModificationPrice&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeInstanceModificationPrice|系统规定参数。取值：DescribeInstanceModificationPrice |
|InstanceId|String|是|i-bp1f2o4ldh8l\*\*\*\*|需要查询升配价格的实例ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceType|String|否|ecs.g6e.large|实例升配的目标实例规格。建议您先调用[DescribeResourcesModification](~~66187~~)查询指定可用区内可升配的实例规格信息。

 **说明：** 查询时，实例规格参数（`InstanceType`）和数据盘参数（`DataDisk.N.*`）不得同时为空，必须至少指定一个。 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘类型。仅当从已停售的实例规格升配至在售实例规格，并将非I/O优化实例规格升级为I/O优化实例规格时，才需要传入参数值。关于实例规格的更多信息，请参见[实例规格族](~~25378~~)以及[已停售的实例规格](~~55263~~)。

 取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘

 默认值：无 |
|DataDisk.N.Category|String|否|cloud\_essd|数据盘类型。当您需要查询ECS实例挂载的新包年包月数据盘的价格时，可以传入该参数值。N的取值范围：1~16。取值范围：

 -   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   cloud\_essd：ESSD云盘
-   cloud：普通云盘。

 默认值：无

 **说明：** 查询时，实例规格参数（`InstanceType`）和数据盘参数（`DataDisk.N.*`）不得同时为空，必须至少指定一个。 |
|DataDisk.N.Size|Integer|否|100|数据盘的容量大小。N的取值范围：1~16，内存单位为GiB。取值范围：

 -   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   cloud：5~2000

 默认值：指定数据盘类型相应的容量大小的最小值。 |
|DataDisk.N.PerformanceLevel|String|否|PL1|当数据盘类型为ESSD云盘时，设置云盘的性能等级。N的取值必须和`DataDisk.N.Category=cloud_essd`中的N保持一致。取值范围：

 -   PL0：单盘最高随机读写IOPS 1万
-   PL1：单盘最高随机读写IOPS 5万
-   PL2：单盘最高随机读写IOPS 10万
-   PL3：单盘最高随机读写IOPS 100万

 默认值：PL1

 有关如何选择ESSD性能等级，请参见[ESSD云盘](~~122389~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PriceInfo|Struct| |价格信息类型（PriceInfo）组成的数据类型，包括价格和优惠规则信息。 |
|Price|Struct| |价格。 |
|Currency|String|CNY|货币单位。可能值：

 -   CNY
-   USD |
|DiscountPrice|Float|61.320|折扣。 |
|OriginalPrice|Float|175.200|原价。 |
|TradePrice|Float|113.880|最终价，为原价减去折扣。 |
|Rules|Array of Rule| |活动规则。 |
|Rule| | | |
|Description|String|升级优惠|活动规则描述。 |
|RuleId|Long|1234567890|活动ID。 |
|RequestId|String|A3DC3196-379B-4F32-A2C5-B937134FAD8A|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceModificationPrice
&RegionId=cn-hangzhou
&InstanceId=i-bp1f2o4ldh8l****
&InstanceType=ecs.g6e.large
&DataDisk.1.Category=cloud_essd
&DataDisk.1.Size=100
&DataDisk.1.PerformanceLevel=PL1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeInstanceModificationPriceResponse>
      <RequestId>A3DC3196-379B-4F32-A2C5-B937134FAD8A</RequestId>
      <PriceInfo>
            <Rules>
                  <Rule>
                        <Description>升级优惠</Description>
                        <RuleId>1234567890</RuleId>
                  </Rule>
            </Rules>
            <Price>
                  <OriginalPrice>175.200</OriginalPrice>
                  <Currency>CNY</Currency>
                  <DiscountPrice>61.320</DiscountPrice>
                  <TradePrice>113.880</TradePrice>
            </Price>
      </PriceInfo>
</DescribeInstanceModificationPriceResponse>
```

`JSON`格式

```
{
    "RequestId": "A3DC3196-379B-4F32-A2C5-B937134FAD8A", 
    "PriceInfo": {
        "Rules": {
            "Rule": [
                {
                    "Description": "升级优惠", 
                    "RuleId": "1234567890"
                }
            ]
        }, 
        "Price": {
            "OriginalPrice": "175.200", 
            "Currency": "CNY", 
            "DiscountPrice": "61.320", 
            "TradePrice": "113.880"
        }
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|指定的ResourceOwnerAccount不合法。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|ChargeTypeViolation|PostPaid instance do not support this operation.|该 API 不支持查询按量付费的 ECS 的变配价格。|
|400|MissingParameter.InstanceTypeOrDataDisk|You must specify the parameter InstanceType or DataDisk.|实例规格和数据盘参数二选一必须传一个，不能都为空。|
|403|InvalidInstanceType.NotSupportUpgrade|The specified InstanceType can only be downgraded. This API supports querying prices only of InstanceType that can be upgraded.|指定的实例规格为降配的规格，该API仅支持查询升配的实例规格的价格。建议您通过DescribeResourcesModification接口获取可升配的实例规格。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的SystemDisk.Category不合法。|
|400|InvalidDiskCategory.Missing|The DataDisk.1.Category parameter that is mandatory for processing the request is not provided.|没有指定数据盘类型。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数DataDisk.n.Category不合法。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|400|InstanceType.Offline|%s|实例规格因停售、供货不足等原因，不支持该操作。|
|400|RegionUnauthorized|%s|该地域未被授权。|
|500|InternalError|%s|内部错误。|
|403|InstanceExpired|The PrePaid instance has been expired.|当前实例已过期，不支持查询变配价格。|
|400|InvalidAction.WithActiveElasticUpgrade|The instance has active Elastic Upgrade.|弹性升级中的实例暂不支持|
|400|PriceNotFound|The price of your queried resource is not available now, please try other resources.|未找到价格，请修改相应的参数值重试。|
|403|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

