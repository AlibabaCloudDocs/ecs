# DescribeDiskReplicaPairs

调用DescribeDiskReplicaPairs查询复制关系列表。

## 接口说明

在查询结果中，您可以查看当前地域中所有的复制关系，支持查看当前地域的所有主盘和从盘。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDiskReplicaPairs&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDiskReplicaPairs|系统规定参数。取值：DescribeDiskReplicaPairs |
|RegionId|String|是|cn-beijing|云盘（主盘或从盘）所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|MaxResults|Integer|否|50|分页查询时每页行数。取值范围：1~500

 默认值：10。 |
|NextToken|String|否|AAAAAdDWBF2\*\*\*\*|查询凭证（Token）。

 通过`NextToken`设置查询凭证（Token），其取值是上一次调用`DescribeDiskReplicaPairs`返回的`NextToken`参数值，再通过`MaxResults`设置单页查询的最大条目数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskReplicaPairs|Array of DiskReplicaPair| |复制关系信息组成的集合。 |
|DiskReplicaPair| | | |
|Description|String|TestReplicaPairDescription|复制关系的描述信息。 |
|DestinationDiskId|String|d-asdfjl2342kj2l3k4\*\*\*\*|从盘的云盘ID。 |
|DestinationRegion|String|cn-shanghai|从盘所属地域。 |
|PairName|String|TestReplicaPair|复制关系名称。 |
|ReplicaPairId|String|rp-dsaf233kj23j2j35\*\*\*\*|复制关系ID。 |
|SourceDiskId|String|d-bp131n0q38u3a4zi\*\*\*\*|主盘的云盘ID。 |
|SourceRegion|String|cn-beijing|主盘所属地域。 |
|Status|String|active|复制关系的状态。取值如下：

 -   inactive：待激活
-   active：激活
-   paused：暂停
-   pausing：暂停中
-   starting：启动中
-   deleting：删除中 |
|NextToken|String|AAAAAdDWBF2\*\*\*\*|本次调用返回的查询凭证值。 |
|RequestId|String|E69EF3CC-94CD-42E7-8926-F133B86387C0|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDiskReplicaPairs
&RegionId=cn-beijing
&MaxResults=50
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeDiskReplicaPairsResponse>
      <NextToken>AAAAAdDWBF2****</NextToken>
      <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
      <DiskReplicaPairs>
            <DiskReplicaPair>
                  <Status>active</Status>
                  <Description>TestReplicaPairDescription</Description>
                  <DestinationDiskId>d-asdfjl2342kj2l3k4****</DestinationDiskId>
                  <PairName>TestReplicaPair</PairName>
                  <DestinationRegion>cn-shanghai</DestinationRegion>
                  <ReplicaPairId>rp-dsaf233kj23j2j35****</ReplicaPairId>
                  <SourceRegion>cn-beijing</SourceRegion>
                  <SourceDiskId>d-bp131n0q38u3a4zi****</SourceDiskId>
            </DiskReplicaPair>
      </DiskReplicaPairs>
</DescribeDiskReplicaPairsResponse>
```

`JSON`格式

```
{
	"NextToken": "AAAAAdDWBF2****",
	"RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"DiskReplicaPairs": {
		"DiskReplicaPair": [{
			"Status": "active",
			"Description": "TestReplicaPairDescription",
			"DestinationDiskId": "d-asdfjl2342kj2l3k4****",
			"PairName": "TestReplicaPair",
			"DestinationRegion": "cn-shanghai",
			"ReplicaPairId": "rp-dsaf233kj23j2j35****",
			"SourceRegion": "cn-beijing",
			"SourceDiskId": "d-bp131n0q38u3a4zi****"
		}]
	}
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|
|400|InvalidParamter|Some parameters are invalid in this request.|请求中包含非法参数。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

