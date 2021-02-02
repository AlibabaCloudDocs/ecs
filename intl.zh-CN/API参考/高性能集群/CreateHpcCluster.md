# CreateHpcCluster

调用CreateHpcCluster创建一个HPC集群。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateHpcCluster&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateHpcCluster|系统规定参数。取值：CreateHpcCluster |
|Name|String|是|hpc-Cluster-01|HPC集群名称。长度为2~128个英文或中文字符。必须以大小字母或中文开头，不能以`http://`和`https://`开头。可以包含数字、英文句号（.）、下划线（\_）或者短划线（-）。 |
|RegionId|String|是|cn-hangzhou|HPC集群所在的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多信息，请参见[如何保证幂等性](~~25693~~)。 |
|Description|String|否|testHPCDescription|HPC集群描述。长度为2~256个英文或中文字符，不能以`http://`和`https://`开头。

 默认值：空 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|HpcClusterId|String|hpc-pnlg1ds9rky4\*\*\*\*|集群ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateHpcCluster
&RegionId=cn-hangzhou
&Name=hpc-Cluster-01
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateHpcClusterResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <HpcClusterId>hpc-pnlg1ds9rky4****</HpcClusterId>
</CreateHpcClusterResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "HpcClusterId": "hpc-pnlg1ds9rky4****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|参数RegionId不得为空。|
|400|InvalidHpcClusterName.Malformed|Specified hpc cluster name is not valid.|指定的HPC集群名称无效。|
|400|InvalidHpcClusterDescription.Malformed|The specified parameter Description is not valid.|指定的HPC集群描述无效。|
|404|InvalidRegionId.NotFound|The specified parameter "RegionId" is not valid.|指定的RegionId不存在，请您检查此产品在该地域是否可用。|
|404|InternalError|Failed to create hpc cluster|HPC集群创建失败。|
|400|Invalid.Parameter|Invalid parameters|参数无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

