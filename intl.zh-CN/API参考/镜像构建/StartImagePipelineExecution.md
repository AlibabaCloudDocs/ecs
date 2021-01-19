# StartImagePipelineExecution

调用StartImagePipelineExecution通过一个镜像模板执行构建镜像的任务。

## 接口说明

-   镜像模板创建好之后，需要通过该接口执行构建镜像的任务，系统将根据镜像模板设置好的参数进行构建、分发、共享镜像。
-   同一个镜像模板，同一时间只能执行一个构建镜像任务。取消构建镜像任务（CancelImagePipelineExecution）可同时执行多次，并且取消构建镜像任务和构建镜像任务之间互不干扰。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=StartImagePipelineExecution&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|StartImagePipelineExecution|系统规定参数。取值：StartImagePipelineExecution |
|ImagePipelineId|String|是|ip-2ze5tsl5bp6nf2b3\*\*\*\*|镜像模板ID。 |
|RegionId|String|是|cn-hangzhou|所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。**ClientToken**只支持ASCII字符，且不能超过64个字符。更多详情，请参见[如何保证幂等性](~~25693~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|ExecutionId|String|exec-5fb8facb8ed7427c\*\*\*\*|构建任务ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=StartImagePipelineExecution
&ImagePipelineId=ip-2ze5tsl5bp6nf2b3****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<StartImagePipelineExecutionResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <ExecutionId>exec-5fb8facb8ed7427c****</ExecutionId>
</StartImagePipelineExecutionResponse>
```

`JSON` 格式

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E", 
    "ExecutionId": "exec-5fb8facb8ed7427c****"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

