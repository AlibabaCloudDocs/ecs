# DescribeManagedInstances

调用DescribeManagedInstances查询托管实例列表。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeManagedInstances&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeManagedInstances|系统规定参数。取值：DescribeManagedInstances |
|RegionId|String|是|cn-hangzhou|地域ID。目前仅支持华东1（杭州）、华北2（北京）、华东2（上海）。 |
|OsType|String|否|windows|托管实例的操作系统类型，取值：

 -   windows
-   linux |
|InstanceIp|String|否|192.168.2.2|托管实例的内网IP或公网IP。 |
|ActivationId|String|否|4ECEEE12-56F1-4FBC-9AB1-890F7494\*\*\*\*|激活码ID。 |
|InstanceName|String|否|my-webapp-server|托管实例的名称。 |
|InstanceId.N|RepeatList|否|mi-hz018jrc1o0\*\*\*\*|托管实例的ID。N的取值范围：1~50 |
|PageNumber|Long|否|1|托管实例列表的页码。

 起始值：1

 默认值：1 |
|PageSize|Long|否|10|分页查询时设置的每页行数。

 最大值：50

 默认值：10 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Instances|Array of Instance| |由Instances组成的数组格式，返回托管实例的信息。 |
|ActivationId|String|3704F543-F768-43FA-9864-897F75B3\*\*\*\*|激活码ID。 |
|AgentVersion|String|2.2.0.102|云助手客户端的版本号。 |
|Connected|Boolean|true|托管实例是否已连接。

 -   true：托管实例已连接，您可以通过云助手管理托管实例。
-   false：托管实例未连接，服务器可能停机或者云助手客户端未正确安装。 |
|Hostname|String|demo|托管实例主机名。 |
|InstanceId|String|mi-hz018jrc1o0\*\*\*\*|托管实例ID。 |
|InstanceName|String|webAPP-linux-01|托管实例名称。 |
|InternetIp|String|40.65.\*\*.\*\*|托管实例的公网IP。 |
|IntranetIp|String|10.0.\*\*.\*\*|托管实例的内网IP。 |
|InvocationCount|Long|1|托管实例执行云助手任务的次数。 |
|LastInvokedTime|String|2021-01-20T09:00:40Z|最后一次执行云助手任务的时间。 |
|MachineId|String|e03231b37ab14e53b5795ad625fc\*\*\*\*|托管实例的机器码。 |
|OsType|String|Linux|托管实例的操作系统。 |
|OsVersion|String|Linux\_\#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021\_x86\_64|操作系统的版本信息。 |
|RegistrationTime|String|2021-01-20T08:57:56Z|托管实例的注册时间。 |
|PageNumber|Long|1|托管实例列表的页码。 |
|PageSize|Long|10|输入时设置的每页行数。 |
|RequestId|String|77115469-F2C5-4ECA-94F7-FA04F2FD\*\*\*\*|请求ID。 |
|TotalCount|Long|1|查询到的托管实例总数。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DescribeManagedInstances
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DescribeManagedInstancesResponse>
  <Instances>
        <MachineId>e03231b37ab14e53b5795ad625fc****</MachineId>
        <InstanceId>mi-hz018jrc1o0****</InstanceId>
        <AgentVersion>2.2.0.102</AgentVersion>
        <Connected>true</Connected>
        <InvocationCount>1</InvocationCount>
        <OsVersion>Linux_#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021_x86_64</OsVersion>
        <ActivationId>3704F543-F768-43FA-9864-897F75B3****</ActivationId>
        <Hostname>demo</Hostname>
        <RegistrationTime>2021-01-20T08:57:56Z</RegistrationTime>
        <IntranetIp>10.0.**.**</IntranetIp>
        <InstanceName>webAPP-linux-01</InstanceName>
        <InternetIp>40.65.**.**</InternetIp>
        <OsType>Linux</OsType>
        <LastInvokedTime>2021-01-20T09:00:40Z</LastInvokedTime>
  </Instances>
  <TotalCount>1</TotalCount>
  <RequestId>77115469-F2C5-4ECA-94F7-FA04F2FDC8F4</RequestId>
  <PageSize>10</PageSize>
  <PageNumber>1</PageNumber>
</DescribeManagedInstancesResponse>
```

`JSON`格式

```
{
	"Instances": [
		{
			"MachineId": "e03231b37ab14e53b5795ad625fc****",
			"InstanceId": "mi-hz018jrc1o0****",
			"AgentVersion": "2.2.0.102",
			"Connected": true,
			"InvocationCount": 1,
			"OsVersion": "Linux_#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021_x86_64",
			"ActivationId": "3704F543-F768-43FA-9864-897F75B3****",
			"Hostname": "demo",
			"RegistrationTime": "2021-01-20T08:57:56Z",
			"IntranetIp": "10.0.**.**",
			"InstanceName": "webAPP-linux-01",
			"InternetIp": "40.65.**.**",
			"OsType": "Linux",
			"LastInvokedTime": "2021-01-20T09:00:40Z"
		}
	],
	"TotalCount": 1,
	"RequestId": "77115469-F2C5-4ECA-94F7-FA04F2FDC8F4",
	"PageSize": 10,
	"PageNumber": 1
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|
|400|InvalidParam.PageNumber|The specified parameter is invalid.|指定的PageNumber参数无效。|
|400|InvalidParam.PageSize|The specified parameter is invalid.|指定的PageSize参数无效。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

