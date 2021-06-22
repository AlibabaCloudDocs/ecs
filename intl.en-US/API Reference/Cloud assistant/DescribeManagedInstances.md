# DescribeManagedInstances

You can call this operation to query managed instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeManagedInstances&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeManagedInstances|The operation that you want to perform. Set the value to DescribeManagedInstances. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the managed instances. Only the China \(Hangzhou\), China \(Beijing\), and China \(Shanghai\) regions are supported. |
|OsType|String|No|windows|The operating system type of the managed instance. Valid Values:

-   windows
-   linux |
|InstanceIp|String|No|192.168.2.2|The internal or public IP address of the managed instance. |
|ActivationId|String|No|4ECEEE12-56F1-4FBC-9AB1-890F7494\*\*\*\*|The ID of the activation code. |
|InstanceName|String|No|my-webapp-server|The name of the managed instance. |
|InstanceId.N|RepeatList|No|mi-hz018jrc1o0\*\*\*\*|The ID of managed instance N. Valid values of N: 1 to 50. |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1 |
|PageSize|Long|No|10|The number of entries to return on each page.

Maximum value: 50.

Default value: 10 |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instances|Array of Instance| |Details of the instances. |
|ActivationId|String|3704F543-F768-43FA-9864-897F75B3\*\*\*\*|The ID of the activation code. |
|AgentVersion|String|2.2.0.102|The version number of the Cloud Assistant client. |
|Connected|Boolean|true|Indicates whether the managed instance is connected. Valid values:

-   True: The managed instance is connected and you can manage this instance by using Cloud Assistant.
-   False: The managed instance is not connected because the managed instance is down or the Cloud Assistant client is not installed correctly. |
|Hostname|String|demo|The hostname of the managed instance. |
|InstanceId|String|mi-hz018jrc1o0\*\*\*\*|The ID of the managed instance. |
|InstanceName|String|webAPP-linux-01|The name of the managed instance. |
|InternetIp|String|40.65.\*\*. \*\*|The public IP address of the managed instance. |
|IntranetIp|String|10.0.\*\*. \*\*|The internal IP address of the managed instance. |
|InvocationCount|Long|1|The number of times that Cloud Assistant tasks were executed on the managed instance. |
|LastInvokedTime|String|2021-01-20T09:00:40Z|The time when the Cloud Assistant task was last executed. |
|MachineId|String|e03231b37ab14e53b5795ad625fc\*\*\*\*|The machine code of the managed instance. |
|OsType|String|Linux|The operating system type of the managed instance. |
|OsVersion|String|Linux\_\#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021\_x86\_64|The version information of the operating system. |
|RegistrationTime|String|2021-01-20T08:57:56Z|The time when the managed instance was registered. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|77115469-F2C5-4ECA-94F7-FA04F2FD\*\*\*\*|The ID of the request. |
|TotalCount|Long|1|The total number of queried managed instances. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeManagedInstances
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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
        <IntranetIp>10.0. **. **</IntranetIp>
        <InstanceName>webAPP-linux-01</InstanceName>
        <InternetIp>40.65. **. **</InternetIp>
        <OsType>Linux</OsType>
        <LastInvokedTime>2021-01-20T09:00:40Z</LastInvokedTime>
  </Instances>
  <TotalCount>1</TotalCount>
  <RequestId>77115469-F2C5-4ECA-94F7-FA04F2FDC8F4</RequestId>
  <PageSize>10</PageSize>
  <PageNumber>1</PageNumber>
</DescribeManagedInstancesResponse>
```

`JSON` format

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
            "IntranetIp": "10.0. **. **",
            "InstanceName": "webAPP-linux-01",
            "InternetIp": "40.65. **. **",
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

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|
|400|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|400|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

