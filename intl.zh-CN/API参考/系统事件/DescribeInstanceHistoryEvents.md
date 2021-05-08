# DescribeInstanceHistoryEvents

调用DescribeInstanceHistoryEvents查询实例的系统事件信息，默认查询已完结（系统事件状态为Executed、Avoided、Canceled、Failed）的历史系统事件。通过指定InstanceEventCycleStatus参数，可以查询任意状态的系统事件。

## 接口说明

-   您最多可以查询最近30天的已完结历史系统事件。对于未完结的系统事件无查询时间限制。
-   通过指定InstanceEventCycleStatus参数，还可以查询处于Scheduled（等待执行事件）、Executing（事件执行中）和Inquiring（事件问询中）状态的系统事件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceHistoryEvents&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeInstanceHistoryEvents|系统规定参数。取值：**DescribeInstanceHistoryEvents**。 |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceId|String|否|i-uf678mass4zvr9n1\*\*\*\*|资源ID。取值范围：

 -   当`ResourceType=instance`时，资源ID表示ECS实例ID。
-   当`ResourceType=ddh`时，资源ID表示专有宿主机ID。
-   当`ResourceType=managedhost`时，资源ID表示智能全托管资源池中的物理机ID。

 如果不指定该参数，表示查询指定地域（`RegionId`）和指定资源类型（`ResourceType`）下，所有资源的系统事件信息。

 **说明：** 推荐您使用`ResourceId.N`参数设置一个或多个资源ID。如果您同时指定了`ResourceId.N`参数和`InstanceId`参数，系统默认优先生效`ResourceId.N`参数。 |
|EventCycleStatus|String|否|Executed|系统事件的生命周期状态。EventCycleStatus只在未指定InstanceEventCycleStatus.N参数时有效。取值范围：

 -   Scheduled：等待执行事件
-   Avoided：事件已避免
-   Executing：事件执行中
-   Executed：事件已完成执行
-   Canceled：事件已取消
-   Failed：事件执行失败
-   Inquiring：事件问询中 |
|EventType|String|否|SystemMaintenance.Reboot|系统事件的类型。EventType参数只在未指定InstanceEventType.N参数时有效。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启。
-   SystemMaintenance.Redeploy：因系统维护实例重新部署。
-   SystemFailure.Reboot：因系统错误实例重启。
-   SystemFailure.Redeploy：因系统错误实例重新部署。
-   SystemFailure.Delete：因实例创建失败实例释放。
-   InstanceFailure.Reboot：因实例错误实例重启。
-   InstanceExpiration.Stop：因包年包月期限到期，实例停止。
-   InstanceExpiration.Delete：因包年包月期限到期，实例释放。
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止。
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放。 |
|NotBefore.Start|String|否|2017-11-30T06:32:31Z|查询系统事件计划执行时间的开始时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|NotBefore.End|String|否|2017-12-01T06:32:31Z|查询系统事件计划执行时间的结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EventPublishTime.Start|String|否|2017-11-30T06:32:31Z|查询系统事件发布时间的开始时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EventPublishTime.End|String|否|2017-12-01T06:32:31Z|查询系统事件发布时间的结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|PageNumber|Integer|否|1|查询结果的页码。取值范围：正整数

 默认值：1 |
|PageSize|Integer|否|10|查询结果的分页大小。取值范围：1~100

 默认值：10 |
|ResourceType|String|否|instance|资源类型。取值范围：

 -   instance：ECS实例
-   ddh：专有宿主机
-   managedhost：智能全托管资源池中的物理机

 默认值：instance |
|EventId.N|String|否|e-uf64yvznlao4jl2c\*\*\*\*|一个或者多个系统事件ID。N的取值范围：1~100，多个取值使用重复列表的形式。 |
|InstanceEventCycleStatus.N|String|否|Executed|一个或者多个系统事件的生命周期状态。N的取值范围：1~6，多个取值使用重复列表的形式。取值范围：

 -   Scheduled：等待执行事件
-   Avoided：事件已避免
-   Executing：事件执行中
-   Executed：事件已完成执行
-   Canceled：事件已取消
-   Failed：事件执行失败
-   Inquiring：事件问询中 |
|InstanceEventType.N|String|否|SystemMaintenance.Reboot|一个或者多个系统事件的类型。N的取值范围：1~30，多个取值使用重复列表的形式。取值范围：

 -   SystemMaintenance.Reboot：因系统维护实例重启。
