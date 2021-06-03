---
keyword: [event, system event, automation, message notification, ECS]
---

# Overview

System events are scheduled or unexpected operations and maintenance events that affect the running status of Elastic Compute Service \(ECS\) instances. System events occur when ECS instances are restarted, stopped, or released due to actions such as update and maintenance, invalid operations, system failure, hardware or software failure, subscription expiration, or overdue payments.

## Differences between routine maintenance and system events

Alibaba Cloud provides routine maintenance for underlying physical servers and prevent potential failures to improve the reliability, performance, and security of ECS instances. When a failure or threat is detected in a physical server, ECS performs hot migration to migrate ECS instances from the at-risk server to a healthy server and ensure that the instances continue to run normally. These operations are called routine maintenance. During routine maintenance, the system does not send notifications, and the instances are not affected.

For system events, ECS sends you notifications that contain information such as solutions and event cycles. For system O&M events, ECS notifies you of the impacts of the system events on your instances and the scheduled execution points in time. You can back up data in a timely manner and make preparations at the application layer before you handle system events. You can also query system events that were handled within the last week and obtain data for troubleshooting and analysis.

## Limits

Retired instance families do not support the system event feature. For more information, see [Retired instance types](/intl.en-US/Instance/Instance type families/Retired instance types.md).

## System event types

The following table describes the types, impacts, and recommended solutions of ECS system events.

|Impact|Event type|Parameter|Recommended solution|
|:-----|:---------|:--------|--------------------|
|Instance restart|Instance restart due to scheduled system maintenance|SystemMaintenance.Reboot|Select an appropriate point in time during the user operation window to perform the following operations: 1.  Restart the instance.

**Note:** You must restart the instance by using the ECS console or by calling the RebootInstance operation. You cannot restart the instance from within the instance. For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instances/Restart an instance.md).

2.  Divert traffic away from the instance that is to be restarted or remove the instance from the backend server group of the Server Load Balancer \(SLB\) instance to avoid impacts on your business.
3.  Optional. Create snapshots for the disks attached to the instance to back up data. |
|Unexpected instance restart|Instance restart due to an unexpected system error|SystemFailure.Reboot|For more information, see [Automatic recovery events of instances](/intl.en-US/Deployment & Maintenance/System events/Automatic recovery events of instances.md).|
|Instance restart due to an unexpected instance error|InstanceFailure.Reboot|If you receive an event notification during or after the instance restart, we recommend that you: -   View system logs and screenshots to troubleshoot the failure and find the causes of the instance failure to prevent further failures. For more information, see [System logs and screenshots](/intl.en-US/Deployment & Maintenance/Troubleshoot operation errors/System logs and screenshots.md).
-   Check whether the instance and applications have recovered. |
|Instance redeployment|Instance redeployment due to scheduled system maintenance|SystemMaintenance.Redeploy|For more information, see [Redeploy an instance equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Redeploy an instance equipped with local disks.md).|
|Instance redeployment due to a system error|SystemFailure.Redeploy|For more information, see [Redeploy an instance equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Redeploy an instance equipped with local disks.md).|
|Instance stop|Subscription instance: instance stop upon expiration|InstanceExpiration.Stop|Renew the instance. For more information, see [Renewal overview](/intl.en-US/Pricing/Renew instances/Renewal overview.md).|
|Pay-as-you-go instance: instance stop due to overdue payments|AccountUnbalanced.Stop|We recommend that you maintain a sufficient balance within your payment account to prevent instances from being stopped. |
|Instance release|Subscription instance: instance release after expiration|InstanceExpiration.Delete|Renew the instance. For more information, see [Renewal overview](/intl.en-US/Pricing/Renew instances/Renewal overview.md).|
|Pay-as-you-go instance: instance release due to overdue payments|AccountUnbalanced.Delete|We recommend that you maintain a sufficient balance within your payment account to prevent instances from being stopped. |
|Instance release|Instance release due to a creation failure|SystemFailure.Delete|For more information, see [System event of instance creation failure](/intl.en-US/Deployment & Maintenance/System events/System event of instance creation failure.md).|
|Impact on disk performance|Severe impact on disk performance|Stalled|At the application layer, isolate the read and write operations on the disk or temporarily remove the ECS instance from the backend server group of the SLB instance.|
|Damage to local disks|Damage to local disks|ErrorDetected|For more information, see [Overview of system events on ECS instances equipped with local disks](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Overview of system events on ECS instances equipped with local disks.md).|
|Instance restart and isolation of damaged local disks|Instance restart and isolation of damaged local disks due to scheduled system maintenance|SystemMaintenance.RebootAndIsolateErrorDisk|For more information, see [Isolate damaged local disks by using Alibaba Cloud CLI](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Isolate damaged local disks by using Alibaba Cloud CLI.md).|
|Instance restart and restoration of damaged local disks|Instance restart and re-initialization of damaged local disks due to scheduled system maintenance|SystemMaintenance.RebootAndReInitErrorDisk|For more information, see [Isolate damaged local disks by using Alibaba Cloud CLI](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Isolate damaged local disks by using Alibaba Cloud CLI.md).|
|Disk detachment error|Removal of residual disks due to system maintenance|SystemMaintenance.CleanInactiveDisks|Log on to the ECS console, view pending events, and then handle the event as instructed. For more information, see [View system events](/intl.en-US/Deployment & Maintenance/System events/View system events.md).|
|Limited performance of burstable instances|The performance of burstable instances below the baseline performance due to insufficient available CPU credits|N/A|You can use one of the following methods to handle the event:-   Enable the unlimited mode. For more information, see [Switch the performance mode of a burstable instance](/intl.en-US/Instance/Instance type families/Burstable instance types/Switch the performance mode of a burstable instance.md).
-   Upgrade instance configurations. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md). |
|Isolation of damaged local disks|Isolation of damaged local disks due to system maintenance|SystemMaintenance.IsolateErrorDisk|For more information, see [Isolate damaged local disks by using Alibaba Cloud CLI](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Isolate damaged local disks by using Alibaba Cloud CLI.md).|
|Restoration of local disks|Re-initialization of damaged local disks due to system maintenance|SystemMaintenance.ReInitErrorDisk|For more information, see [Isolate damaged local disks by using Alibaba Cloud CLI](/intl.en-US/Deployment & Maintenance/System events/System events on ECS instances equipped with local disks/Isolate damaged local disks by using Alibaba Cloud CLI.md).|

