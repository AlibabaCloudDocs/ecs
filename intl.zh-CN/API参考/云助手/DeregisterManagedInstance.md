# DeregisterManagedInstance

调用DeregisterManagedInstance注销一个托管实例。注销后您将无法再使用云助手向实例发送命令或文件。

****

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DeregisterManagedInstance&type=RPC&version=2014-05-26)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeregisterManagedInstance|系统规定参数。取值：DeregisterManagedInstance |
|InstanceId|String|是|mi-hz01axdfas\*\*\*\*|托管实例ID。 |
|RegionId|String|是|cn-hangzhou|地域ID。目前仅支持华东1（杭州）、华北2（北京）、华东2（上海）。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Instance|Struct| |托管实例的信息组成的集合。 |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F7494\*\*\*\*|激活码ID。 |
|AgentVersion|String|2.2.0.102|云助手客户端的版本号。 |
|Hostname|String|test-Hostname|托管实例主机名。 |
|InstanceId|String|mi-hz01axdfas\*\*\*\*|托管实例ID。 |
|InstanceName|String|test-InstanceName-001|托管实例名称。 |
|InternetIp|String|47.8.\*\*.\*\*|托管实例的公网IP。 |
|IntranetIp|String|10.0.\*\*.\*\*|托管实例的内网IP。 |
|InvocationCount|Long|2|托管实例执行云助手任务的次数。 |
|LastInvokedTime|String|2021-01-20T09:00:40Z|最后一次执行云助手任务的时间。 |
|MachineId|String|e03231b37ab14e53b5795ad625fc\*\*\*\*|托管实例的机器码。 |
|OsType|String|linux|托管实例的操作系统。 |
|OsVersion|String|Linux\_\#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021\_x86\_64|操作系统的版本信息。 |
|RegistrationTime|String|2021-01-20T08:57:56Z|托管实例的注册时间。 |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74942176|请求ID。 |

## 示例

请求示例

```
https://ecs.aliyuncs.com/?Action=DeregisterManagedInstance
&InstanceId=mi-hz01axdfas****
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<DeregisterManagedInstanceResponse>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F74942176</RequestId>
      <Instance>
            <MachineId>e03231b37ab14e53b5795ad625fc****</MachineId>
            <AgentVersion>2.2.0.102</AgentVersion>
            <InstanceId>mi-hz01axdfas****</InstanceId>
            <InvocationCount>2</InvocationCount>
            <OsVersion>Linux_#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021_x86_64</OsVersion>
            <Hostname>test-Hostname</Hostname>
            <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F7494****</ActivationId>
            <RegistrationTime>2021-01-20T08:57:56Z</RegistrationTime>
            <IntranetIp>10.0.**.**</IntranetIp>
            <InstanceName>test-InstanceName-001</InstanceName>
            <InternetIp>47.8.**.**</InternetIp>
            <OsType>linux</OsType>
            <LastInvokedTime>2021-01-20T09:00:40Z</LastInvokedTime>
      </Instance>
</DeregisterManagedInstanceResponse>
```

`JSON`格式

```
{
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F74942176", 
    "Instance": {
        "MachineId": "e03231b37ab14e53b5795ad625fc****", 
        "AgentVersion": "2.2.0.102", 
        "InstanceId": "mi-hz01axdfas****", 
        "InvocationCount": "2", 
        "OsVersion": "Linux_#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021_x86_64", 
        "Hostname": "test-Hostname", 
        "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F7494****", 
        "RegistrationTime": "2021-01-20T08:57:56Z", 
        "IntranetIp": "10.0.**.**", 
        "InstanceName": "test-InstanceName-001", 
        "InternetIp": "47.8.**.**", 
        "OsType": "linux", 
        "LastInvokedTime": "2021-01-20T09:00:40Z"
    }
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发送请求时发生错误，请稍后重试。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Ecs)查看更多错误码。

