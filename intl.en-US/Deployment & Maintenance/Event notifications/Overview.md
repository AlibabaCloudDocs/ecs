---
keyword: [event notification, system event, automation, notification message, ecs]
---

# Overview

This topic provides an overview of ECS event notifications. Event notifications provide information about resource changes. Notifications can be sent for the following events: system events \(including O&M events and exceptions\), instance status changes, events that data disks are attached or detached, and events that snapshots are created. Event notifications enable you to configure message-processing middleware for events to implement event-driven automated O&M in place of SDK polling.

## Event notification name

After you configure notifications for events, you can receive the corresponding notifications if the events occur. The name field of a notification indicates the code name of the event. This field is in the following format: <resource type\>:<event\>:<status\>.

-   <resource type\>: the type of the corresponding ECS resource. Example values: Instance and Disk. Instance indicates ECS instance and Disk indicates Elastic Block Storage \(EBS\) device.
-   <event\>: the name of the event. Example values: SystemMaintenance.Reboot, StateChange, PreemptibleInstanceInterruption, DiskOperationCompleted, and CreateSnapshotCompleted.
-   <status\>: the status of the event. For the valid values of this field, see [Overview](/intl.en-US/Deployment & Maintenance/System events/Overview.md).

    **Note:** The <status\> field is available only for system events related to instances and EBS devices.


## Event notification format

After event notifications are configured, ECS sends the notifications based on the method that you specified. The following example shows a non-customized event notification in the JSON format. This notification is sent for the event that the status of an ECS instance changes.

**Note:** If the notification method that you set supports format conversion, the notification that you receive may be converted to other formats.

```
{
    "eventTime": "20181226T220114.058+0800",
    "id": "9435EAD6-3CF6-4494-8F7A-3A********77",
    "level": "INFO",
    "name": "Instance:StateChange",
    "product": "ECS",
    "regionId": "cn-hangzhou",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
    "userId": "169070********30",
    "ver": "1.0",
    "content": {
        "resourceId": "i-bp1ecr********5go2go",
        "resourceType": "ALIYUN::ECS::Instance",
        "state": "Stopping"
    }
}
```

The following table describes fixed top-level fields in a notification.

|Field|Description|Example|
|-----|-----------|-------|
|id|The ID of the event.|9435EAD6-3CF6-4494-8F7A-3A\*\*\*\*\*\*\*\*77|
|eventTime|The time when the event occurred \(UTC+8\).|20181226T220114.058+0800|
|level|The level of the event. Valid values: -   INFO
-   WARN
-   CRITICAL

|INFO|
|name|The name of the event. For more information, see the [Event notification name](#section_qx4_4f2_ig4) section.|Instance:StateChange|
|product|The name of the service. Valid value: ECS.|ECS|
|regionId|The ID of the region where the event occurred. For the valid values of this field, see [Regions and zones]().|cn-hangzhou|
|resourceId|The Alibaba Cloud Resource Name \(ARN\) of the resource.|acs:ecs:cn-hangzhou:169070\*\*\*\*\*\*\*\*30:instance/i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|userId|The ID of the Alibaba Cloud account.|169070\*\*\*\*\*\*\*\*30|
|content|The event details. This field can contain one or more subfields. For more information about the subfields, see the following topics: -   [Instance event notification](/intl.en-US/Deployment & Maintenance/Event notifications/Event notification list/Instance event notification.md)
-   [Block storage event notification](/intl.en-US/Deployment & Maintenance/Event notifications/Event notification list/Block storage event notification.md)
-   [Snapshot event notification](/intl.en-US/Deployment & Maintenance/Event notifications/Event notification list/Snapshot event notification.md)

|None|

**References**  


[Set event notifications](/intl.en-US/Deployment & Maintenance/Event notifications/Set event notifications.md)

[PutEventRule](/intl.en-US/API Reference/Event-triggered alert rules/PutEventRule.md)

