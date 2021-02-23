# DescribeAutoProvisioningGroupHistory

You can call this operation to query the scheduling tasks of an auto provisioning group.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeAutoProvisioningGroupHistory&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAutoProvisioningGroupHistory|The operation that you want to perform. Set the value to DescribeAutoProvisioningGroupHistory. |
|AutoProvisioningGroupId|String|Yes|apg-bp67acfmxazb4p\*\*\*\*|The ID of the auto provisioning group. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the auto provisioning group. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|5|The number of entries to return on each page. Maximum value: 100.

Default value: 10. |
|StartTime|String|No|2019-04-01T15:10:20Z|The beginning of the time range of the queried data. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EndTime|String|No|2019-06-20T15:10:20Z|The end of the time range of the queried data. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutoProvisioningGroupHistories|Array| |An array consisting of AutoProvisioningGroupHistory data. |
|AutoProvisioningGroupHistory| | | |
|ActivityDetails|Array| |An array consisting of ActivityDetail data. |
|ActivityDetail| | | |
|Detail|String|New ECS instances "i-bp67acfmxazb4p\*\*\*\*, i-bp67acfmxazb5p\*\*\*\*" created.|The execution details of instance creation performed by the single scheduling task. |
|Status|String|Successful|The execution status of instance creation performed by the single scheduling task. Valid values:

-   Successful: Instances are created.
-   Failed: Instances failed to be created.
-   InProgress: Instances are being created.
-   Warning: Partial instances are created. |
|LastEventTime|String|2019-04-01T15:10:20Z|The execution time of the last instance creation performed by the single scheduling task. |
|StartTime|String|2019-04-01T15:10:20Z|The start time of executing the single scheduling task. |
|Status|String|Success|The execution status of the single scheduling task. Valid values:

-   prepare: The scheduling task is being executed.
-   success: The scheduling task is executed.
-   failed: The scheduling task failed to be executed. |
|TaskId|String|apg-task-bp67acfmxazb4p\*\*\*\*|The ID of the scheduling task. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|B48A12CD-1295-4A38-A8F0-0E92C937\*\*\*\*|The ID of the request. |
|TotalCount|Integer|10|The number of queried scheduling tasks in the auto provisioning group. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeAutoProvisioningGroupHistory
&AutoProvisioningGroupId=apg-bp67acfmxazb4p****
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeAutoProvisioningGroups>
      <PageNumber>1</PageNumber>
      <TotalCount>1</TotalCount>
      <PageSize>10</PageSize>
      <RequestId>BA55349F-6E36-4E64-964B-419515D1****</RequestId>
      <AutoProvisioningGroupHistories>
            <AutoProvisioningGroupHistory>
                  <Status>success</Status>
                  <ActivityDetails>
                        <ActivityDetail>
                              <Detail>New ECS instances i-bp67acfmxazb4ph***, i-bp67acfmxazb4pi*** created. </Detail>
                              <Status>Successful</Status>
                        </ActivityDetail>
                  </ActivityDetails>
                  <LastEventTime>2019-06-17T08:48:00Z</LastEventTime>
                  <StartTime>2019-06-17T08:47:52Z</StartTime>
                  <TaskId>apg-task-uf66bqtabg10wcf6****</TaskId>
            </AutoProvisioningGroupHistory>
      </AutoProvisioningGroupHistories>
</DescribeAutoProvisioningGroups>
```

`JSON` format

```
{
    "PageNumber": 1,
    "TotalCount": 1,
    "PageSize": 10,
    "RequestId": "BA55349F-6E36-4E64-964B-419515D1****",
    "AutoProvisioningGroupHistories": {
        "AutoProvisioningGroupHistory": [
            {
                "Status":"success",
                "ActivityDetails": {
                    "ActivityDetail": [
                        {
                            "Detail": "New ECS instances i-bp67acfmxazb4ph***, i-bp67acfmxazb4pi*** created.",
                            "Status": "Successful"
                        }
                    ]
                },
                "LastEventTime": "2019-06-17T08:48:00Z",
                "StartTime": "2019-06-17T08:47:52Z",
                "TaskId": "apg-task-uf66bqtabg10wcf6****"
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|Forbidden.RAM|User not authorized to operate on the specified resource, or this API doesn't support RAM.|The error message returned because you are not authorized to manage this resource, or this API operation does not support RAM roles.|
|400|MissingParamter.RegionId|The regionId should not be null.|The error message returned because the RegionId parameter is not specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

