# ModifyInstanceMaintenanceAttributes

You can call this operation to modify the maintenance properties of one or more instances.

## Description

This operation is used to modify the maintenance policy of an instance. The maintenance policy consists of the following maintenance properties:

-   Maintenance window: the time period that you specify for maintenance.
-   Maintenance action: the policy that you specify in response to instance shutdown.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceMaintenanceAttributes&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ModifyInstanceMaintenanceAttributes|The operation that you want to perform. Set the value to ModifyInstanceMaintenanceAttributes. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId.N|RepeatList|No|i-bp67acfmxazb4ph\*\*\*\*|The ID of instance N. Valid values of N: 1 to 100. |
|MaintenanceWindow.N.StartTime|String|No|02:00:00|The start time of maintenance window N. The time must be on the hour at exactly 0 minute and 0 second. The MaintenanceWindow.N.StartTime and MaintenanceWindow.N.EndTime parameters must be specified at the same time. The MaintenanceWindow.N.Endtime value must be 1 to 23 hours later than the MaintenanceWindow.N.StartTime value. Specify the time in the `HH:mm:ss` format. The time must be in UTC+8. Set the value of N to 1. |
|MaintenanceWindow.N.EndTime|String|No|18:00:00|The end time of maintenance window N. The time must be on the hour at exactly 0 minute and 0 second. The MaintenanceWindow.N.StartTime and MaintenanceWindow.N.EndTime parameters must be specified at the same time. The MaintenanceWindow.N.Endtime value must be 1 to 23 hours later than the MaintenanceWindow.N.StartTime value. Specify the time in the `HH:mm:ss` format. The time must be in UTC+8. Set the value of N to 1. |
|ActionOnMaintenance|String|No|AutoRecover|The maintenance action. Valid values:

-   Stop: stops the instance.
-   AutoRecover: automatically recovers the instance.
-   AutoRedeploy: fails the instance over, which may cause damage to the data disks attached to the instance. |
|NotifyOnMaintenance|Boolean|No|false|Specifies whether to send an event notification before instance shutdown. Valid values:

-   True: sends an event notification.
-   False: does not send an event notification.

Default value: false. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com?Action=ModifyInstanceMaintenanceAttributes
&InstanceId.1=i-bp67acfmxazb4ph****
&ActionOnMaintenance=AutoRecover
&<Common request parameters>
```

Sample success responses

`XML` format

```
<ModifyInstanceMaintenanceAttributesResponse>    
    <RequestId>E69FF3CC-94DD-42EF-8836-F33C45EDF9945ED</RequestId>
<ModifyInstanceMaintenanceAttributesResponse>
```

`JSON` format

```
{
    "RequestId": "E69FF3CC-94DD-42EF-8836-F33C45EDF9945ED"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidInstanceId.NotFound|%s|The error message returned because the specified instance does not exist.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|OperationDenied.NotInWhiteList|%s|The error message returned because you are not authorized to perform this operation. Try again when you are authorized.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

