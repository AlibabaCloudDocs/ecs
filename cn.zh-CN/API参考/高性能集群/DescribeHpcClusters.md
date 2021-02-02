# DescribeHpcClusters

调用DescribeHpcClusters查询您可用的HPC集群。请求参数作为筛选器（Filter）使用，筛选关系为逻辑与关系，参数之间无依赖关系。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeHpcClusters&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeHpcClusters|系统规定参数。取值：DescribeHpcClusters |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |
|HpcClusterIds|String|否|\["hpc-xxxxxxxxx", "hpc-yyyyyyyyy", … "hpc-zzzzzzzzz"\]|HPC集群ID。

 取值可以由多个HPC集群ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。 |
|PageNumber|Integer|否|1|HPC集群列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|HpcClusters|Array of HpcCluster| |由HpcCluster组成的数组格式，返回HPC集群的信息。 |
|HpcCluster| | | |
|Description|String|testDescription|HPC集群的描述。 |
|HpcClusterId|String|hpc-bp1a5zr3u7nq9cx\*\*\*\*|HPC集群ID。 |
|Name|String|testName|HPC集群的名称。 |
|PageNumber|Integer|1|HPC集群列表的页码。 |
|PageSize|Integer|10|输入时设置的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|2|HPC集群总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeHpcClusters
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeHpcClustersResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>2</TotalCount>
      <HpcClusters>
            <HpcCluster>
                  <Name>chuatest1</Name>
                  <Description>testDescription1</Description>
                  <HpcClusterId>hpc-bp1a5zr3u7nq9cx****</HpcClusterId>
            </HpcCluster>
            <HpcCluster>
                  <Name>chuatest2</Name>
                  <Description>testDescription2</Description>
                  <HpcClusterId>hpc-l6aam7fivcfd21fu****</HpcClusterId>
            </HpcCluster>
      </HpcClusters>
      <PageSize>10</PageSize>
      <RequestId>382960A6-C535-4705-B6EA-8338466270C4</RequestId>
</DescribeHpcClustersResponse>
```

`JSON`格式

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "HpcClusters": {
        "HpcCluster": [
            {
                "Name": "chuatest1",
                "Description": "testDescription1",
                "HpcClusterId": "hpc-bp1a5zr3u7nq9cx****"
            },
            {
                "Name": "chuatest2",
                "Description": "testDescription2",
                "HpcClusterId": "hpc-l6aam7fivcfd21fu****"
            }
        ]
    },
    "PageSize": 10,
    "RequestId": "382960A6-C535-4705-B6EA-8338466270C4"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|指定的RegionId不存在，请您检查此产品在该地域是否可用。|
|400|MissingParameter.HpcClusterId|The input parameter HpcClusterId that is mandatory for processing this request is not supplied.|参数HpcClusterId不能为空。|
|400|InvalidHpcClusterIds.ExceedLimit|The amount of specified specified hpc cluster ids exceeds the limit.|参数HpcClusterIds中的数据量不在规定的范围内。|
|400|InvalidHpcClusterIds.Malformed|The amount of specified specified hpc cluster ids is invalid.|参数HpcClusterIds中的数据量不在规定的范围内。|
|400|Invalid.Parameter|Invalid parameters.|参数无效。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

