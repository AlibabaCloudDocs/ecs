# StartDiskReplicaPair

调用StartDiskReplicaPair启动一个复制关系并开始云盘数据同步流程。

## 接口说明

复制关系只有在待激活（`inactive`）或暂停（`paused`）状态时，您才能启动。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=StartDiskReplicaPair&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|StartDiskReplicaPair|系统规定参数。取值：StartDiskReplicaPair |
|RegionId|String|是|cn-beijing|源云盘所属地域。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ReplicaPairId|String|是|rp-dsaf233kj23j2j35\*\*\*\*|复制关系ID。您可以调用[DescribeDiskReplicaPairs](~~209201~~)查询复制关系ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|E69EF3CC-94CD-42E7-8926-F133B86387C0|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=StartDiskReplicaPair
&RegionId=cn-beijing
&ReplicaPairId=rp-dsaf233kj23j2j35****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<StartDiskReplicaPairResponse>
        <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</StartDiskReplicaPairResponse>
```

`JSON`格式

```
{
    "RequestId": "E69EF3CC-94CD-42E7-8926-F133B86387C0"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单。|
|400|InvalidRegionId.MalFormed|The specified parameter RegionId is not valid.|指定的RegionId不合法。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