-   SystemMaintenance.Redeploy：因系统维护实例重新部署。
-   SystemFailure.Reboot：因系统错误实例重启。
-   SystemFailure.Redeploy：因系统错误实例重新部署。
-   SystemFailure.Delete：因实例创建失败实例释放。
-   InstanceFailure.Reboot：因实例错误实例重启。
-   InstanceExpiration.Stop：因包年包月期限到期，实例停止。
-   InstanceExpiration.Delete：因包年包月期限到期，实例释放。
-   AccountUnbalanced.Stop：因账号欠费，按量付费实例停止。
-   AccountUnbalanced.Delete：因账号欠费，按量付费实例释放。 |
|ResourceId.N|String|否|i-uf678mass4zvr9n1\*\*\*\*|一个或多个资源ID。N的取值范围：1~100。参数的多个取值使用重复列表的形式。取值范围：

 -   当`ResourceType=instance`时，资源ID表示ECS实例ID。
-   当`ResourceType=ddh`时，资源ID表示专有宿主机ID。
-   当`ResourceType=managedhost`时，资源ID表示智能全托管资源池中的物理机ID。

 如果不指定该参数，表示查询指定地域（`RegionId`）和指定资源类型（`ResourceType`）下，所有资源的系统事件信息。

 **说明：** 推荐您使用`ResourceId.N`参数设置一个或多个资源ID。如果您同时指定了`ResourceId.N`参数和`InstanceId`参数，系统默认优先生效`ResourceId.N`参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageSize|Integer|10|输入时设置的每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|PageNumber|Integer|1|实例列表页码。 |
|TotalCount|Integer|2|实例总个数。 |
|InstanceSystemEventSet|Array of InstanceSystemEventType| |实例历史系统事件组成的数组。 |
|InstanceSystemEventType| | | |
|EventId|String|e-uf64yvznlao4jl2c\*\*\*\*|系统事件ID。 |
|EventPublishTime|String|2017-11-30T06:32:31Z|系统事件发布时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|EventFinishTime|String|2017-12-01T06:35:31Z|系统事件结束时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|ResourceType|String|instance|资源类型。可能值：

 -   instance：ECS实例
-   ddh：专有宿主机
-   managedhost：智能全托管资源池中的物理机 |
|ImpactLevel|String|100|影响级别。 |
|NotBefore|String|2017-12-06T00:00:00Z|系统事件计划执行时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|InstanceId|String|i-uf678mass4zvr9n1\*\*\*\*|资源ID。 |
|Reason|String|System maintenance is scheduled due to \*\*\*.|系统事件的计划原因。 |
|EventType|Object| |系统事件类型。 |
|Name|String|InstanceExpiration.Stop|系统事件类型名称。 |
|Code|Integer|34|系统事件类型代码。 |
|EventCycleStatus|Object| |系统事件的生命周期状态。 |
|Name|String|Executed|系统事件状态名称。 |
|Code|Integer|0|系统事件状态代码。 |
|ExtendedAttribute|Object| |事件扩展属性。 |
|Device|String|/dev/vda|本地盘设备名。 |
|DiskId|String|d-diskid1|本地盘ID。 |
|InactiveDisks|Array of InactiveDisk| |已释放但需要清理的非活跃云盘或本地盘信息组成的数组。 |
|InactiveDisk| | | |
|CreationTime|String|2018-11-30T06:32:31Z|云盘或本地盘创建时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |
|DeviceSize|String|80|云盘或本地盘大小，单位GiB。 |
|DeviceCategory|String|cloud\_efficiency|云盘或本地盘种类。可能值：

 -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD盘
-   cloud\_essd：ESSD云盘
-   local\_ssd\_pro：I/O密集型本地盘
-   local\_hdd\_pro：吞吐密集型本地盘
-   ephemeral：（已停售）本地盘
-   ephemeral\_ssd：（已停售）本地SSD盘 |
|DeviceType|String|data|云盘或本地盘类型。可能值：

 -   system：系统盘
