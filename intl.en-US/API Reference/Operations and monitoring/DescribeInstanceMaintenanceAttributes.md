# DescribeInstanceMaintenanceAttributes

You can call this operation to query the maintenance properties of an instance.

## Description

This operation is used to query the specified maintenance policy of an instance, which contains the following two major maintenance properties:

-   Maintenance window: the time period that you specify for maintenance.
-   Maintenance action: the policy that you specify in response to instance shutdown.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceMaintenanceAttributes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstanceMaintenanceAttributes|The operation that you want to perform. Set the value to DescribeInstanceMaintenanceAttributes. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId.N|RepeatList|No|i-bp67acfmxazb4p\*\*\*\*|The ID of instance N. Valid values of N: 1 to 100. |
|PageNumber|Long|No|1|The number of the page to return.

Pages start from page 1.

Default value: 1. |
|PageSize|Long|No|10|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|MaintenanceAttributes|Array of MaintenanceAttribute| |Details of the maintenance properties. |
|MaintenanceAttribute| | | |
|ActionOnMaintenance|Struct| |The property of the maintenance action of the instance. |
|DefaultValue|String|AutoRecover|The default maintenance action. |
|SupportedValues|List|"SupportedValue": \["Stop", "AutoRecover"\]|Details of the supported maintenance actions. |
|Value|String|Stop|The current maintenance action. Valid values:

-   Stop: The instance is shutdown.
-   AutoRecover: The instance is automatically recovered.
-   AutoRedeploy: Failover is performed, which may cause damage to the data disks attached to the instance. |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|MaintenanceWindows|Array of MaintenanceWindow| |Details of the maintenance window. |
|MaintenanceWindow| | | |
|EndTime|String|18:00:00|The end time of the maintenance window. |
|StartTime|String|02:00:00|The start time of the maintenance window. |
|NotifyOnMaintenance|Boolean|false|Indicates whether an event notification was sent before instance shutdown. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|10|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|100|The total number of queried maintenance properties. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com?Action=DescribeInstanceMaintenanceAttributes
&InstanceId.1=i-bp67acfmxazb4p****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstanceMaintenanceAttributesResponse>
      <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <TotalCount>100</TotalCount>
      <InstanceMaintenanceAttributes>
            <InstanceMaintenanceAttribute>
                  <InstanceId>i-bp67acfmxazb4ph***</InstanceId>
                  <NotifyOnMaintenance>false</NotifyOnMaintenance>
                  <MaintenanceWindows>
                        <MaintenanceWindow>
                              <StartTime>02:00:00</StartTime>
                              <EndTime>18:00:00</EndTime>
                        </MaintenanceWindow>
                  </MaintenanceWindows>
                  <ActionOnMaintenance>
                        <Value>Stop</Value>
                        <DefaultValue>AutoRecover</DefaultValue>
                        <SupportedValues>
                              <SupportedValue>Stop</SupportedValue>
                              <SupportedValue>AutoRecover</SupportedValue>
                        </SupportedValues>
                  </ActionOnMaintenance>
            </InstanceMaintenanceAttribute>
      </InstanceMaintenanceAttributes>
</DescribeInstanceMaintenanceAttributesResponse>
```

`JSON` format

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 100,
    "InstanceMaintenanceAttributes": {
        "InstanceMaintenanceAttribute": [{
            "InstanceId": "i-bp67acfmxazb4ph***",
            "NotifyOnMaintenance": false,
            "MaintenanceWindows ": {
                "MaintenanceWindow": [{
                    "StartTime": "02:00:00",
                    "EndTime": "18:00:00"
                }]
            },
            "ActionOnMaintenance": {
                "Value": "Stop",
                "DefaultValue": "AutoRecover",
                "SupportedValues": {
                    "SupportedValue": ["Stop", "AutoRecover"]
                }
            }
        }]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|InstanceIdLimitExceeded|%s|The error message returned because the value of N in the InstanceId.N parameter is greater than 100.|
|403|OperationDenied.NotInWhiteList|%s|The error message returned because you are not authorized to perform this operation. Try again when you are authorized.|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|The error message returned because the specified InstanceId parameter does not exist. Check whether the instance ID is correct.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

