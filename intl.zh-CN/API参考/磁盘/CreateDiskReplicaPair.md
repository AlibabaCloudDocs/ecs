# CreateDiskReplicaPair

调用CreateDiskReplicaPair创建云盘异步复制关系。

## 接口说明

云盘异步复制功能，是将一个云盘上的数据异步复制到另外一个地域的云盘，可在主盘（即源云盘）异常时提供数据保护，从而减少或避免数据丢失，为关键数据制定业务连续性计划。更多信息，请参见[什么是云盘异步复制](~~208904~~)。

如果需要使用云盘异步复制功能同步云盘的数据，您首先需要调用CreateDiskReplicaPair创建云盘复制关系，再调用[StartDiskReplicaPair](~~209199~~)启动复制关系。

在创建云盘异步复制关系前，您需要先在目标地域创建一个和主盘具有相同规格和容量的云盘。您可以调用[DescribeDisks](~~25514~~)查询主盘的规格和容量，再调用[CreateDisk](~~25513~~)在目标地域创建相同规格和容量的从盘。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CreateDiskReplicaPair&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateDiskReplicaPair|系统规定参数。取值：CreateDiskReplicaPair |
|DestinationDiskId|String|是|d-asdfjl2342kj2l3k4\*\*\*\*|从盘的云盘ID。 |
|DestinationRegionId|String|是|cn-shanghai|从盘所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DiskId|String|是|d-bp131n0q38u3a4zi\*\*\*\*|主盘的云盘ID。 |
|PairName|String|是|TestReplicaPair|复制关系名称。 |
|RegionId|String|是|cn-beijing|主盘所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|Description|String|否|TestReplicaPairDescription|复制关系的描述信息。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PairId|String|rp-dsaf233kj23j2j35\*\*\*\*|复制关系ID。 |
|RequestId|String|20758A-585D-4A41-A9B2-28DA8F4F534F|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CreateDiskReplicaPair
&DiskId=d-bp1famypsnar20bv****
&PairName=TestReplicaPair
&RegionId=cn-beijing
&DestinationRegionId=cn-shanghai
&DestinationDiskId=d-asdfjl2342kj2l3k4****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<CreateDiskReplicaPairResponse>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
        <PairId>rp-dsaf233kj23j2j3****</PairId>
</CreateDiskReplicaPairResponse>
```

`JSON`格式

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0",
    "PairId": "rp-dsaf233kj23j2j3****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidDiskId.NotFound|The specified disk does not exist.|指定的磁盘不存在。请您检查磁盘ID是否正确。|
|403|IncorrectDiskStatus|The operation is not supported in this status.|当前的磁盘不支持此操作，请您确认磁盘处于正常使用状态，是否欠费。|
|400|IncompleteParamter|Some fields can not be null in this request.|请求中缺失参数。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

