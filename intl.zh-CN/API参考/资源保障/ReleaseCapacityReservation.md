# ReleaseCapacityReservation

调用ReleaseCapacityReservation释放容量预定服务。

## 接口说明

立即生效的容量预定服务，当释放方式为手动释放时，调用该接口可直接释放容量预定服务。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=ReleaseCapacityReservation&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ReleaseCapacityReservation|系统规定参数。取值：ReleaseCapacityReservation |
|PrivatePoolOptions.Id|String|是|crp-bp67acfmxazb4\*\*\*\*|容量预定服务ID。 |
|RegionId|String|是|cn-hangzhou|容量预定服务所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DryRun|Boolean|否|false|是否对此次请求进行检索。取值：false，目前仅支持不检索本次请求，直接释放容量预定服务。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=ReleaseCapacityReservation
&RegionId=cn-hangzhou
&PrivatePoolOptions.Id=crp-bp67acfmxazb4****
&DryRun=false
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<ReleaseCapacityReservationResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ReleaseCapacityReservationResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter.RegionId|The specified RegionId should not be null.|RegionId是必选参数。|
|500|InternalError|The request processing has failed due to some unknown error, exception or failure.|内部错误，请重试。如果多次尝试失败，请提交工单。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

