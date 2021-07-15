# DescribePrice

调用DescribePrice查询云服务器ECS资源的最新价格。

## 接口说明

-   查询不同类型资源的价格时，必需参数也有所不同，具体说明如下：
    -   参数`ResourceType=instance`时，您必须同时指定参数`InstanceType`。
    -   参数`ResourceType=disk`时，您必须同时指定参数`DataDisk.1.Category`和`DataDisk.1.Size`。查询`disk`资源的价格时，只返回云盘按量付费的价格，即参数`PriceUnit`只能取值为`Hour`。
    -   查询`ResourceType=ddh`时，您必须同时指定参数`DedicatedHostType`。
    -   查询`ResourceType=ElasticityAssurance`时，必须同时指定参数`InstanceType`。
    -   查询`ResourceType=CapacityReservation`时，必须同时指定参数`InstanceType`。
-   查询`ResourceType=bandwidth`时，只返回按流量计费（`PayByTraffic`）的价格。
-   参数`ResourceType=instance`时，仅支持查询四块以内数据盘的价格。
-   默认查询付费方式（`ChargeType`）为按量付费（`PostPaid`）的价格，您可以通过指定`PriceUnit`参数查询云服务器ECS不同计费周期的价格。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribePrice&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribePrice|系统规定参数。取值：DescribePrice |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ResourceType|String|否|instance|目标资源的类型。取值范围：

 -   instance：查询ECS实例的最新价格列表。当取值为`instance`时，必须同时指定参数`InstanceType`。
-   disk：查询云盘的最新价格列表。当取值为`disk`时，必须同时指定参数`DataDisk.1.Category`和`DataDisk.1.Size`。
-   bandwidth：查询带宽的最新价格列表。
-   ddh：查询专有宿主机的最新价格列表。
-   ElasticityAssurance：查询弹性保障服务的价格信息。当取值为`ElasticityAssurance`时，必须同时指定参数`InstanceType`。
-   CapacityReservation：查询容量预定服务的价格信息。当取值为`CapacityReservation`时，必须同时指定参数`InstanceType`。

 默认值：instance |
|ImageId|String|否|centos\_7\_05\_64\_20G\_alibase\_20181212.vhd|镜像ID，表示启动实例时希望装载的运行环境。您可以调用[DescribeImages](~~25534~~)查询您可用的镜像资源。如果不指定，默认查询Linux系统镜像的价格。 |
|InstanceType|String|否|ecs.g6.large|实例的资源规格。参数`ResourceType`的值为`instance`时，您必须同时指定该参数。更多详情，请参见[实例规格族](~~25378~~)，也可以调用[DescribeInstanceTypes](~~25620~~)接口获得最新的规格表。 |
|IoOptimized|String|否|optimized|查询的实例是否为I/O优化实例。取值范围：

 -   none：非I/O优化
-   optimized：I/O优化

 当InstanceType为[系列I](~~55263~~)的规格时，默认值为none。

 当InstanceType为非[系列I](~~55263~~)的规格时，默认值为optimized。 |
|InstanceNetworkType|String|否|vpc|实例的网络类型。取值范围：

 -   classic：实例的网络类型为经典网络（Classic）。
-   vpc：实例的网络类型为专有网络（VPC）。

 默认值：vpc |
|InternetChargeType|String|否|PayByTraffic|网络带宽计费方式。取值范围：

 -   PayByBandwidth：按固定带宽计费。
-   PayByTraffic：按带宽流量计费。

 默认值：PayByTraffic |
|InternetMaxBandwidthOut|Integer|否|5|公网出带宽最大值，单位为Mbit/s（Megabit per second）。取值范围：0~100

 默认值：0 |
|SystemDisk.Category|String|否|cloud\_ssd|系统盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘

 参数默认值说明：

 -   当InstanceType为已停售的实例规格，且参数`IoOptimized`取值为`none`时，该参数默认值为`cloud`。
-   其它情况下，该参数默认值为`cloud_efficiency`。 |
|SystemDisk.Size|Integer|否|80|系统盘大小，单位为GiB。取值范围：20~500

 默认值：max\{40, 参数ImageId对应的镜像大小\}

 **说明：** 该参数的取值必须大于或者等于max\{20, ImageSize\}。 |
