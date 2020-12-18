# DescribeCloudAssistantStatus

You can call this operation to query whether the Cloud Assistant client is installed on one or more instances.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer automatically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCloudAssistantStatus&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCloudAssistantStatus|The operation that you want to perform. Set the value to DescribeCloudAssistantStatus. |
|InstanceId.N|RepeatList|Yes|i-bp1iudwa5b1tqa\*\*\*\*|The ID of instance N. You can specify up to 50 instance IDs in each request. Valid values of N: 1 to 50. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceCloudAssistantStatusSet|Array| |Details about the installation status of the Cloud Assistant client. |
|InstanceCloudAssistantStatus| | | |
|CloudAssistantStatus|String|true|Indicates whether the Cloud Assistant client is installed on the instance. |
|CloudAssistantVersion|String|1.0.1.395|The version number of the Cloud Assistant client. |
|InstanceId|String|i-bp1iudwa5b1tqa\*\*\*\*|The ID of the instance. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeCloudAssistantStatus
&InstanceId.1=i-bp1iudwa5b1tqa****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeCloudAssistantStatusResponse>
      <InstanceCloudAssistantStatusSet>
            <InstanceCloudAssitantStatus>
                  <InstanceId>i-bp11f7trr4hbi1****</InstanceId>
                  <CloudAssistantVersion>1.0.1.395</CloudAssistantVersion>
                  <CloudAssitantStatus>true</CloudAssitantStatus>
            </InstanceCloudAssitantStatus>
            <InstanceCloudAssitantStatus>
                  <InstanceId>i-bp1iudwa5b1tqa****</InstanceId>
                  <CloudAssistantVersion>1.0.1.395</CloudAssistantVersion>
                  <CloudAssitantStatus>true</CloudAssitantStatus>
            </InstanceCloudAssitantStatus>
      </InstanceCloudAssistantStatusSet>
</DescribeCloudAssistantStatusResponse>
```

`JSON` format

```
{
    "InstanceCloudAssistantStatusSet": {
        "InstanceCloudAssistantStatus": [
            {
                "InstanceId": "i-bp11f7trr4hbi1****",
                "CloudAssistantVersion": "1.0.1.395",
                "CloudAssitantStatus": "true"
            },
            {
                "InstanceId": "i-bp1iudwa5b1tqa****",
                "CloudAssistantVersion": "1.0.1.395",
                "CloudAssitantStatus": "true"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified instance does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

