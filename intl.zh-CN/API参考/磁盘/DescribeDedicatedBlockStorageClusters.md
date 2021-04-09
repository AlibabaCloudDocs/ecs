# DescribeDedicatedBlockStorageClusters

调用DescribeDedicatedBlockStorageClusters查询已创建的专属块存储集群列表。

## 接口说明

请求参数的作用类似于一个过滤器，过滤器为逻辑与（AND）关系。如果某一参数为空，则过滤器不起作用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDedicatedBlockStorageClusters&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDedicatedBlockStorageClusters|系统规定参数。取值：DescribeDedicatedBlockStorageClusters |
|RegionId|String|是|cn-hangzhou|集群所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ZoneId|String|否|cn-hangzhou-h|集群所属可用区ID，您可以调用[DescribeZones](~~25610~~)获取可用区列表。 |
|DedicatedBlockStorageClusterId.N|RepeatList|否|dbsc-bp12wlf6am0v\*\*\*\*|专属块存储集群ID。

 如果想要查询指定的一个或多个集群的信息，需要设置此参数。例如：您想要查询`dbsc-bp12wlf6am0v****`和`dbsc-bp12wlf6abcd****`两个集群的信息，参数设置如下：

 ```

&DedicatedBlockStorageClusterId.1=dbsc-bp12wlf6am0v****
&DedicatedBlockStorageClusterId.2=dbsc-bp12wlf6abcd****

``` |
|Status.N|RepeatList|否|Running|专属块存储集群的状态。取值如下：

 -   Preparing：待交付
-   Running：运行中
-   Expired：集群到期
-   Offline：下线

 N的取值范围：1~4

 如果想要查询指定状态的集群信息，需要设置此参数。例如，您需要查询待交付和运行中的集群信息，参数设置如下：

 ```

&Status.1=Preparing
&Status.2=Running

``` |
|Category|String|否|cloud\_essd|云盘类型。当前仅支持cloud\_essd，即ESSD云盘。 |
|NextToken|String|否|AAAAAdDWBF2|查询凭证（Token）。

 通过`NextToken`设置查询凭证（Token），其取值是上一次调用DescribeDedicatedBlockStorageClusters返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数。 |
|MaxResults|Integer|否|10|返回的最大数。取值范围：1~500

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DedicatedBlockStorageClusters|Array of DedicatedBlockStorageCluster| |由一个或多个集群组成的数组。 |
|DedicatedBlockStorageCluster| | | |
|Category|String|cloud\_essd|云盘类型。当前仅支持cloud\_essd，即ESSD云盘。 |
|CreateTime|String|2021-03-06 10:16:34|专属块存储集群创建时间。 |
|DedicatedBlockStorageClusterCapacity|Struct| |专属块存储集群的存储容量信息。 |
|AvailableCapacity|Long|40|当前集群可用的容量，单位为TB。 |
|TotalCapacity|Long|72|当前集群总容量，单位为TB。 |
|DedicatedBlockStorageClusterId|String|dbsc-xxxxxx|专属块存储集群ID。 |
|DedicatedBlockStorageClusterName|String|myDBSCCluster|专属块存储集群名称。 |
|Description|String|myDBSCCluster|专属块存储集群的描述信息。 |
|ExpiredTime|String|2022-03-06 10:16:34|专属块存储集群到期时间。 |
|PerformanceLevel|String|PL1|ESSD云盘的性能级别。当前仅支持PL1。

 有关ESSD PL1的性能参数，请参见[ESSD云盘](~~122389~~)。 |
|Status|String|Running|专属块存储集群的状态。取值如下：

 -   Preparing：待交付
-   Running：运行中
-   Expired：集群到期
-   Offline：下线

 N的取值范围：1~4 |
|ZoneId|String|cn-hangzhou-h|集群所属可用区ID。 |
|NextToken|String|AAAAAdDWBF2|本次调用返回的查询凭证值。 |
|RequestId|String|11B55F58-D3A4-4A9B-9596-342420D02FF8|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDedicatedBlockStorageClusters
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeDedicatedBlockStorageClustersResponse>
      <DedicatedBlockStorageClusters>
            <DedicatedBlockStorageCluster>
                  <Status>Running</Status>
                  <Description>myDBSCCluster</Description>
                  <ZoneId>cn-hangzhou-h</ZoneId>
                  <DedicatedBlockStorageClusterId>dbsc-xxxxxx</DedicatedBlockStorageClusterId>
                  <PerformanceLevel>PL1</PerformanceLevel>
                  <CreateTime>2021-03-06 10:16:34</CreateTime>
                  <ExpiredTime>2022-03-06 10:16:34</ExpiredTime>
                  <Category>cloud_essd</Category>
                  <DedicatedBlockStorageClusterName>myDBSCCluster</DedicatedBlockStorageClusterName>
                  <DedicatedBlockStorageClusterCapacity>
                        <AvailableCapacity>40</AvailableCapacity>
                        <TotalCapacity>72</TotalCapacity>
                  </DedicatedBlockStorageClusterCapacity>
            </DedicatedBlockStorageCluster>
      </DedicatedBlockStorageClusters>
      <NextToken>AAAAAdDWBF2</NextToken>
      <RequestId>11B55F58-D3A4-4A9B-9596-342420D02FF8</RequestId>
</DescribeDedicatedBlockStorageClustersResponse>
```

`JSON`格式

```
{
	"DedicatedBlockStorageClusters": {
		"DedicatedBlockStorageCluster": [{
			"Status": "Running",
			"Description": "myDBSCCluster",
			"ZoneId": "cn-hangzhou-h",
			"DedicatedBlockStorageClusterId": "dbsc-xxxxxx",
			"PerformanceLevel": "PL1",
			"CreateTime": "2021-03-06 10:16:34",
			"ExpiredTime": "2022-03-06 10:16:34",
			"Category": "cloud_essd",
			"DedicatedBlockStorageClusterName": "myDBSCCluster",
			"DedicatedBlockStorageClusterCapacity": {
				"AvailableCapacity": "40",
				"TotalCapacity": "72"
			}
		}]
	},
	"NextToken": "AAAAAdDWBF2",
	"RequestId": "11B55F58-D3A4-4A9B-9596-342420D02FF8"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidStatus.ValueNotSupported|%s|该资源当前的状态不支持此操作。|
|404|InvalidRegionId.NotFound|The specified region does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidZoneId.NotFound|The specified zone does not exist.|指定的可用区ID不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

