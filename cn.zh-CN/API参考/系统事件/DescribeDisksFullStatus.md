# DescribeDisksFullStatus

调用DescribeDisksFullStatus查询一块或多块块存储的全部状态信息。

## 接口说明

-   块存储的全部状态信息包含块存储生命周期（`Status`）、块存储健康状态（`HealthStatus`）和块存储事件类型（`EventType`）。
-   由于块存储相关事件的发布时间、事件的计划执行时间以及事件的实际执行时间相同，如果指定一段时间（`EventTime.Start`~`EventTime.End`），则可以查询这段时间中发生过的所有历史事件。目前，您最多可以查询最近一周的历史事件。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeDisksFullStatus&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeDisksFullStatus|系统规定参数。取值：DescribeDisksFullStatus |
|RegionId|String|是|cn-hangzhou|块存储所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|DiskId.N|RepeatList|否|d-bp67acfmxazb4p\*\*\*\*|块存储ID。N的取值范围：1~100 |
|EventId.N|RepeatList|否|e-bp67acfmxazb4p\*\*\*\*|事件ID。N的取值范围：1~100 |
|Status|String|否|Available|指定块存储的生命周期状态，详情请参见[云盘状态表](~~25689~~)。取值范围：

 -   In\_use：使用中
-   Available：待挂载
-   Attaching：挂载中
-   Detaching：卸载中
-   Creating：创建中
-   ReIniting：初始化中 |
|HealthStatus|String|否|Warning|指定块存储的健康状态。取值范围：

 -   Impaired：暂时性不可读写
-   Warning：服务降级
-   Initializing：初始化中
-   InsufficientData：数据不足
-   NotApplicable：不适用 |
|EventType|String|否|Stalled|指定块存储的事件类型。取值范围：

 -   Degraded：块存储性能降级。
-   SeverelyDegraded：块存储性能严重降级。
-   Stalled：块存储性能受到严重影响。
-   ErrorDetected：本地盘出现损坏。 |
|EventTime.Start|String|否|2018-05-06T02:43:10Z|查询事件发生时间的开始时间。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC+0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。 |
|EventTime.End|String|否|2018-05-08T02:48:52Z|查询事件发生时间的结束时间。

 按照[ISO8601](~~25696~~)标准表示，并使用UTC+0时间，格式为`yyyy-MM-ddTHH:mm:ssZ`。 |
|PageNumber|Integer|否|1|查询结果的页码。取值范围：正整数

 默认值：1 |
|PageSize|Integer|否|10|查询结果的分页大小。取值范围：1~100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|DiskFullStatusSet|Array of DiskFullStatusType| |块存储全状态数组。 |
|DiskFullStatusType| | | |
|Device|String|null|块存储挂载于实例上的设备名，例如/dev/xvdb。

 该参数仅在`Status`参数值为`In_use`时有值，其他状态时为空。

 **说明：** 该参数即将停止使用，为提高代码兼容性，建议您尽量不要使用该参数。 |
|DiskEventSet|Array of DiskEventType| |块存储事件数组。 |
|DiskEventType| | | |
|EventEndTime|String|2018-05-06T02:48:52Z|事件结束时间。 |
|EventId|String|e-bp67acfmxazb4p\*\*\*\*|块存储事件ID。 |
|EventTime|String|2018-05-08T02:43:10Z|事件发生时间。 |
|EventType|Struct| |事件类型。 |
|Code|Integer|7|事件类型代码。 |
|Name|String|Stalled|事件类型名称。可能值：

 -   Degraded：块存储性能降级。
