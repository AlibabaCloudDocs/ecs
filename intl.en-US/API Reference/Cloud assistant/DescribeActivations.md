# DescribeActivations

You can call this operation to query the created activation codes and the usage of the activation codes.

****

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeActivations&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeActivations|The operation that you want to perform. Set the value to DescribeActivations. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the activation code. Only the China \(Hangzhou\), China \(Beijing\), and China \(Shanghai\) regions are supported. |
|ActivationId|String|No|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the activation code. |
|InstanceName|String|No|test-InstanceName|The default instance name prefix. |
|PageNumber|Long|No|1|The page number of the page to return.

Pages start from page 1.

Default value: 1 |
|PageSize|Long|No|10|The number of entries to return on each page.

Maximum value: 50.

Default value: 10 |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|ActivationList|Array of Activation| |Details of the activation codes and their usage information. |
|ActivationId|String|4ECEEE12-56F1-4FBC-9AB1-890F1234\*\*\*\*|The ID of the activation code. |
|CreationTime|String|2021-01-20T06:00:00Z|The time when the task was created. |
|DeregisteredCount|Integer|1|The number of instances that were deregistered. |
|Description|String|This is description.|The description of the activation code. |
|Disabled|Boolean|false|Indicates whether the activation code is disabled. |
|InstanceCount|Integer|1|The maximum number of times that the activation code were used to register managed instances. |
|InstanceName|String|test-InstanceName|The default instance name prefix. |
|IpAddressRange|String|0.0.0.0/0|The IP addresses of hosts that are allowed to use the activation code. |
|RegisteredCount|Integer|1|The number of instances that were registered by using the activation code. |
|TimeToLiveInHours|Long|4|The validity period of the activation code. Unit: hours. |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|10|The number of entries returned per page. |
|RequestId|String|4ECEEE12-56F1-4FBC-9AB1-890F74625134|The ID of the request. |
|TotalCount|Long|1|The total number of entries returned. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeActivations
&RegionId=cn-hangzhou
&ActivationId=4ECEEE12-56F1-4FBC-9AB1-890F1234****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeActivationsResponse>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>4ECEEE12-56F1-4FBC-9AB1-890F74942176</RequestId>
      <PageNumber>1</PageNumber>
      <ActivationList>
            <InstanceName>test-InstanceName</InstanceName>
            <DeregisteredCount>1</DeregisteredCount>
            <InstanceCount>1</InstanceCount>
            <Description>This is description. </Description>
            <CreationTime>2021-01-20T06:00:00Z</CreationTime>
            <ActivationId>4ECEEE12-56F1-4FBC-9AB1-890F1234****</ActivationId>
            <RegisteredCount>1</RegisteredCount>
            <TimeToLiveInHours>4</TimeToLiveInHours>
            <Disabled>false</Disabled>
            <IpAddressRange>0.0.0.0/0</IpAddressRange>
      </ActivationList>
</DescribeActivationsResponse>
```

`JSON` format

```
{
    "TotalCount": "1", 
    "PageSize": "10", 
    "RequestId": "4ECEEE12-56F1-4FBC-9AB1-890F74942176", 
    "PageNumber": "1", 
    "ActivationList": [
        {
            "InstanceName": "test-InstanceName", 
            "DeregisteredCount": "1", 
            "InstanceCount": "1", 
            "Description": "This is description.", 
            "CreationTime": "2021-01-20T06:00:00Z", 
            "ActivationId": "4ECEEE12-56F1-4FBC-9AB1-890F1234****", 
            "RegisteredCount": "1", 
            "TimeToLiveInHours": "4", 
            "Disabled": "false", 
            "IpAddressRange": "0.0.0.0/0"
        }
    ]
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was sent. Try again later.|
|400|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned because the specified PageNumber parameter is invalid.|
|400|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned because the specified PageSize parameter is invalid.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