## System event status

The following table describes the status of a system event throughout its lifecycle.

|Status|Status property|Description|
|:-----|:--------------|:----------|
|Inquiring|Transitory|The system event is in the Inquiring state and waiting for your confirmation. The event enters the Executing state after it is confirmed.|
|Scheduled|Transitory|The system event has been scheduled but not performed.|
|Avoided|Stable|The system event was responded to in advance within the user operation window.|
|Executing|Transitory|The system event is being executed.|
|Executed|Stable|The system event has been executed.|
|Canceled|Stable|The scheduled system event has been canceled.|
|Failed|Stable|The system event failed.|

## System event windows

System events have the following windows:

-   **User operation window**: the period between the time when a system event is initiated and the time when the system event is executed. You can select the recommended method based on the impacts of the system event on your business to handle the event in advance or wait until the default actions are triggered. If ECS fixes a system event triggered by a system failure, ECS sends you an event notification in advance based on the system maintenance schedule.

    The following section describes the duration of the user operation window:

    -   For events in the Inquiring state, no time limit applies.
    -   For maintenance-related system events, the window is 24 hours to 48 hours.
    -   For subscription instances that are to be stopped due to expiration, the window is three days.
    -   For pay-as-you-go instances that are to be stopped due to overdue payments, the window is less than 1 hour.
    -   Instances in which a system event occurs due to billing issues are immediately stopped and released in 15 days if the issue is not resolved.
    -   Unexpected system events that are caused by failures or invalid operations do not have a user operation window.
-   **Event execution window**: the period between the time when the system event is responded to and the time when the event execution is complete. The system sends you the execution result.

    The following section describes the duration of the event execution window:

    -   For system events such as failure recovery, the window is within 10 minutes.
    -   Unexpected system events that are caused by failures or invalid operations have a short event execution window.

![Event execution window](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1797919951/p3942.png)

