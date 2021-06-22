# DeregisterManagedInstance

You can call this operation to deregister a managed instance. After you deregister the managed instance, you can no longer use Cloud Assistant to send commands or files to this instance.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeregisterManagedInstance&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeregisterManagedInstance|The operation that you want to perform. Set the value to DeregisterManagedInstance. |
|InstanceId|String|Yes|mi-hz01axdfas\*\*\*\*|The ID of the managed instance. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the managed instance. Only the China \(Hangzhou\), China \(Beijing\), and China \(Shanghai\) regions are supported. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Instance|Struct| |Details of the managed instance. |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F7494\*\*\*\*|The ID of the activation code. |
|AgentVersion|String|2.2.0.102|The version number of the Cloud Assistant client. |
|Hostname|String|test-Hostname|The hostname of the managed instance. |
|InstanceId|String|mi-hz01axdfas\*\*\*\*|The ID of the managed instance. |
|InstanceName|String|test-InstanceName-001|The name of the managed instance. |
|InternetIp|String|47.8.\*\*. \*\*|The public IP address of the managed instance. |
|IntranetIp|String|10.0.\*\*. \*\*|The internal IP address of the managed instance. |
|InvocationCount|Long|2|The number of times that Cloud Assistant tasks were executed on the managed instance. |
|LastInvokedTime|String|2021-01-20T09:00:40Z|The time when the Cloud Assistant task was last executed. |
|MachineId|String|e03231b37ab14e53b5795ad625fc\*\*\*\*|The machine code of the managed instance. |
|OsType|String|linux|The operating system type of the managed instance. |
|OsVersion|String|Linux\_\#38~18.04.1-Ubuntu SMP Wed Jan 6 18:26:30 UTC 2021\_x86\_64|The version information of the operating system. |
|RegistrationTime|String|2021-01-20T08:57:56Z|The time when the managed instance was registered. |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74942176|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeregisterManagedInstance
&InstanceId=mi-hz01axdfas****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

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
            <IntranetIp>10.0. **. **</IntranetIp>
            <InstanceName>test-InstanceName-001</InstanceName>
            <InternetIp>47.8. **. **</InternetIp>
            <OsType>linux</OsType>
            <LastInvokedTime>2021-01-20T09:00:40Z</LastInvokedTime>
      </Instance>
</DeregisterManagedInstanceResponse>
```

`JSON` format

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
        "IntranetIp": "10.0. **. **", 
        "InstanceName": "test-InstanceName-001", 
        "InternetIp": "47.8. **. **", 
        "OsType": "linux", 
        "LastInvokedTime": "2021-01-20T09:00:40Z"
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

