# DescribeCloudAssistantStatus

调用DescribeCloudAssistantStatus查询一台或者多台实例是否安装了云助手客户端。如果已安装了云助手，还将查询云助手命令执行的总数量、正在执行的数量以及最近一次命令执行的时间。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeCloudAssistantStatus&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCloudAssistantStatus|系统规定参数。取值：DescribeCloudAssistantStatus |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。 |
|InstanceId.N|RepeatList|否|i-bp1iudwa5b1tqa\*\*\*\*|实例ID列表，单次请求最多支持100台实例。N的取值范围：1~100 |
|OSType|String|否|Windows|实例的操作系统类型。取值范围：

 -   Windows
-   Linux |
|PageNumber|Long|否|1|当前页码。

 起始值：1

 默认值：1 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 最大值：100

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|InstanceCloudAssistantStatusSet|Array of InstanceCloudAssistantStatus| |实例云助手安装状态结果集合。 |
|InstanceCloudAssistantStatus| | | |
|ActiveTaskCount|Long|0|正在执行的命令的数量。 |
|CloudAssistantStatus|String|true|是否已经安装了云助手。 |
|CloudAssistantVersion|String|2.2.0.106|云助手客户端版本号。 |
|InstanceId|String|i-bp1iudwa5b1tqa\*\*\*\*|实例ID。 |
|InvocationCount|Long|2|已执行的命令的总数量。 |
|LastInvokedTime|String|2021-03-15T08:00:00Z|最近一次命令执行的时间。 |
|OSType|String|Linux|实例操作系统类型。可能值：

 -   Windows
-   Linux |
|PageNumber|Long|1|当前页码。 |
|PageSize|Long|1|每页行数。 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。 |
|TotalCount|Long|1|实例总个数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeCloudAssistantStatus
&InstanceId.1=i-bp1iudwa5b1tqa****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeCloudAssistantStatusResponse>
      <TotalCount>1</TotalCount>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageSize>1</PageSize>
      <PageNumber>1</PageNumber>
      <InstanceCloudAssistantStatusSet>
            <InstanceCloudAssistantStatus>
                  <CloudAssistantVersion>2.2.0.106</CloudAssistantVersion>
                  <InstanceId>i-bp1iudwa5b1tqa****</InstanceId>
                  <CloudAssistantStatus>true</CloudAssistantStatus>
                  <OSType>Linux</OSType>
                  <InvocationCount>2</InvocationCount>
                  <ActiveTaskCount>0</ActiveTaskCount>
                  <LastInvokedTime>2021-03-15T08:00:00Z</LastInvokedTime>
            </InstanceCloudAssistantStatus>
      </InstanceCloudAssistantStatusSet>
</DescribeCloudAssistantStatusResponse>
```

`JSON`格式

```
{
  "TotalCount": 1,
  "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
  "PageSize": 1,
  "PageNumber": 1,
  "InstanceCloudAssistantStatusSet": {
    "InstanceCloudAssistantStatus": [
      {
        "CloudAssistantVersion": "2.2.0.106",
        "InstanceId": "i-bp1iudwa5b1tqa****",
        "CloudAssistantStatus": "true",
        "OSType": "Linux",
        "InvocationCount": 2,
        "ActiveTaskCount": 0,
        "LastInvokedTime": "2021-03-15T08:00:00Z"
      }
    ]
  }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|指定地域下不支持调用API。请检查RegionId参数取值是否正确。|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|404|InvalidInstance.NotFound|The specified instance does not exist.|指定的实例不存在。|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|目标实例数量超过上限。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