|SystemDisk.PerformanceLevel|String|否|PL1|系统盘类型为ESSD云盘时，区分性能等级。仅当`SystemDiskCategory=cloud_essd`时该参数有效。取值范围：

 -   PL0
-   PL1（默认）
-   PL2
-   PL3 |
|DataDisk.1.Size|Integer|否|2000|第一块数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800 |
|DataDisk.1.Category|String|否|cloud\_ssd|第一块数据盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|DataDisk.1.PerformanceLevel|String|否|PL1|第一块数据盘类型为ESSD云盘时，区分性能等级。仅当`DataDisk.1.Category=cloud_essd`时该参数有效。取值范围：

 -   PL0
-   PL1（默认）
-   PL2
-   PL3 |
|DataDisk.2.Size|Integer|否|200|第二块数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800 |
|DataDisk.2.Category|String|否|cloud\_ssd|第二块数据盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|DataDisk.2.PerformanceLevel|String|否|PL1|第二块数据盘类型为ESSD云盘时，区分性能等级。仅当`DataDisk.2.Category=cloud_essd`时该参数有效。取值范围：

 -   PL0
-   PL1（默认）
-   PL2
-   PL3 |
|DataDisk.3.Size|Integer|否|2000|第三块数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800 |
|DataDisk.3.Category|String|否|cloud\_ssd|第三块数据盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|DataDisk.3.PerformanceLevel|String|否|PL1|第三块数据盘类型为ESSD云盘时，区分性能等级。仅当`DataDisk.3.Category=cloud_essd`时该参数有效。取值范围：

 -   PL0
-   PL1（默认）
-   PL2
-   PL3 |
|DataDisk.4.Size|Integer|否|2000|第四块数据盘的容量大小，内存单位为GiB。取值范围：

 -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768
-   ephemeral\_ssd：5~800 |
|DataDisk.4.Category|String|否|cloud\_ssd|第四块数据盘的云盘种类。取值范围：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘
-   cloud\_essd：ESSD云盘 |
|DataDisk.4.PerformanceLevel|String|否|PL1|第四块数据盘类型为ESSD云盘时，区分性能等级。仅当`DataDisk.4.Category=cloud_essd`时该参数有效。取值范围：

 -   PL0
-   PL1（默认）
-   PL2
-   PL3 |
|Period|Integer|否|1|云服务器ECS的计费时长。取值范围：

 -   当参数PriceUnit取值为Month时：1~9
-   当参数PriceUnit取值为Year时：1~5
-   当参数PriceUnit取值为Hour时：1
-   当参数PriceUnit取值为Week时：1~4

 默认值：1 |
|PriceUnit|String|否|Year|查询云服务器ECS不同计费周期的价格。取值范围：

 -   Month：按月计费的价格单位。
-   Year：按年计费的价格单位。
-   Hour（默认）：按小时计费的价格单位。
-   Week：按周计费的价格单位。 |
|Amount|Integer|否|1|查询批量购买某种配置的云服务器ECS的价格。取值范围：1~1000

 默认值：1 |
|AssuranceTimes|String|否|Unlimited|弹性保障的总次数。取值：Unlimited，目前仅支持在服务生效期内的无限次模式。

 默认值：Unlimited |
|InstanceTypeList.N|RepeatList|否|ecs.g6.xlarge|实例规格。目前仅支持无限次保障服务设置单个实例规格。 |
|DedicatedHostType|String|否|ddh.c5|专有宿主机的规格。您可以调用[DescribeDedicatedHostTypes](~~134240~~)接口获得最新的专有宿主机规格表。 |
|SpotStrategy|String|否|NoSpot|按量付费实例的抢占策略。取值范围：

 -   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，最高按量付费价格。

 默认值：NoSpot

 **说明：** 当`PriceUnit=Hour`、`Period=1`时，该参数才有效。由于`PriceUnit`默认值为`Hour`，`Period`默认值为`1`，因此您在设置该参数值时，无需设置`PriceUnit`和`Period`参数值。 |
