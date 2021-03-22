---
keyword: [event notification, system event, automation, message notification, ECS]
---

# Elastic Block Storage event notifications

You can subscribe to notifications for the following Elastic Block Storage events: system events, data disk attaching or detaching, disk retaining, and disk release due to overdue payments.

## Events

You can subscribe to notifications for the following Elastic Block Storage events:

-   [System events](#section_hxf_fg4_w14)
-   [Data disk attaching or detaching](#section_o6e_vi0_uhe)
-   [Disk retaining](#section_575_2e4_f4m)
-   [Disk release due to overdue payments](#section_2by_hk4_ct3)

## System events

Elastic Block Storage system events are caused only by exceptions. ECS sends two notifications: one at the start time of the event and the other at the end time of the event. For the event notification names of different system events, see [Appendix: event notification names](#section_0p8_lij_brj).

The following notifications are example notifications in the JSON format for a Stalled event that has a severe impact on disk performance.

-   The initial notification that ECS sends you when the event starts contains the executeStartTime parameter.

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
      "level": "CRITICAL",
      "name": "Disk:Stalled:Executing",
      "userId": "169070********30",
      "eventTime": "20190410T080101.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-t4navn7********6x5no",
        "diskId": "d-t4ndyqve********n4ds",
        "device": "/dev/xvdb",
        "eventType": "Stalled",
        "executeStartTime": "2019-04-10T01:01:01Z",
        "ecsInstanceId": "i-bp1ecr********5go2go",
        "ecsInstanceName": "ecs-instance-name"
      }
    }
    ```

-   The notification that ECS sends you when the event ends contains the executeFinishTime parameter.

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
      "level": "CRITICAL",
      "name": "Disk:Stalled:Executing",
      "userId": "169070********30",
      "eventTime": "20190410T080301.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-t4navn7********6x5no",   
        "diskId": "d-t4ndyqve********n4ds",    
        "device": "/dev/xvdb",                 
        "eventType": "Stalled",                
        "executeStartTime": "2019-04-10T01:01:01Z",   
        "executeFinishTime": "2019-04-10T01:03:01Z",  
        "ecsInstanceId": "i-bp1ecr********5go2go",    
        "ecsInstanceName": "ecs-instance-name"        
      }
    }
    ```


The following table describes the sub-parameters contained in the content parameter.

|Parameter|Description|Example|
|---------|-----------|-------|
|eventId|The ID of the system event.|e-t4navn7\*\*\*\*\*\*\*\*6x5no|
|diskId|The ID of the Elastic Block Storage device whose performance is affected.|d-t4ndyqve\*\*\*\*\*\*\*\*n4ds|
|device|The mount point of the Elastic Block Storage device.|/dev/xvdb|
|eventType|The type of the system event. Valid values: -   Degraded: The performance of the Elastic Block Storage device is degraded.
-   SeverelyDegraded: The performance of the Elastic Block Storage device is severely degraded.
-   Stalled: The performance of the Elastic Block Storage device is severely affected.

|Stalled|
|executeStartTime|The start time of the system event. The time is in UTC.|2019-04-10T01:01:01Z|
|executeFinishTime|The end time of the system event. The time is in UTC.|2019-04-10T01:03:01Z|
|ecsInstanceId|The ID of the ECS instance to which the Elastic Block Storage device is attached.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|ecsInstanceName|The name of the ECS instance to which the Elastic Block Storage device is attached.|ecs-instance-name|

## Data disk attaching or detaching

After a data disk is attached to or detached from an instance, ECS sends you a notification to indicate whether the attach or detach operation is successful. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md) and [Detach a data disk](/intl.en-US/Block Storage/Cloud disks/Detach a data disk.md).

The following code shows the event notification in the JSON format:

```
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
  "level": "INFO",
  "name": "Disk:DiskOperationCompleted",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
      "diskId" : "d-t4ndyqve********n4ds",
      "operation" : "AttachDisk",
      "result" : "accomplished"
  }
}
```

The following table describes the sub-parameters contained in the content parameter.

|Parameter|Description|Example|
|---------|-----------|-------|
|diskId|The ID of the disk.|d-bp1bwa\*\*\*\*\*\*\*\*9ol4mi|
|operation|The operation type. Valid values: -   AttachDisk: attaches a disk.
-   DetachDisk: detaches a disk.

|AttachDisk|
|result|The operation result. Valid values: -   accomplished: The operation succeeds.
-   failed: The operation fails.

**Note:** If the operation succeeds, the level value of the event is INFO. If the operation fails, the level value of the event is WARN.

|accomplished|

## Disk retaining

You can disable **Release with Instance** for disks, including system and data disks. The disks are retained and converted to pay-as-you-go data disks when their attached instances are released. For more information, see [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).

The following code shows the event notification in the JSON format:

```
{
    "ver": "1.0",
    "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
    "product": "ECS",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
    "level": "INFO",
    "instanceName": "disk-event-subscription",
    "name": "Disk:ConvertToPostpaidCompleted",
    "userId": "169070********30",
    "eventTime": "20190409T121826.922+0800",
    "regionId": "cn-hangzhou",
    "content": {
    "diskId" : "d-t4ndyqve********n4ds",
    "result" : "accomplished"
    },
}
```

The following table describes the sub-parameters contained in the content parameter.

|Parameter|Description|Example|
|---------|-----------|-------|
|diskId|The ID of the disk.|d-bp1bwa\*\*\*\*\*\*\*\*9ol4mi|
|result|The operation result. Valid values: -   accomplished: The operation succeeds.
-   failed: The operation fails.

|accomplished|

## Disk release due to overdue payments

You may receive a disk release notification in the following scenarios:

-   You do not complete real-name verification for your account if Elastic Block Storage devices are located in mainland China.
-   Your pay-as-you-go disk is released because you have an overdue payment in your account.

The following code shows the event notification in the JSON format:

```
{
    "ver": "1.0",
    "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
    "product": "ECS",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
    "level": "CRITICAL",
    "instanceName": "disk-event-subscription",
    "name": "Disk:OverduePaymentRelease",
    "userId": "169070********30",
    "eventTime": "20190409T121826.922+0800",
    "regionId": "cn-hangzhou",
    "content": {
    "instanceId" : "i-bp1792********an2ukf",
    "diskId" : "d-t4ndyqve********n4ds"
    },
}
```

The following table describes the sub-parameters contained in the content parameter.

|Parameter|Description|Example|
|---------|-----------|-------|
|instanceId|The ID of the instance to which the disk is attached.|i-bp1792\*\*\*\*\*\*\*\*an2ukf|
|diskId|The ID of the disk.|d-bp1bwa\*\*\*\*\*\*\*\*9ol4mi|

## Appendix: event notification names

|Event|Event type and code|Event notification name and code|
|-----|-------------------|--------------------------------|
|Performance impact|Severe impact on disk performance: Stalled|-   Start of severe impact on disk performance: Disk:Stalled:Executing
-   End of severe impact on disk performance: Disk:Stalled:Executed |
|Local disk damage|Local disks damaged: ErrorDetected|-   Start of local disk damage alert: Disk:ErrorDetected:Executing
-   End of local disk damage alert: Disk:ErrorDetected:Executed |