-   SeverelyDegraded：块存储性能严重降级。
-   Stalled：块存储性能受到严重影响。
-   ErrorDetected：本地盘出现损坏。 |
|ImpactLevel|String|100|影响级别。 |
|DiskId|String|d-bp67acfmxazb4p\*\*\*\*|块存储ID。 |
|HealthStatus|Struct| |块存储健康状态。 |
|Code|Integer|128|块存储健康状态代码。 |
|Name|String|Impaired|块存储健康状态名称。 |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|实例ID。 |
|Status|Struct| |块存储生命周期状态。 |
|Code|Integer|129|块存储生命周期状态代码。 |
|Name|String|Available|块存储生命周期状态名称。 |
|PageNumber|Integer|1|列表页码。 |
|PageSize|Integer|10|每页大小。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Integer|2|全状态总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&DiskId.1=d-bp13pl2v34qj0xg0****
&EventId.1=e-uf64yvznlao4jl2c****
&Status=Available
&HealthStatus=Warning
&EventType=Stalled
&EventTime.Start=2018-05-06T02:43:10Z
&EventTime.End=2018-05-08T02:48:52Z
&PageNumber=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<DescribeDisksFullStatusResponse>
      <DiskFullStatusSet>
            <DiskFullStatusType>
                  <DiskEventSet>
                        <DiskEventType>
                              <EventId>e-bp67acfmxazb4p****</EventId>
                              <EventType>
                                    <Code>7</Code>
                                    <Name>Stalled</Name>
                              </EventType>
                              <EventTime>2018-05-08T02:43:10Z</EventTime>
                        </DiskEventType>
                  </DiskEventSet>
                  <DiskId>d-bp67acfmxazb4p****</DiskId>
                  <InstanceId>i-bp67acfmxazb4p****</InstanceId>
                  <Device>/dev/xvda</Device>
                  <HealthStatus>
                        <Code>128</Code>
                        <Name>Impaired</Name>
                  </HealthStatus>
                  <Status>
                        <Code>129</Code>
                        <Name>Available</Name>
                  </Status>
            </DiskFullStatusType>
            <DiskFullStatusType>
                  <DiskEventSet>
                        <DiskEventType>
                              <EventId>e-bp67acfmxazb4p****</EventId>
                              <EventType>
                                    <Code>1</Code>
                                    <Name>Degraded</Name>
                              </EventType>
                              <EventTime>2018-05-06T02:43:10Z</EventTime>
                              <EventEndTime>2018-05-06T02:48:52Z</EventEndTime>
                        </DiskEventType>
                  </DiskEventSet>
                  <DiskId>d-disk2</DiskId>
                  <InstanceId>i-instance2</InstanceId>
                  <Device>/dev/xvdb</Device>
                  <HealthStatus>
                        <Code>64</Code>
                        <Name>Warning</Name>
                  </HealthStatus>
                  <Status>
                        <Code>0</Code>
                        <Name>Ok</Name>
                  </Status>
            </DiskFullStatusType>
      </DiskFullStatusSet>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <RequestId>1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211</RequestId>
      <TotalCount>2</TotalCount>
</DescribeDisksFullStatusResponse>
```

`JSON` 格式

```
{
    "DiskFullStatusSet": {
        "DiskFullStatusType": [
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-bp67acfmxazb4p****",
                            "EventType": {
                                "Code": "7",
                                "Name": "Stalled"
                            },
                            "EventTime": "2018-05-08T02:43:10Z"
                        }
                    ]
                },
                "DiskId": "d-bp67acfmxazb4p****",
                "InstanceId": "i-bp67acfmxazb4p****",
                "Device": "/dev/xvda",
                "HealthStatus": {
                    "Code": 128,
                    "Name": "Impaired"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            },
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-bp67acfmxazb4p****",
                            "EventType": {
                                "Code": "1",
                                "Name": "Degraded"
                            },
                            "EventTime": "2018-05-06T02:43:10Z",
                            "EventEndTime": "2018-05-06T02:48:52Z"
                        }
                    ]
                },
                "DiskId": "d-disk2",
                "InstanceId": "i-instance2",
                "Device": "/dev/xvdb",
                "HealthStatus": {
                    "Code": 0,
                    "Name": "Ok"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            }
        ]
    },
    "PageNumber": 1,
    "PageSize": 10,
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "TotalCount": 2
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失参数，请检查参数是否完整。|
|403|InvalidParameter|%s|无效的参数。|
|403|DiskIdLimitExceeded|%s|指定的DiskId个数不能超过100个。|
|403|EventIdLimitExceeded|%s|一次最多能指定100个模拟事件ID。|
|403|InvalidParameter.TimeEndBeforeStart|%s|您输入的参数无效，请确认结束时间是否早于开始时间。|
|403|OperationDenied.NotInWhiteList|%s|该操作无效，请先加入白名单。|
|403|TooManyDiskEvent.DiskIdRequired|%s|对此资源ID的请求过多，请稍后重试。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