|SpotDuration|Integer|否|1|抢占式实例的保留时长，单位为小时。取值范围：0~6

 -   保留时长2~6正在邀测中，如需开通请提交工单。
-   取值为0，则为无保护期模式。

 默认值：1 |
|ZoneId|String|否|cn-hagzhou-i|可用区ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PriceInfo|Struct| |价格信息类型（Price），包括价格和优惠规则。 |
|Price|Struct| |价格。 |
|Currency|String|CNY|货币单位。 |
|DetailInfos|Array of ResourcePriceModel| |价格的详细信息。

 **说明：** 该返回值正在邀测中，暂未开放使用。 |
|ResourcePriceModel| | | |
|DiscountPrice|Float|655.2|折扣价。 |
|OriginalPrice|Float|4368|原价。 |
|Resource|String|instance|资源名称。 |
|SubRules|Array of Rule| |定价规则子集。 |
|Rule| | | |
|Description|String|买满1年，立享官网价格8.5折优惠|规则子集描述。 |
|RuleId|Long|587|规则ID。 |
|TradePrice|Float|3712.8|成交价。 |
|DiscountPrice|Float|655.2|折扣。 |
|OriginalPrice|Float|4368|原价。 |
|ReservedInstanceHourPrice|Float|1|0预付或部分预付的预留实例券的小时价。 |
|TradePrice|Float|3712.8|最终价，为原价减去折扣。 |
|Rules|Array of Rule| |活动规则。 |
|Rule| | | |
|Description|String|买满1年，立享官网价格8.5折优惠。|活动规则描述。 |
|RuleId|Long|587|活动ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribePrice
&RegionId=cn-hangzhou
&ResourceType=instance
&InstanceType=ecs.g6.large
&ImageId=centos_7_05_64_20G_alibase_20181212.vhd
&InstanceNetworkType=vpc
&InternetChargeType=PayByTraffic
&InternetMaxBandwidthOut=5
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribePriceResponse>
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
</DescribePriceResponse>
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
          "RuleId": "ONE_YEAR_85_PERCENT"
        }
      ]
    }
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidSpotAuthorized|The specified Spot param is unauthorized.|指定的SpotDuration参数值未获得授权。|
|400|InvalidInstanceType.ValueUnauthorized|The specified InstanceType is not authorized.|指定的实例规格未授权使用。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|您指定的实例规格不存在，或者您没有权限操作此规格的实例。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid.|暂不支持指定的网络付费类型的实例，请确认相关参数是否正确。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter "InternetMaxBandwidthOut" is not valid.|指定的InternetMaxBandwidthOut参数不合法。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Category" is not valid.|指定的SystemDisk.Category不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的DataDisk.n.Size超出允许范围，或者快照的容量超过指定磁盘类别的大小限制。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.n.Category" is not valid.|指定的参数DataDisk.n.Category不合法。|
|400|InvalidParameter.Conflict|The specified image does not support the specified instance type.|指定的镜像不能用于指定的实例规格。|
|400|InvalidNetworkType.Mismatch|Specified parameter "InternetChargeType" conflict with instance network type.|实例的网络类型不支持指定的网络计费方式。|
|400|InvalidDiskCategory.Mismatch|The specified disk categories' combination is not supported.|不支持的磁盘种类搭配。|
|400|InvalidIoOptimizedValue.ValueNotSupported|IoOptimized value not supported.|不支持指定的I/O优化值。|
|400|InvalidPeriod|The specified period is not valid.|指定的时段不合法。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter " DataDisk.n.Category " is not valid.|指定的磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter " SystemDisk.Category " is not valid.|指定的系统盘类型无效。|
|400|InstanceDiskCategoryLimitExceed|The specified DataDisk.n.Size beyond the permitted range, or the capacity of snapshot exceeds the size limit of the specified disk category.|指定的DataDisk.n.Size超出允许范围，或者快照的容量超过了指定磁盘类别的大小限制。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified vm bandwidth is not valid.|指定的虚拟机带宽无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter SystemDisk.Category is not valid.|指定的SystemDisk.Category不合法。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter Bandwidth is not valid.|指定的Bandwidth不合法。|
|400|InstanceDiskNumber.LimitExceed|The total number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|400|InvalidDiskCategory.ValueNotSupported|The specified parameter "DiskCategory" is not valid.|指定的SystemDisk.Category参数有误。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|%s|参数InternetMaxBandwidthOut无效。|
|400|InvalidDataDiskCategory.ValueNotSupported|%s|指定的数据磁盘类型无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|%s|当前操作不支持此系统磁盘类型。|
|400|InvalidParameter.Conflict|%s|您输入的参数无效，请检查参数之间是否冲突。|
|400|InvalidInternetChargeType.ValueNotSupported|%s|暂不支持指定的网络计费方式，请确认相关参数是否正确。|
|400|InvalidInstanceType.ValueNotSupported|%s|该操作暂不支持指定的实例类型。|
|400|RegionUnauthorized|%s|该地域未被授权。|
|400|InvalidSystemDiskSize.ValueNotSupported|%s|当前操作不支持设置的系统盘大小。|
|400|InvalidDataDiskSize.ValueNotSupported|%s|指定的数据盘容量无效。|
|400|InvalidSystemDiskCategory.ValueNotSupported|The specified parameter "SystemDisk.Size" is not valid.|指定的SystemDisk.Size不合法。|
|400|InvalidSystemDiskSize.LessThanImageSize|The specified parameter "SystemDisk.Size" is less than the image size.|指定的SystemDisk.Size小于镜像大小。|
|400|InvalidDataDiskCategory.ValueNotSupported|The specified parameter "DataDisk.Category" is not valid.|指定的参数DataDisk.Category不合法。|
|400|InvalidDataDiskSize.ValueNotSupported|The specified parameter "DataDisk.Size" is not valid.|指定的参数DataDisk.Size不合法。|
|400|Throttling|Request was denied due to request throttling.|当前的操作太过频繁，请稍后重试。|
|400|PriceNotFound|The price of your queried resource is not available now, please try other resources.|未找到价格，请修改相应的参数值重试。|
|400|InvalidResourceType.ValueNotSupported|The specified parameter ResourceType is not valid.|指定的资源类型不合法。|
|400|InvalidPriceUnit.ValueNotSupported|The specified parameter PriceUnit is not valid.|指定的单价不合法。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified parameter InternetMaxBandwidthOut is not valid.|指定的公网出带宽最大值不合法。|
|400|EncryptedOption.Conflict|%s|参数不支持（加密盘）。|
|403|ImageNotSubscribed|The specified image has not be subscribed.|指定的镜像未在镜像市场订阅。|
|403|OperationDenied|The specified Image is disabled or is deleted.|指定的镜像被禁用或被删除。|
|403|InvalidSystemDiskCategory.ValueUnauthorized|The disk category is not authorized.|该磁盘类别未经授权。|
|403|InstanceDiskCategoryLimitExceed|The total size of specified disk category in an instance exceeds.|磁盘种类总容量超过实例限制。|
|403|ImageRemovedInMarket|The specified market image is not available, Or the specified user defined image includes product code because it is based on an image subscribed from marketplace, and that image in marketplace includeing exact the same product code has been removed.|指定的市场镜像不可用，或者指定的用户定义镜像包含产品代码，因为它基于从市场订购的镜像，并且市场中包含完全相同的产品代码的镜像已被删除。|
|403|QuotaExceed.PortableCloudDisk|The quota of portable cloud disk exceeds.|可卸载磁盘数量已达上限。|
|403|Forbbiden|User not authorized to operate on the specified resource.|用户未被授权操作指定的资源。|
|403|InstanceDiskNumLimitExceed|The number of specified disk in an instance exceeds.|实例下磁盘数目超过限制。|
|403|IoOptimized.NotSupported|The specified image is not support IoOptimized Instance.|指定的镜像不支持I/O优化型实例。|
|403|ImageNotSupportInstanceType|The specified image don't support the InstanceType instance.|指定的镜像不支持此类实例规格。|
|403|InvalidDiskSize.TooSmall|Specified disk size is less than the size of snapshot|指定的磁盘容量小于快照容量。|
|403|OperationDenied|The type of the disk does not support the operation|此磁盘种类不支持指定的操作。|
|403|InvalidDiskCategory.Mismatch|The specified disk categories combination is not supported.|不支持的磁盘种类搭配。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not support the specified instance type.|指定的磁盘种类不支持该实例规格。|
|403|InvalidDiskCategory.NotSupported|The upgrade operation of instance does not support this category of disk.|实例的升级操作不支持此类磁盘。|
|403|InvalidParameter.ResourceOwnerAccount|ResourceOwnerAccount is Invalid.|指定的ResourceOwnerAccount不合法。|
|403|RegionUnauthorized|There is no authority to create instance in the specified region.|用户未被授权在指定的地域创建实例。|
|403|OperationDenied|The resource is out of usage.|该实例不在运行状态，请您启动实例或检查操作是否合理。|
|403|InstanceType.Offline|%s|实例规格因停售、供货不足等原因，不支持该操作。|
|403|OperationDenied|The specified parameter InstanceNetworkType is not authorized.|用户未被授权指定的实例网络类型。|
|403|InvalidAmount.Malformed|The specified parameter Amount is not valid.|参数Amount格式错误。|
|403|InvalidDiskSize.TooSmall|Specified system disk size is less than the size of image|指定的系统盘容量小于此镜像的大小。|
|403|InvalidChargeType.MarketImage|The specified chargeType of marketplace image is invalid|该市场镜像的付费类型无效。|
|403|InvalidDiskIds.NotFound|Some of the specified disks do not exist.|指定的磁盘不存在。|
|403|InvalidDiskCategory.NotSupported|The specified disk category is not supported.|指定的云盘类型不支持当前操作。|
|403|PrePaidInstance.Expired|The prePaid instance has expired.|包年包月实例已到期。|
|403|InvalidAction.Unauthorized|The specified action is not valid.|指定的操作无效。|
|404|InvalidImageId.NotFound|The specified ImageId does not exist.|指定的镜像在该用户账号下不存在，请您检查镜像ID是否正确。|
|404|IoOptimized.NotSupported|The specified instancetype is not support IoOptimized instance|指定的实例规格不支持I/O优化。|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例计费方式不存在。|
|404|DependencyViolation.IoOptimized|The specified instancetype must be IoOptimized instance.|指定的实例规格必须为I/O优化实例，请您检查实例规格是否正确。|
|404|InvalidSystemDiskSize.LessThanImageSize|The specified parameter SystemDisk.Size is less than the image size.|指定的参数SystemDisk.Size小于镜像文件大小数值。|
|404|InvalidSystemDiskSize.LessThanMinSize|The specified parameter SystemDisk.Size is less than the minimum size.|指定的SystemDisk.Size低于最小值。|
|404|InvalidSystemDiskSize.MoreThanMaxSize|The specified parameter SystemDisk.Size is more than the maximum size|指定的SystemDisk.Size超过最大值。|
|404|InvalidSystemDiskSize.ValueNotSupported|The specified parameter SystemDisk.Size is invalid.|指定的SystemDisk.Size不合法。|
|404|InvalidInstanceType.Missing|The InstanceType parameter that is mandatory for processing the request is not provided.|InstanceType参数为必填参数。|
|404|InvalidNetworkType.ValueNotSupported|The specified parameter NetworkType is not valid.|指定的网络类型不合法。|
|404|InvalidDiskCategory.Missing|The DataDisk.1.Category parameter that is mandatory for processing the request is not provided.|没有指定数据盘类型。|
|404|Invalid.InstanceId.NotFound|The Instance provided does not exist.|指定的实例不存在。|
|404|InvalidMarketImage.NotFound|The specified marketplace image does not exist, please change the imageId and try again.|指定的市场镜像不存在，请更改参数后重试。|
|404|InvalidDiskIds.NotPortable|The specified DiskId is not portable.|指定的磁盘是不可移植的。|
|404|InvalidSystemDisk.NotFound|The specified system disk does not exist.|指定的系统盘不存在。|
|404|InvalidResourceGroup.NotFound|The ResourceGroup provided does not exist in our records.|资源组并不在记录中。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|500|InternalError|%s|内部错误。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

