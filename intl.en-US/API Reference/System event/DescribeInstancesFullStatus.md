# DescribeInstancesFullStatus

You can call this operation to query the full status information of one or more ECS instances. The full status information includes the instance status and the status of an instance system event. The instance status is the lifecycle status of an instance. The status of an instance system event is the health status of a maintenance event.

## Description

The response includes the instance status and the instance system events in the Scheduled state.

If a period is specified, all the events within the period are queried.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=DescribeInstancesFullStatus&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeInstancesFullStatus|The operation that you want to perform. Set the value to DescribeInstancesFullStatus. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the instance. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |
|InstanceId.N|RepeatList|No|i-bp67acfmxazb4p\*\*\*\*|The ID of instance N. Valid values of N: 1 to 100. Specify multiple values in the repeated list format. |
|EventId.N|RepeatList|No|e-bp1hygp5b04o56l0\*\*\*\*|The ID of system event N. Valid values of N: 1 to 100. Specify multiple values in the repeated list format. |
|Status|String|No|Running|The lifecycle status of the instance. Valid values:

-   Starting
-   Running
-   Stopped |
|HealthStatus|String|No|Maintaining|The health status of the instance. Valid values:

-   Impaired: The instance is impaired.
-   Warning: The instance performance may be degraded due to maintenance or technical issues.
-   Maintaining: The instance is undergoing maintenance.
-   Initializing: The instance is being initialized.
-   InsufficientData: The status cannot be determined due to insufficient data.
-   NotApplicable: The parameter is not applicable.

All the values are case-sensitive. |
|InstanceEventType.N|RepeatList|No|InstanceExpiration.Stop|The type of system event N. Valid values of N: 1 to 30. Specify multiple values in the repeated list format. Valid values:

-   SystemMaintenance.Reboot: The instance is restarted due to system maintenance.
-   SystemFailure.Reboot: The instance is restarted due to a system failure.
-   InstanceFailure.Reboot: The instance is restarted due to an instance failure.
-   InstanceExpiration.Stop: The instance is stopped due to subscription expiration.
-   InstanceExpiration.Delete: The instance is released due to subscription expiration.
-   AccountUnbalanced.Stop: The pay-as-you-go instance is stopped due to overdue payments.
-   AccountUnbalanced.Delete: The pay-as-you-go instance is released due to overdue payments. |
|EventType|String|No|InstanceExpiration.Stop|The type of the system event. This parameter takes effect only when the InstanceEventType.N parameter is not specified. Valid values:

-   SystemMaintenance.Reboot: The instance is restarted due to system maintenance.
-   SystemFailure.Reboot: The instance is restarted due to a system failure.
-   InstanceFailure.Reboot: The instance is restarted due to an instance failure.
-   InstanceExpiration.Stop: The instance is stopped due to subscription expiration.
-   InstanceExpiration.Delete: The instance is released due to subscription expiration.
-   AccountUnbalanced.Stop: The pay-as-you-go instance is stopped due to overdue payments.
-   AccountUnbalanced.Delete: The pay-as-you-go instance is released due to overdue payments. |
|NotBefore.Start|String|No|2017-12-07T00:00:00Z|The start time of the scheduled event execution. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|NotBefore.End|String|No|2017-11-30T00:00:00Z|The end time of the scheduled event execution. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EventPublishTime.Start|String|No|2017-11-30T00:00:00Z|The start time of the period during which a system event is published. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|EventPublishTime.End|String|No|2017-12-07T00:00:00Z|The end time of the period during which a system event is published. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. |
|PageNumber|Integer|No|1|The number of the page to return. Pages start from page 1.

Default value: 1. |
|PageSize|Integer|No|10|The number of entries to return on each page. Valid values: 1 to 100.

Default value: 10. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|InstanceFullStatusSet|Array of InstanceFullStatusType| |Details about the instance full status data. |
|InstanceFullStatusType| | | |
|HealthStatus|Struct| |The health status of the instance. |
|Code|Integer|64|The code of the health status. |
|Name|String|Warning|The name of the health status. |
|InstanceId|String|i-bp67acfmxazb4p\*\*\*\*|The ID of the instance. |
|ScheduledSystemEventSet|Array of ScheduledSystemEventType| |Details about the scheduled system events. |
|ScheduledSystemEventType| | | |
|EventCycleStatus|Struct| |The status of the system event. |
|Code|Integer|24|The code of the system event status. |
|Name|String|Scheduled|The name of the system event status. |
|EventId|String|e-bp1hygp5b04o56l0\*\*\*\*|The ID of the instance event. |
|EventPublishTime|String|2017-11-30T06:32:31Z|The time when the system event was published. The time is displayed in UTC. |
|EventType|Struct| |The type of the system event. Valid values: |
|Code|Integer|1|The code of the system event type. |
|Name|String|SystemMaintenance.Reboot|The name of the system event type. |
|ExtendedAttribute|Struct| |The extended attribute of system events for instances that have local disks attached. |
|Device|String|/dev/vdb|The device name of the local disk. |
|DiskId|String|d-bp67acfmxazb4p\*\*\*\*|The ID of the local disk. |
|InactiveDisks|Array of InactiveDisk| |Details about the inactive cloud disks or local disks that have been released but must be removed. |
|InactiveDisk| | | |
|CreationTime|String|2018-07-27T13:53:25Z|The time when the disk was created. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|DeviceCategory|String|cloud\_ssd|The category of the disk. Valid values:

