# DeleteActivation

You can call this operation to delete an unused activation code.

## Description

The activation code to be deleted must have not been used to register managed instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DeleteActivation&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteActivation|The operation that you want to perform. Set the value to DeleteActivation. |
|ActivationId|String|Yes|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the activation code. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the activation code. Only the China \(Hangzhou\), China \(Beijing\), and China \(Shanghai\) regions are supported. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Activation|Struct| |Details of the activation code and its usage information. |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the activation code. |
|CreationTime|String|2021-01-20T06:00:00Z|The time when the task was created. |
|DeregisteredCount|Integer|0|The number of instances that were deregistered. |
|Description|String|This is description.|The description of the activation code. |
|InstanceCount|Integer|1|The maximum number of times that the activation code can be used to register managed instances. |
|InstanceName|String|test-InstanceName|The default instance name prefix. |
|IpAddressRange|String|0.0.0.0/0|The IP addresses of hosts that are allowed to use the activation code. |
|RegisteredCount|Integer|0|The number of instances that were registered by using the activation code. |
|TimeToLiveInHours|Long|4|The validity period of the activation code. Unit: hours. |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74942176|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DeleteActivation
&ActivationId=4ECEEE12-56F1-4FBC-9AB1-890F1234****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DeleteActivationResponse>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F74942176</RequestId>
      <Activation>
            <InstanceName>test-InstanceName</InstanceName>
            <DeregisteredCount>0</DeregisteredCount>
            <InstanceCount>1</InstanceCount>
            <Description>This is description. </Description>
            <CreationTime>2021-01-20T06:00:00Z</CreationTime>
            <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
            <RegisteredCount>0</RegisteredCount>
            <TimeToLiveInHours>4</TimeToLiveInHours>
            <IpAddressRange>0.0.0.0/0</IpAddressRange>
      </Activation>
</DeleteActivationResponse>
```

`JSON` format

```
{
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F74942176", 
    "Activation": {
        "InstanceName": "test-InstanceName", 
        "DeregisteredCount": "0", 
        "InstanceCount": "1", 
        "Description": "This is description.", 
        "CreationTime": "2021-01-20T06:00:00Z", 
        "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****", 
        "RegisteredCount": "0", 
        "TimeToLiveInHours": "4", 
        "IpAddressRange": "0.0.0.0/0"
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