-   data：数据盘 |
|ReleaseTime|String|2019-11-30T06:32:31Z|云盘或本地盘释放时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceHistoryEvents
&RegionId=cn-hangzhou
&InstanceId=i-uf678mass4zvr9n1****
&EventId.1=e-uf64yvznlao4jl2c****
&InstanceEventCycleStatus.1=Executed
&EventCycleStatus=Executed
&InstanceEventType.1=SystemMaintenance.Reboot
&NotBefore.Start=2017-11-30T06:32:31Z
&NotBefore.End=2017-12-01T06:32:31Z
&PageNumber=1
&PageSize=1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
HTTP/1.1 200 OK
Content-Type:application/xml

<DescribeInstanceHistoryEventsResponse>
    <InstanceSystemEventSet>
        <InstanceSystemEventType>
            <InstanceId>i-uf678mass4zvr9n1****</InstanceId>
            <EventId>e-uf64yvznlao4jl2c****</EventId>
            <EventType>
                <Code>1</Code>
                <Name>SystemMaintenance.Reboot</Name>
            </EventType>
            <EventCycleStatus>
                <Code>0</Code>
                <Name>Executed</Name>
            </EventCycleStatus>
            <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
            <NotBefore>2017-12-01T06:32:31Z</NotBefore>
            <EventFinishTime>2017-12-01T06:35:31Z</EventFinishTime>
            <ResourceType>instance</ResourceType>
        </InstanceSystemEventType>
        <InstanceSystemEventType>
            <InstanceId>i-uf678mass4zvr9n1****</InstanceId>
            <EventId>e-uf61cbvp0w8x2xfx****</EventId>
            <EventType>
                <Code>34</Code>
                <Name>InstanceExpiration.Stop</Name>
            </EventType>
            <EventCycleStatus>
                <Code>8</Code>
                <Name>Avoided</Name>
            </EventCycleStatus>
            <EventPublishTime>2017-11-29T06:32:31Z</EventPublishTime>
            <NotBefore>2017-12-06T00:00:00Z</NotBefore>
            <EventFinishTime>2017-12-05T12:35:31Z</EventFinishTime>
            <ResourceType>instance</ResourceType>
        </InstanceSystemEventType>
    </InstanceSystemEventSet>
    <PageSize>10</PageSize>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <RequestId>02EA76D3-5A2A-44EB-XXXX-8901881D8707</RequestId>
</DescribeInstanceHistoryEventsResponse>
```

`JSON`格式

```
HTTP/1.1 200 OK
Content-Type:application/json

{
  "InstanceSystemEventSet" : {
    "InstanceSystemEventType" : [ {
      "InstanceId" : "i-uf678mass4zvr9n1****",
      "EventId" : "e-uf64yvznlao4jl2c****",
      "EventType" : {
        "Code" : 1,
        "Name" : "SystemMaintenance.Reboot"
      },
      "EventCycleStatus" : {
        "Code" : 0,
        "Name" : "Executed"
      },
      "EventPublishTime" : "2017-11-30T06:32:31Z",
      "NotBefore" : "2017-12-01T06:32:31Z",
      "EventFinishTime" : "2017-12-01T06:35:31Z",
      "ResourceType" : "instance"
    }, {
      "InstanceId" : "i-uf678mass4zvr9n1****",
      "EventId" : "e-uf61cbvp0w8x2xfx****",
      "EventType" : {
        "Code" : 34,
        "Name" : "InstanceExpiration.Stop"
      },
      "EventCycleStatus" : {
        "Code" : 8,
        "Name" : "Avoided"
      },
      "EventPublishTime" : "2017-11-29T06:32:31Z",
      "NotBefore" : "2017-12-06T00:00:00Z",
      "EventFinishTime" : "2017-12-05T12:35:31Z",
      "ResourceType" : "instance"
    } ]
  },
  "PageSize" : 10,
  "PageNumber" : 1,
  "TotalCount" : 2,
  "RequestId" : "02EA76D3-5A2A-44EB-XXXX-8901881D8707"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|InvalidParameter|%s|无效的参数。|
|403|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|
|403|InvalidParameter.TimeEndBeforeStart|%s|您输入的参数无效，请确认结束时间是否早于开始时间。|
|403|OperationDenied.NotInWhiteList|%s|该操作无效，请先加入白名单。|
|404|MissingParameter|%s|缺失参数，请检查参数是否完整。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