-   cloud: basic disk.
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   local\_ssd\_pro: I/O intensive local disk
-   local\_hdd\_pro: throughput intensive local disk
-   ephemeral: retired local disk
-   ephemeral\_ssd: retired local SSD |
|DeviceSize|String|80|The size of the disk. Unit: GiB. |
|DeviceType|String|system|The type of the disk. Valid values:

-   system: system disk
-   data: data disk |
|ReleaseTime|String|2019-07-27T13:53:25Z|The time when the disk was released. The time follows the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time is displayed in UTC. |
|ImpactLevel|String|100|The level of the system event impact. |
|NotBefore|String|2017-12-07T00:00:00Z|The scheduled execution time of the system event. The time is displayed in UTC. |
|Reason|String|A simulated event.|The reason for scheduling the system event. |
|Status|Struct| |The lifecycle status of the instance. |
|Code|Integer|1|The code of the instance lifecycle status. |
|Name|String|Running|The name of the instance lifecycle status. |
|PageNumber|Integer|1|The page number of the returned page. |
|PageSize|Integer|1|The number of entries returned per page. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |
|TotalCount|Integer|2|The total number of the returned entries. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=DescribeInstancesFullStatus
&RegionId=cn-hangzhou
&InstanceId.1=i-bp67acfmxazb4p****
&EventId.1=e-bp1hygp5b04o56l0****
&Status=Running
&HealthStatus=Maintaining
&InstanceEventType.1=InstanceExpiration.Stop
&EventType=InstanceExpiration.Stop
&NotBefore.Start=2017-12-07T00:00:00Z
&NotBefore.End=2017-11-30T00:00:00Z
&EventPublishTime.Start=2017-11-30T00:00:00Z
&EventPublishTime.End=2017-12-07T00:00:00Z
&PageNumber=1
&PageSize=1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<DescribeInstancesFullStatusResponse>
      <TotalCount>1</TotalCount>
      <RequestId>7EBCB534-1CE5-46E7-92A6-507B1654CC03</RequestId>
      <PageSize>10</PageSize>
      <PageNumber>1</PageNumber>
      <InstanceFullStatusSet>
            <InstanceFullStatusType>
                  <Status>
                        <Code>1</Code>
                        <Name>Running</Name>
                  </Status>
                  <InstanceId>i-bp19cx17f2yx****</InstanceId>
                  <HealthStatus>
                        <Code>64</Code>
                        <Name>Warning</Name>
                  </HealthStatus>
                  <ScheduledSystemEventSet>
                        <ScheduledSystemEventType>
                              <EventCycleStatus>
                                    <Code>24</Code>
                                    <Name>Scheduled</Name>
                              </EventCycleStatus>
                              <EventPublishTime>2020-04-24T07:09:37Z</EventPublishTime>
                              <EventType>
                                    <Code>65</Code>
                                    <Name>SystemFailure.Reboot</Name>
                              </EventType>
                              <ExtendedAttribute></ExtendedAttribute>
                              <EventId>e-bp1hygp5b04o56l0****</EventId>
                              <NotBefore>2020-04-24T10:32:31Z</NotBefore>
                              <Reason>A simulated event. </Reason>
                        </ScheduledSystemEventType>
                  </ScheduledSystemEventSet>
            </InstanceFullStatusType>
      </InstanceFullStatusSet>
</DescribeInstancesFullStatusResponse>
```

`JSON` format

```
{
    "TotalCount": 1,
    "RequestId": "7EBCB534-1CE5-46E7-92A6-507B1654CC03",
    "PageSize": 10,
    "PageNumber": 1,
    "InstanceFullStatusSet": {
        "InstanceFullStatusType": [
            {
                "Status": {
                    "Code": 1,
                    "Name": "Running"
                },
                "InstanceId": "i-bp19cx17f2yx****",
                "HealthStatus": {
                    "Code": 64,
                    "Name": "Warning"
                },
                "ScheduledSystemEventSet": {
                    "ScheduledSystemEventType": [
                        {
                            "EventCycleStatus": {
                                "Code": 24,
                                "Name": "Scheduled"
                            },
                            "EventPublishTime": "2020-04-24T07:09:37Z",
                            "EventType": {
                                "Code": 65,
                                "Name": "SystemFailure.Reboot"
                            },
                            "ExtendedAttribute": {},
                            "EventId": "e-bp1hygp5b04o56l0****",
                            "NotBefore": "2020-04-24T10:32:31Z",
                            "Reason": "A simulated event."
                        }
                    ]
                }
            }
        ]
    }
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|InvalidParameter.TimeEndBeforeStart|%s|The error message returned because the specified parameter is invalid. Check whether the end time is earlier than the start time.|
|403|OperationDenied.NotInWhiteList|%s|The error message returned because you are not authorized to perform this operation. Try again when you are in the whitelist.|
|403|InstanceIdLimitExceeded|%s|The error message returned because the value set for N in the InstanceId.N parameter is more than 100.|
|403|EventIdLimitExceeded|%s|The error message returned because more than 100 system event IDs are specified.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

