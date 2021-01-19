# DeleteImagePipeline

调用DeleteImagePipeline删除一个镜像模板。

## 接口说明

如果存在构建中（BUILDING）、分发中（DISTRIBUTING）、资源回收中（RELEASING）或取消中（CANCELLING）的构建任务，则不允许直接删除模板，需要等待构建任务成功（SUCCESS）、失败（FAILED）或已取消（CANCELLED）。构建任务的详细信息可以通过DescribeImagePipelineExecutions查询。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeleteImagePipeline&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteImagePipeline|系统规定参数。取值：DeleteImagePipeline |
|ImagePipelineId|String|是|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeleteImagePipeline
&ImagePipelineId=ip-2ze5tsl5bp6nf2b3****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeleteImagePipelineResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteImagePipelineResponse>
```

`JSON`格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

