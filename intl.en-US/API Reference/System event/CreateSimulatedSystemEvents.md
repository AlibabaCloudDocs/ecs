# CreateSimulatedSystemEvents

You can call this operation to schedule simulated system events for one or more ECS instances. The simulated system events do not actually occur or affect ECS instances.

## Description

You can use the ECS console, call the [DescribeInstanceHistoryEvents](~~63962~~) operation, or use Cloud Monitor to view the scheduled simulated system events.

The following section describes the lifecycle of a simulated system event:

-   Scheduled: The status of the simulated system event is automatically changed to Scheduled after it is scheduled.
-   Executed: The status of the simulated system event is automatically changed to Executed at the scheduled time specified by the NotBefore parameter if no manual intervention is involved.
-   Canceled: The status of the simulated system event is changed to Canceled if you cancel the event by calling the [CancelSimulatedSystemEvents](~~88808~~) operation.
-   Avoided: The status of the simulated system event generated from maintenance-triggered instance restart can be changed to Avoided if you restart the instance before the scheduled time of the simulated system event. The maintenance-triggered instance restart is indicated by the SystemMaintenance.Reboot value. For more information, see [RebootInstance](~~25502~~).

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Ecs&api=CreateSimulatedSystemEvents&type=RPC&version=2014-05-26)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateSimulatedSystemEvents|The operation that you want to perform. Set the value to CreateSimulatedSystemEvents. |
|EventType|String|Yes|SystemMaintenance.Reboot|The type of the system event. Valid values:

-   SystemMaintenance.Reboot: The instance is restarted due to system maintenance.
-   SystemFailure.Reboot: The instance is restarted due to a system failure.
-   InstanceFailure.Reboot: The instance is restarted due to an instance failure.
-   SystemMaintenance.Stop: The instance is stopped due to system maintenance.
-   SystemMaintenance.Redeploy: The instance is redeployed due to system maintenance.
-   SystemFailure.Redeploy: The instance is redeployed due to a system failure.
-   SystemFailure.Stop: The instance is stopped due to a system failure.
-   InstanceFailure.Reboot: The instance is restarted due to an instance failure. |
|InstanceId.N|RepeatList|Yes|i-bp1gtjxuuvwj17zr\*\*\*\*|The ID of instance N. Valid values of N: 1 to 100. Specify multiple values in the repeated list format. |
|NotBefore|String|Yes|2018-12-01T06:32:31Z|The start time of the scheduled event execution. Specify the time in the [ISO 8601](~~25696~~) standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.

**Note:** For exception events due to system failures or instance failures, the simulated events of these exception events enter the Executing \(`Executing`\) state when the simulated events are created. The value of `NotBefore` is the time when the simulated events enter the Executed \(`Executed`\) state. |
|RegionId|String|Yes|cn-hangzhou|The region ID of the event. You can call the [DescribeRegions](~~25609~~) operation to query the most recent region list. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|EventIdSet|List|" EventId " : \[ " e-bp16helosl7v0ooj\*\*\*\* " \]|The list of simulated event IDs. |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|The ID of the request. |

## Examples

Sample requests

```
https://ecs.aliyuncs.com/?Action=CreateSimulatedSystemEvents
&EventType=SystemMaintenance.Reboot
&InstanceId.1=i-bp1gtjxuuvwj17zr****
&NotBefore=2018-12-01T06:32:31Z
&RegionId=cn-hangzhou
&<Common request parameters>
```

Sample success responses

`XML` format

```
<CreateSimulatedSystemEventsResponse>
      <EventIdSet>
            <EventId>e-bp191hqye34x****</EventId>
            <EventId>e-bp191hqye34y****</EventId>
      </EventIdSet>
          <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
</CreateSimulatedSystemEventsResponse>
```

`JSON` format

```
{
    "EventIdSet":{
        "EventId":[
            "e-bp191hqye34x****",
            "e-bp191hqye34y****"
        ]
    },
    "RequestId":"679E9056-9B75-4306-8A72-A1DF93EBEF74"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|MissingParameter|%s|The error message returned because a required parameter is not specified.|
|403|InvalidParameter|%s|The error message returned because a specified parameter is invalid.|
|403|InvalidNotBefore.Passed|%s|The error message returned because the specified value of the NotBefore parameter is earlier than the current time.|
|404|InvalidInstanceId.NotFound|%s|The error message returned because the specified instance does not exist.|
|403|SimulatedEventLimitExceeded|%s|The error message returned because the maximum number of simulated system events has been reached.|
|403|InstanceIdLimitExceeded|%s|The error message returned because the value of N in the InstanceId.N parameter is greater than 100.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

