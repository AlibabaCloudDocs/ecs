# CancelImagePipelineExecution

调用CancelImagePipelineExecution取消一个镜像构建任务。

## 接口说明

调用该接口前，请确认需要取消的镜像构建任务处于构建中（BUILDING）、分发中（DISTRIBUTING）或资源回收中（RELEASING）的状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=CancelImagePipelineExecution&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CancelImagePipelineExecution|系统规定参数。取值：CancelImagePipelineExecution |
|ExecutionId|String|是|exec-5fb8facb8ed7427c\*\*\*\*|构建任务ID。 |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=CancelImagePipelineExecution
&ExecutionId=exec-5fb8facb8ed7427c****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<CancelImagePipelineExecutionResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</CancelImagePipelineExecutionResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

