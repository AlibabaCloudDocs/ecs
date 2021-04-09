# CreateDedicatedBlockStorageCluster

调用CreateDedicatedBlockStorageCluster创建专属存储集群。

## 接口说明

专属块存储集群（Dedicated Block Storage Cluster）是一种物理隔离、用户独占整个块存储集群的块存储服务。更多信息，请参见[什么是专属块存储集群](~~208883~~)。

专属块存储集群上创建的云盘只能挂载到同可用区的ECS实例上。您在创建专属块存储集群前，需要规划好地域和可用区。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateDedicatedBlockStorageCluster&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDedicatedBlockStorageCluster|系统规定参数。取值：CreateDedicatedBlockStorageCluster |
|Capacity|Integer|是|72|专属集群容量。单位为TB，取值范围：72 ~ 2304 |
|Category|String|是|cloud\_essd|专属块存储集群可创建的云盘类型。当前仅支持cloud\_essd，即ESSD云盘。 |
|RegionId|String|是|cn-hangzhou|集群所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|是|cn-hangzhou-h|集群所属可用区ID，您可以调用[DescribeZones](~~25610~~)获取可用区列表。 |
|DedicatedBlockStorageClusterName|String|否|myDBSCCluster|专属块存储集群名称。 |
|Description|String|否|myDBSCCluster|专属块存储集群的描述信息。 |
|PerformanceLevel|String|否|PL1|ESSD云盘的性能级别。当前仅支持PL1。

 有关ESSD PL1的性能参数，请参见[ESSD云盘](~~122389~~)。 |
|Period|Integer|否|2|购买集群的时长，单位由`PeriodUnit`指定。

 -   当`PeriodUnit`=`Year`时，`Period`取值：\{"1", "2", "3", "4"\}。
-   当`PeriodUnit`=`Month`时，`Period`取值：\{"6", "7", "8", "9", "10", "11"\}。

 默认值：6 |
|PeriodUnit|String|否|Year|购买集群的时长单位。取值如下：

 -   Year：年
-   Month：月

 默认值：Month |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。

 `ClientToken`只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DedicatedBlockStorageClusterId|String|dbsc-xxxxx|专属块存储集群ID。 |
|DedicatedBlockStorageClusterOrderId|String|50155660025\*\*\*\*|支付订单ID。 |
|RequestId|String|20758A-585D-4A41-A9B2-28DA8F4F534F|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateDedicatedBlockStorageCluster
&Capacity=72
&Category=cloud_essd
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-h
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateDedicatedBlockStorageClusterResponse>
      <DedicatedBlockStorageClusterOrderId>50155660025****</DedicatedBlockStorageClusterOrderId>
      <RequestId>20758A-585D-4A41-A9B2-28DA8F4F534F</RequestId>
      <DedicatedBlockStorageClusterId>dbsc-xxxxx</DedicatedBlockStorageClusterId>
</CreateDedicatedBlockStorageClusterResponse>
```

`JSON`格式

```
{
	"DedicatedBlockStorageClusterOrderId": "50155660025****",
	"RequestId": "20758A-585D-4A41-A9B2-28DA8F4F534F",
	"DedicatedBlockStorageClusterId": "dbsc-xxxxx"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|指定的可用区ID不存在。|
|404|InvalidRegionId.NotFound|The specified region does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

