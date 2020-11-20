# DescribeSpotPriceHistory

调用DescribeSpotPriceHistory查询抢占式实例近30天内的历史价格。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSpotPriceHistory&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSpotPriceHistory|系统规定参数。取值：DescribeSpotPriceHistory |
|InstanceType|String|是|ecs.t1.xsmall|实例规格。 |
|NetworkType|String|是|vpc|抢占式实例网络类型。取值范围：

 -   classic：表示抢占式实例的网络类型为经典网络。
-   vpc：表示抢占式实例的网络类型为专有网络。 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|否|cn-hangzhou-g|可用区ID。 |
|SpotDuration|Integer|否|1|抢占式实例的保留时长，单位为小时。取值范围：0~6

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   取值为0，则为无保护期模式。

 默认值：1 |
|IoOptimized|String|否|optimized|是否为I/O优化实例。取值范围：

 -   optimized：表示抢占式实例为I/O优化实例。
-   none：表示抢占式实例为非I/O优化实例。

 系列I实例默认值：none

 其余实例规格族默认值：optimized |
|StartTime|String|否|2017-08-22T08:45:08Z|查询抢占式实例历史价格的起始时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。

 默认值：空，空代表结束时间前3小时，最大值不得超过指定的结束时间30天。 |
|EndTime|String|否|2017-08-22T08:45:08Z|查询抢占式实例历史价格的结束时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。

 默认值：空，空表示当前时间。 |
|OSType|String|否|linux|操作系统的发行平台类型。取值范围：

 -   linux
-   windows |
|Offset|Integer|否|0|查询开始行。

 默认值：0 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Currency|String|CNY|价格的货币单位。 |
|NextOffset|Integer|1000|下一页开始行，查询下一页的数据。参数`Offset`的指定值为该值。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|SpotPrices|Array of SpotPriceType| |抢占价格详情。 |
|SpotPriceType| | | |
|InstanceType|String|ecs.g5.large|抢占式实例的实例规格。 |
|IoOptimized|String|optimized|抢占式实例是否为I/O优化实例。 |
|NetworkType|String|vpc|抢占式实例的网络类型。 |
|OriginPrice|Float|0.354|按量付费实例部分原价。 |
|SpotPrice|Float|0.036|抢占式实例价格。 |
|Timestamp|String|2019-11-19T06:00:00Z|时间格式为`yyyy-MM-ddTHH:mm:ssZ`的价格时间。 |
|ZoneId|String|cn-hangzhou-c|抢占式实例所属的可用区ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeSpotPriceHistory
&NetworkType=vpc
&RegionId=cn-hangzhou
&InstanceType=ecs.g5.large
&StartTime=2019-11-19T00:00:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeSpotPriceHistoryResponse>
      <RequestId>5E2D59BA-4EB0-45C4-A0D7-D98C1A4B320B</RequestId>
      <SpotPrices>
            <SpotPriceType>
                  <IoOptimized>optimized</IoOptimized>
                  <OriginPrice>0.354</OriginPrice>
                  <NetworkType>vpc</NetworkType>
                  <ZoneId>cn-hangzhou-g</ZoneId>
                  <Timestamp>2019-11-19T06:00:00Z</Timestamp>
                  <SpotPrice>0.036</SpotPrice>
                  <InstanceType>ecs.g5.large</InstanceType>
            </SpotPriceType>
            <SpotPriceType>
                  <IoOptimized>optimized</IoOptimized>
                  <OriginPrice>0.354</OriginPrice>
                  <NetworkType>vpc</NetworkType>
                  <ZoneId>cn-hangzhou-g</ZoneId>
                  <Timestamp>2019-11-19T07:00:00Z</Timestamp>
                  <SpotPrice>0.036</SpotPrice>
                  <InstanceType>ecs.g5.large</InstanceType>
            </SpotPriceType>
      </SpotPrices>
      <Currency>CNY</Currency>
</DescribeSpotPriceHistoryResponse>
```

`JSON` 格式

```
{
	"RequestId": "5E2D59BA-4EB0-45C4-A0D7-D98C1A4B320B",
	"SpotPrices": {
		"SpotPriceType": [
			{
				"IoOptimized": "optimized",
				"OriginPrice": 0.354,
				"NetworkType": "vpc",
				"ZoneId": "cn-hangzhou-g",
				"Timestamp": "2019-11-19T06:00:00Z",
				"SpotPrice": 0.036,
				"InstanceType": "ecs.g5.large"
			},
			{
				"IoOptimized": "optimized",
				"OriginPrice": 0.354,
				"NetworkType": "vpc",
				"ZoneId": "cn-hangzhou-g",
				"Timestamp": "2019-11-19T07:00:00Z",
				"SpotPrice": 0.036,
				"InstanceType": "ecs.g5.large"
			}
		]
	},
	"Currency": "CNY"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidUserType.NotSupported|%s|您当前的账号不支持此操作。|
|403|Abs.InvalidAccount.NotFound|%s|您的阿里云账号不存在，或者您的AccessKey已经过期。|
|400|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|Forbedden.NotSupportRAM|%s|暂不支持RAM用户执行该操作。|
|400|UnsupportedParameter|%s|不支持参数。|
|403|Forbbiden.SubUser|%s|您的账号没有操作此资源的权限，请向主账号申请相关的权限。|
|400|InvalidParameter|%s|无效的参数。|
|400|InvalidInstanceID.Malformed|%s|参数InstanceId格式错误。|
|400|InvalidParams.StartTime|%s|指定的参数StartTime无效。|
|400|InvalidParams.EndTime|%s|指定的参数EndTime无效。|
|400|Abs.Abs.InvalidSpotInstanceUID|%s|抢占式实例ID格式不正确。|
|400|InvalidParams.NetworkType|%s|指定的参数NetworkType无效。|
|400|InvalidParams.IoOptimized|%s|指定的参数IoOptimized无效。|
|400|InvalidParams.OSType|%s|指定的参数OSType无效。|
|400|Abs.IoOptimized.ValueNotSupported|%s|实例I/O优化属性无效，请检查参数设置是否正确。|
|400|InvalidZoneId.NotFound|The specified zone does not exist.|指定的可用区ID不存在。|
|400|InvalidParams.ZoneId|%s|指定的参数ZoneId无效。|
|400|InvalidParams.RegionId|%s|指定的参数RegionId无效。|
|400|InvalidParams.InstanceType|%s|指定的参数InstanceType无效。|
|400|InvalidParams.PageSize|%s|指定的参数PageSize无效。|
|400|InvalidParams.Offset|%s|指定的参数Offset无效。|
|400|InvalidInstanceType.ValueNotSupported|%s|该操作暂不支持指定的实例类型。|
|400|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为I/O优化实例，请您检查实例规格是否正确。|
|400|InvalidSpotDuration|The specified SpotDuration is not valid.|指定的SpotDuration参数有误。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

