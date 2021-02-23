# DescribeAutoProvisioningGroupHistory

调用DescribeAutoProvisioningGroupHistory查询弹性供应组的调度任务信息。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupHistory&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAutoProvisioningGroupHistory|系统规定参数。取值：DescribeAutoProvisioningGroupHistory |
|AutoProvisioningGroupId|String|是|apg-bp67acfmxazb4p\*\*\*\*|弹性供应组的ID。 |
|RegionId|String|是|cn-hangzhou|弹性供应组所在地域的ID。 |
|PageNumber|Integer|否|1|分页查询的当前页码。起始值：1

 默认值：1 |
|PageSize|Integer|否|5|分页查询时设置的每页行数。最大值：100

 默认值：10 |
|StartTime|String|否|2019-04-01T15:10:20Z|查询调度历史的起始时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EndTime|String|否|2019-06-20T15:10:20Z|查询调度历史的结束时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutoProvisioningGroupHistories|Array of AutoProvisioningGroupHistory| |所有调度任务的信息。 |
|AutoProvisioningGroupHistory| | | |
|ActivityDetails|Array of ActivityDetail| |单次调度任务的详细信息。 |
|ActivityDetail| | | |
|Detail|String|New ECS instances "i-bp67acfmxazb4p\*\*\*\*, i-bp67acfmxazb5p\*\*\*\*" created.|单次调度任务一次实例创建活动的执行详情。 |
|Status|String|Successful|单次调度任务一次实例创建活动的执行状态。可能值：

 -   Successful：实例创建成功。
-   Failed：实例创建失败。
-   InProgress：实例创建中。
-   Warning：实例部分创建成功。 |
|LastEventTime|String|2019-04-01T15:10:20Z|单次调度任务最后一次实例创建活动的执行时间。 |
|StartTime|String|2019-04-01T15:10:20Z|开始执行单次调度任务的时间。 |
|Status|String|success|单次调度任务的状态。可能值：

 -   prepare：调度任务执行中。
-   success：调度任务执行成功。
-   failed：调度任务执行失败。 |
|TaskId|String|apg-task-bp67acfmxazb4p\*\*\*\*|单次调度任务的ID。 |
|PageNumber|Integer|1|页码。 |
|PageSize|Integer|10|每页行数。 |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|请求ID。 |
|TotalCount|Integer|10|查询到的调度任务的总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupHistory
&AutoProvisioningGroupId=apg-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeAutoProvisioningGroupsResponse>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>BA55349F-6E36-4E64-964B-419515D1****</RequestId>
      <AutoProvisioningGroupHistories>
            <AutoProvisioningGroupHistory>
                  <Status>success</Status>
                  <ActivityDetails>
                        <ActivityDetail>
                              <Detail>New ECS instances i-bp67acfmxazb4ph***, i-bp67acfmxazb4pi*** created.</Detail>
                              <Status>Successful</Status>
                        </ActivityDetail>
                  </ActivityDetails>
                  <LastEventTime>2019-06-17T08:48:00Z</LastEventTime>
                  <StartTime>2019-06-17T08:47:52Z</StartTime>
                  <TaskId>apg-task-uf66bqtabg10wcf6****</TaskId>
            </AutoProvisioningGroupHistory>
      </AutoProvisioningGroupHistories>
</DescribeAutoProvisioningGroupsResponse>
```

`JSON`格式

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "BA55349F-6E36-4E64-964B-419515D1****",
    "AutoProvisioningGroupHistories": {
        "AutoProvisioningGroupHistory": [
            {
                "Status": "success",
                "ActivityDetails": {
                    "ActivityDetail": [
                        {
                            "Detail": "New ECS instances i-bp67acfmxazb4ph***, i-bp67acfmxazb4pi*** created.",
                            "Status": "Successful"
                        }
                    ]
                },
                "LastEventTime": "2019-06-17T08:48:00Z",
                "StartTime": "2019-06-17T08:47:52Z",
                "TaskId": "apg-task-uf66bqtabg10wcf6****"
            }
        ]
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|您没有操作此资源的权限，或者此 API 不支持 RAM 角色。|
|400|MissingParamter.RegionId|The regionId should not be null.|参数RegionId不得为空。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

