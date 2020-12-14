# DescribeTasks

You can call this operation to query the progress of one or more asynchronous tasks.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeTasks&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeTasks|The operation that you want to perform. Set the value to DescribeTasks. |
|RegionId|String|Yes|cn-hangzhou|The region ID. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1. Default value: 1. |
|PageSize|Integer|No|2|The number of entries to return on each page. Valid values: 1 to 100. Default value: 10. |
|TaskIds|String|No|t-bp1hvgwromzv32iq\*\*\*\*,t-bp179lofu2pv768w\*\*\*\*|The IDs of the tasks. You can specify up to 100 tasks at a time. Separate multiple tasks IDs with commas \(,\). |
|TaskAction|String|No|ImportImage|The name of the operation that generates the task. Valid values:

-   ImportImage
-   ExportImage
-   RedeployInstance |
|TaskStatus|String|No|Finished|The status of the task. Valid values:

-   Finished
-   Processing
-   Failed

This parameter is empty by default.

**Note:** The system only retrieves tasks in the Finished, Processing, and Failed states, and ignores other values. |
|StartTime|String|No|2015-11-23T15:10:00Z|The beginning of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EndTime|String|No|2015-11-23T15:16:00Z|The end of the time range to query. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|2|The number of entries returned per page. |
|RegionId|String|cn-hangzhou|The region ID. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TaskSet|Array of Task| |Details about the tasks. |
|Task| | | |
|CreationTime|String|2015-11-24T12:50Z|The time when the task was created. |
|FinishedTime|String|2015-11-24T12:50Z|The time when the task was complete. |
|SupportCancel|String|true|Indicates whether the task can be canceled. |
|TaskAction|String|IMPORT\_IMAGE|The name of the task. |
|TaskId|String|t-bp1hvgwromzv32iq\*\*\*\*|The ID of the task. |
|TaskStatus|String|Finished|The status of the task. |
|TotalCount|Integer|2|The total number of entries returned. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeTasks
&RegionId=cn-hangzhou
&PageNumber=1
&PageSize=2
&TaskIds=t-bp1hvgwromzv32iq****
&TaskAction=ImportImage
&TaskStatus=Finished
&StartTime=2015-11-23T15:10:00Z
&EndTime=2015-11-23T15:16:00Z
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeTasksResponse>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <PageSize>2</PageSize>
    <RegionId>cn-hangzhou</RegionId>
    <RequestId>E5C82807-5588-4661-9A96-350B206A7623</RequestId>
    <TaskSet>
        <Task>
            <CreationTime>2015-11-24T12:50Z</CreationTime>
            <FinishedTime>2015-11-24T12:50Z</FinishedTime>
            <SupportCancel>true</SupportCancel>
            <TaskAction>IMPORT_IMAGE</TaskAction>
            <TaskStatus>Finished</TaskStatus>
            <TaskId>t-bp1hvgwromzv32iq****</TaskId>
        </Task>
        <Task>
            <CreationTime>2015-11-23T15:10Z</CreationTime>
            <FinishedTime>2015-11-23T15:16Z</FinishedTime>
            <SupportCancel>true</SupportCancel>
            <TaskAction>IMPORT_IMAGE</TaskAction>
            <TaskStatus>Finished</TaskStatus>
            <TaskId>t-bp179lofu2pv768w****</TaskId>
        </Task>
    </TaskSet>
</DescribeTasksResponse>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 2,
    "PageSize": 2,
    "RegionId": "cn-hangzhou",
    "TaskSet": [
        {
            "Task": [
                {
                    "CreationTime": "2015-11-24T12:50Z",
                    "FinishedTime": "2015-11-24T12:50Z",
                    "SupportCancel": true,
                    "TaskAction": "ImportImage",
                    "TaskStatus": "Finished",
                    "TaskId": "t-bp1hvgwromzv32iq****"
                },
                {
                    "CreationTime": "2015-11-23T15:10Z",
                    "FinishedTime": "2015-11-23T15:16Z",
                    "SupportCancel": true,
                    "TaskAction": "ImportImage",
                    "TaskStatus": "Finished",
                    "TaskId": "t-bp179lofu2pv768w****"
                }
            ]
        }
    ],
    "RequestId": "F746C690-D9EA-4F87-AF31-8E1910FAB541"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|The error message returned because the RegionId parameter is not specified.|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|The error message returned because the specified RegionId parameter does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

