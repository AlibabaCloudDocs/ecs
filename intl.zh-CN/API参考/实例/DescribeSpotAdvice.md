# DescribeSpotAdvice

调用DescribeSpotAdvice查询指定地域下，抢占式实例近30天的实例平均释放率、平均折扣率等信息。

## 接口说明

-   您可以通过该接口查询抢占式实例近30天的信息，便于您合理选择抢占式实例的实例规格。支持查询的信息包括：
    -   实例平均释放率。
    -   实例平均折扣率。
    -   通过折扣率计算出的平均价格。
-   仅支持查询专有网络VPC、I/O优化的抢占式实例。
-   您可以通过以下任一方式查询抢占式实例近30天的信息：
    -   设置`Cores`、`Memory`两参数或`MinCores`、`MinMemory`两参数，查询符合vCPU及内存要求的实例规格信息。
    -   设置`InstanceTypes.N`查询指定的实例规格信息。
    -   设置`Cores`、`Memory`两参数或`MinCores`、`MinMemory`两参数后，再设置`InstanceTypeFamily`或`InstanceFamilyLevel`，查询某一实例规格族或某一级别内，符合vCPU及内存要求的实例规格信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSpotAdvice&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|否|DescribeSpotAdvice|系统规定参数。取值：DescribeSpotAdvice |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Cores|Integer|否|2|实例规格的vCPU数量。取值请参见[实例规格族](~~25378~~)。 |
|Memory|Float|否|8.0|实例规格的内存大小。单位：GiB。取值请参见[实例规格族](~~25378~~)。 |
|MinCores|Integer|否|2|实例规格的vCPU数量的最小值。取值请参见[实例规格族](~~25378~~)。 |
|MinMemory|Float|否|8.0|实例规格的内存大小的最小值。取值请参见[实例规格族](~~25378~~)。 |
|ZoneId|String|否|cn-hangzhou-i|可用区ID。

 默认值：无，即查询指定地域下的所有可用区。 |
|InstanceTypes.N|RepeatList|否|ecs.c5.large|实例规格。N的取值范围：1~10。取值请参见[实例规格族](~~25378~~)。 |
|InstanceTypeFamily|String|否|ecs.c5|实例规格族。取值请参见[实例规格族](~~25378~~)。 |
|InstanceFamilyLevel|String|否|EntryLevel|实例规格族级别。取值范围：

 -   EntryLevel：入门级。
-   EnterpriseLevel：企业级。
-   CreditEntryLevel：积分入门级。更多信息，请参见[突发性能实例](~~59977~~)。

 默认值：无，即查询所有级别。 |
|GpuSpec|String|否|NVIDIA T4|GPU计算卡的类型。取值范围：

 -   NVIDIA P4
-   NVIDIA T4
-   NVIDIA P100
-   NVIDIA V100
-   NVIDIA A100

 默认值：无，即查询所有类型。更多信息，请参见[GPU计算型实例概述](~~108496~~)。 |
|GpuAmount|Integer|否|2|GPU实例对应的GPU数量。取值请参见[GPU计算型实例概述](~~108496~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AvailableSpotZones|Array of AvailableSpotZone| |可用区及其对应的抢占式实例相关信息组成的数组。

 **说明：** 返回值的顺序按照实例规格的历史平均折扣率排序。 |
|AvailableSpotZone| | | |
|AvailableSpotResources|Array of AvailableSpotResource| |近30天抢占式实例的释放率、折扣率等信息组成的数组。 |
|AvailableSpotResource| | | |
|AverageSpotDiscount|Integer|20|近30天抢占式实例的均价相比按量付费实例价格的折扣率。单位：%。可能值：1~100。

 您可以根据该返回值计算抢占式实例的均价。例如，按量付费实例的价格为1，该返回值为20（即20%），则近30天抢占式实例的均价为0.2。 |
|InstanceType|String|ecs.c5.large|实例规格。 |
|InterruptRateDesc|String|0-3%|近30天抢占式实例的释放率的范围，对应`InterruptionRate`返回值。可能值：

 -   0-3%
-   3-5%
-   5-10%
-   10-100% |
|InterruptionRate|Float|0|近30天抢占式实例的平均释放率。单位：% |
|ZoneId|String|cn-hangzhou-i|可用区ID。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeSpotAdvice
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-i
&InstanceTypes.1=ecs.c5.large
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeSpotAdviceResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <AvailableSpotZones>
            <AvailableSpotZone>
                  <ZoneId>cn-hangzhou-i</ZoneId>
            </AvailableSpotZone>
            <AvailableSpotZone>
                  <AvailableSpotResources>
                        <AvailableSpotResource>
                              <InterruptRateDesc>0-3%</InterruptRateDesc>
                              <InstanceType>ecs.c5.large</InstanceType>
                              <AverageSpotDiscount>20</AverageSpotDiscount>
                              <InterruptionRate>0</InterruptionRate>
                        </AvailableSpotResource>
                  </AvailableSpotResources>
            </AvailableSpotZone>
      </AvailableSpotZones>
      <RegionId>cn-hangzhou</RegionId>
</DescribeSpotAdviceResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "AvailableSpotZones": {
        "AvailableSpotZone": [
            {
                "ZoneId": "cn-hangzhou-i"
            }, 
            {
                "AvailableSpotResources": {
                    "AvailableSpotResource": [
                        {
                            "InterruptRateDesc": "0-3%", 
                            "InstanceType": "ecs.c5.large", 
                            "AverageSpotDiscount": "20", 
                            "InterruptionRate": "0"
                        }
                    ]
                }
            }
        ]
    }, 
    "RegionId": "cn-hangzhou"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Invalid.RegionId|The specified RegionId does not exist.|地域参数无效。|
|404|Unavailable.Regions|The available regions does not exists|地域参数无效。|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|目标资源类型无效。|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|资源类型无效。|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|指定的目标资源无效。|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|指定的参数IoOptimized无效。|
|404|Invalid.NetworkType|The specified NetworkType is not valid.|指定的参数NetworkType无效。|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist in our records.|指定的宿主机在当前地域中不存在。|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|参数“InstanceType”、“Cores”、“Memory”不能同时为空。|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|指定的RegionId不合法。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

