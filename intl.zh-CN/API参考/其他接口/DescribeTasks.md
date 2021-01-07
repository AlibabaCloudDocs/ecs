# DescribeTasks

调用DescribeTasks查询一个或多个异步请求的进度。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeTasks&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeTasks|系统规定参数。取值：DescribeTasks |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|PageNumber|Integer|否|1|查询结果的页码。

 起始值：1

 默认值：1 |
|PageSize|Integer|否|2|分页查询时设置的每页记录数。

 最大值：100

 默认值：10 |
|TaskIds|String|否|t-bp1hvgwromzv32iq\*\*\*\*,t-bp179lofu2pv768w\*\*\*\*|任务ID，单次最多支持指定100个，ID之间使用半角逗号（,）分隔。 |
|TaskAction|String|否|ImportImage|任务操作的接口名称。取值范围：

 -   ImportImage：导入镜像
-   ExportImage：导出镜像
-   RedeployInstance：重新部署ECS实例
-   ModifyDiskSpec：变更云盘类型 |
|TaskStatus|String|否|Finished|任务状态。取值范围：

 -   Finished：已完成
-   Processing：运行中
-   Failed：失败

 默认值：无

 **说明：** 只支持查询状态为Finished、Processing和Failed的任务，填入其他取值将不会生效。 |
|StartTime|String|否|2015-11-23T15:10:00Z|按创建时间查询，创建时间区间的起始点。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EndTime|String|否|2015-11-23T15:16:00Z|按创建时间查询，创建时间区间的终止点。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码。 |
|PageSize|Integer|2|当前分页包含多少条目。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TaskSet|Array of Task| |任务集合。 |
|Task| | | |
|CreationTime|String|2015-11-24T12:50Z|创建时间。 |
|FinishedTime|String|2015-11-24T12:50Z|结束时间。 |
|SupportCancel|String|true|是否支持取消任务。 |
|TaskAction|String|IMPORT\_IMAGE|任务名称。 |
|TaskId|String|t-bp1hvgwromzv32iq\*\*\*\*|任务ID。 |
|TaskStatus|String|Finished|任务状态。 |
|TotalCount|Integer|2|列表条目数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeTasks
&RegionId=cn-hangzhou
&PageNumber=1
&PageSize=2
&TaskIds=t-bp1hvgwromzv32iq****
&TaskAction=ImportImage
&TaskStatus=Finished
&StartTime=2015-11-23T15:10:00Z
&EndTime=2015-11-23T15:16:00Z
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeTasksResponse>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <PageSize>2</PageSize>
    <RegionId>cn-hangzhou</RegionId>
    <RequestId>E5C82807-5588-4661-9A96-350B206A7623</RequestId>
    <TaskSet>
        <Task>
            <CreationTime>2015-11-24T12:50Z</CreationTime>
            <FinishedTime>2015-11-24T12:50Z</FinishedTime>
            <SupportCancel>true</SupportCancel>
            <TaskAction>IMPORT_IMAGE</TaskAction>
            <TaskStatus>Finished</TaskStatus>
            <TaskId>t-bp1hvgwromzv32iq****</TaskId>
        </Task>
        <Task>
            <CreationTime>2015-11-23T15:10Z</CreationTime>
            <FinishedTime>2015-11-23T15:16Z</FinishedTime>
            <SupportCancel>true</SupportCancel>
            <TaskAction>IMPORT_IMAGE</TaskAction>
            <TaskStatus>Finished</TaskStatus>
            <TaskId>t-bp179lofu2pv768w****</TaskId>
        </Task>
    </TaskSet>
</DescribeTasksResponse>
```

`JSON` 格式

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "PageSize": 2,
    "RegionId": "cn-hangzhou",
    "TaskSet": [
        {
            "Task": [
                {
                    "CreationTime": "2015-11-24T12:50Z",
                    "FinishedTime": "2015-11-24T12:50Z",
                    "SupportCancel": true,
                    "TaskAction": "ImportImage",
                    "TaskStatus": "Finished",
                    "TaskId": "t-bp1hvgwromzv32iq****"
                },
                {
                    "CreationTime": "2015-11-23T15:10Z",
                    "FinishedTime": "2015-11-23T15:16Z",
                    "SupportCancel": true,
                    "TaskAction": "ImportImage",
                    "TaskStatus": "Finished",
                    "TaskId": "t-bp179lofu2pv768w****"
                }
            ]
        }
    ],
    "RequestId": "F746C690-D9EA-4F87-AF31-8E1910FAB541"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数RegionId不得为空。|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

