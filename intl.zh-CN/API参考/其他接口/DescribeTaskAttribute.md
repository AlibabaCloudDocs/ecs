# DescribeTaskAttribute

调用DescribeTaskAttribute查询异步任务的详细信息。目前，可以查询的异步任务有导入镜像（ImportImage）、导出镜像（ExportImage）及变更云盘类型（ModifyDiskSpec）。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeTaskAttribute&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeTaskAttribute|系统规定参数。取值：DescribeTaskAttribute |
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|TaskId|String|是|t-ce946ntx4wr\*\*\*\*|任务ID。您可以调用[DescribeTasks](~~25622~~)查看任务ID。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CreationTime|String|2015-11-23T02:13Z|任务创建时间。 |
|FailedCount|Integer|0|失败任务数。 |
|FinishedTime|String|2015-11-23T02:19Z|任务完成时间。 |
|OperationProgressSet|Array of OperationProgress| |返回任务包含的信息，其中包括每一个子任务的状态和相关信息。 |
|OperationProgress| | | |
|ErrorCode|String|ParameterInvalid|错误代码。 |
|ErrorMsg|String|The specified RegionId parameter is invalid.|错误信息。 |
|OperationStatus|String|Success|操作状态。 |
|RelatedItemSet|Array of RelatedItem| |资源信息类型。 |
|RelatedItem| | | |
|Name|String|OSSObject|相关项名称。 |
|Value|String|MYOSSPRE\_m-23f8tcp\*\*\*\_t-23ym6mv\*\*\*.vhd|相关项值。 |
|RegionId|String|cn-hangzhou|地域ID。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|SuccessCount|Integer|1|成功任务数。 |
|SupportCancel|String|true|是否可以取消任务（[CancelTask](~~25624~~)）。取值范围：

 -   true：可以取消
-   false：无法取消 |
|TaskAction|String|ExportImage|任务操作的接口名称。 |
|TaskId|String|t-ce946ntx4wr\*\*\*\*|任务ID。 |
|TaskProcess|String|100%|任务进程。 |
|TaskStatus|String|Finished|任务状态。 |
|TotalCount|Integer|1|任务总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeTaskAttribute
&RegionId=cn-hangzhou
&TaskId=t-ce946ntx4wr****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeTaskAttributeResponse>
    <CreationTime>2015-11-23T02:13Z</CreationTime>
    <OperationProgressSet>
        <OperationProgress>
            <RelatedItemSet>
                <RelatedItem>
                    <Name>OSSBucket</Name>
                    <Value>image-temp</Value>
                </RelatedItem>
                <RelatedItem>
                    <Name>OSSObject</Name>
                    <Value>MYOSSPRE_m-23f8tcp***_t-23ym6mv***.vhd</Value>
                </RelatedItem>
                <RelatedItem>
                    <Name>ImageFormat</Name>
                    <Value>vhd</Value>
                </RelatedItem>
            </RelatedItemSet>
            <ErrorMsg></ErrorMsg>
            <ErrorCode></ErrorCode>
            <OperationStatus>Success</OperationStatus>
        </OperationProgress>
    </OperationProgressSet>
    <FinishedTime>2015-11-23T02:19Z</FinishedTime>
    <FailedCount>0</FailedCount>
    <SupportCancel>true</SupportCancel>
    <TotalCount>1</TotalCount>
    <SuccessCount>1</SuccessCount>
    <RequestId>EF0C5969-279B-49C8-AD83-BACCC74DD38C</RequestId>
    <RegionId>cn-hangzhou</RegionId>
    <TaskAction>ExportImage</TaskAction>
    <TaskStatus>Finished</TaskStatus>
    <TaskProcess>100%</TaskProcess>
    <TaskId>t-ce946ntx4wr****</TaskId>
</DescribeTaskAttributeResponse>
```

`JSON` 格式

```
{
    "CreationTime": "2015-11-23T02:13Z",
    "OperationProgressSet": {
        "OperationProgress": [
            {
                "RelatedItemSet": {
                    "RelatedItem": [
                        {
                            "Name": "OSSBucket",
                            "Value": "image-temp"
                        },
                        {
                            "Name": "OSSObject",
                            "Value": "MYOSSPRE_m-23f8tcp***_t-23ym6mv***.vhd"
                        },
                        {
                            "Name": "ImageFormat",
                            "Value": "vhd"
                        }
                    ]
                },
                "ErrorMsg": "",
                "ErrorCode": "",
                "OperationStatus": "Success"
            }
        ]
    },
    "FinishedTime": "2015-11-23T02:19Z",
    "FailedCount": 0,
    "SupportCancel": true,
    "TotalCount": 1,
    "SuccessCount": 1,
    "RequestId": "4BE2C7FE-C7A4-4675-A153-174E032AABFB",
    "RegionId": "cn-hangzhou",
    "TaskAction": "ExportImage",
    "TaskStatus": "Finished",
    "TaskProcess": "100%",
    "TaskId": "t-ce946ntx4wr****"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的地域ID不存在。|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数RegionId不得为空。|
|400|MissingParameter|An input parameter "TaskId" that is mandatory for processing the request is not supplied.|参数TaskId不得为空。|
|400|InvalidTaskId.NotFound|The specified "TaskId" is not found.|指定的TaskId不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

