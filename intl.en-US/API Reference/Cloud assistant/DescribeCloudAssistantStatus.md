# DescribeCloudAssistantStatus

You can call this operation to query whether the Cloud Assistant client is installed on one or more instances. If the Cloud Assistant client is installed, the system queries the total number of Cloud Assistant commands, the number of commands that are being run, and the latest time when a command was run.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeCloudAssistantStatus&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCloudAssistantStatus|The operation that you want to perform. Set the value to DescribeCloudAssistantStatus. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId.N|RepeatList|No|i-bp1iudwa5b1tqa\*\*\*\*|The ID of instance N. You can specify up to 100 instance IDs in each request. Valid values of N: 1 to 100. |
|OSType|String|No|Windows|The operating system of the instance. Valid values:

-   Windows
-   Linux |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page.

Maximum value: 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceCloudAssistantStatusSet|Array of InstanceCloudAssistantStatus| |Details about the installation status of the Cloud Assistant client. |
|InstanceCloudAssistantStatus| | | |
|ActiveTaskCount|Long|0|The number of commands that are being run. |
|CloudAssistantStatus|String|true|Indicates whether the Cloud Assistant client is installed on the instance. |
|CloudAssistantVersion|String|2.2.0.106|The version number of the Cloud Assistant client. |
|InstanceId|String|i-bp1iudwa5b1tqa\*\*\*\*|The ID of the instance. |
|InvocationCount|Long|2|The total number of commands that have been run. |
|LastInvokedTime|String|2021-03-15T08:00:00Z|The latest time when the command was run. |
|OSType|String|Linux|The operating system of the instance. Valid values:

-   Windows
-   Linux |
|PageNumber|Long|1|The page number of the returned page. |
|PageSize|Long|1|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Long|1|The total number of instances. |

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

`JSON` format

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

## Error codes

|HTTP|Error code|Error message|Description|
|----|----------|-------------|-----------|
|400|RegionId.ApiNotSupported|The api is not supported in this region.|The error message returned because this API operation cannot be called in the specified region. Check whether the specified RegionId parameter is valid.|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned because an error occurred when the request was being sent. Try again later.|
|404|InvalidInstance.NotFound|The specified instance does not exist.|The error message returned because the specified InstanceId parameter does not exist.|
|403|InstanceIds.ExceedLimit|The number of instance IDs exceeds the upper limit.|The error message returned because the maximum number of instances has been reached.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

