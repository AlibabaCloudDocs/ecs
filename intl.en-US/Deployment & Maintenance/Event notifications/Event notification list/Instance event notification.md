---
keyword: [event notification, system event, automation, message notification, ECS]
---

# Instance event notification

Elastic Compute Service \(ECS\) can send notifications for instance events such as system events, instance status changes, and release of preemptible instances.

## Events

ECS can send notifications for the following instance events:

-   [System events](#section_gu3_yxb_yt4)
-   [Instance status changes](#section_kzt_1pq_eau)
-   [Release of a preemptible instance](#section_7ef_g8g_x02)
-   [Hot migration of ECS instances on a dedicated host](#section_hzp_hcm_aib)
-   [Changes in the performance mode of burstable instances](#section_muf_u1g_ohb)
-   [Limited performance of burstable instances](#section_glx_g6x_cn4)

## System events

When a system event occurs on an instance, ECS sends an initial notification for the event, and sends subsequent notifications every time the event status changes. For the names of notifications for system events, see [Appendix: Notifications for instance-related system events](#section_r7e_5s7_vu8).

The following examples show notifications in the JSON format for an **Instance restart due to system maintenance** \(SystemMaintenance.Reboot\) event.

-   The first notification indicates that the event is in the **Scheduled** \(Scheduled\) state.

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "CRITICAL",
      "name": "Instance:SystemMaintenance.Reboot:Scheduled",
      "userId": "169070********30",
      "eventTime": "20190409T121826.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-bp11trd********pqum2",
        "publishTime": "2019-04-09T04:18:26Z",
        "notBefore": "2019-04-12T01:01:01Z",      
        "instanceId": "i-bp1ecr********5go2go",   
        "eventType": "SystemMaintenance.Reboot",  
        "eventStatus": "Scheduled"
      }
    }
    ```

-   If you restart the instance before the time specified by the notBefore subparameter, the system event is avoided and ECS sends a notification which indicates that the event status is changed to **Avoided** \(Avoided\).

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "CRITICAL",
      "name": "Instance:SystemMaintenance.Reboot:Scheduled",
      "userId": "169070********30",
      "eventTime": "20190410T160101.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-bp11trdr********qum2",
        "publishTime": "2019-04-09T04:18:26Z",
        "notBefore": "2019-04-12T01:01:01Z",
        "instanceId": "i-bp1ecr********5go2go",
        "eventType": "SystemMaintenance.Reboot",
        "eventStatus": "Avoided",
        "executeStartTime": "2019-04-10T08:01:01Z",  
        "executeFinishTime": "2019-04-10T08:01:01Z"  
      }
    }
    ```


The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|eventId|The ID of the system event.|e-t4navn7\*\*\*\*\*\*\*\*6x5no|
|publishTime|The time when the system event is pushed.|2019-04-09T04:18:26Z|
|notBefore|The scheduled start time of the event. This subparameter is available only for system maintenance events.|2019-04-12T01:01:01Z|
|instanceId|The ID of the affected instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|eventType|The type of the system event. For more information about the subparameter values, see [Overview](/intl.en-US/Deployment & Maintenance/System events/Overview.md).|SystemMaintenance.Reboot|
|eventStatus|The status of the system event. For more information about the subparameter values, see [Overview](/intl.en-US/Deployment & Maintenance/System events/Overview.md).|Avoided|
|executeStartTime|The start time of the event. It is in UTC.|2019-04-10T08:01:01Z|
|executeFinishTime|The end time of the event. It is in UTC. **Note:** The executeStartTime and and executeFinishTime subparameters are available only for events in the **Executing** \(Executing\), **Executed** \(Executed\), **Canceled** \(Canceled\), or **Avoided** \(Avoided\) state.

|2019-04-10T08:01:01Z|

## Instance status changes

When the status of your instance changes, ECS sends you an event notification. For more information about instance status changes, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

The following example shows a notification for the event that the status of an instance changes to **Running** \(Running\):

```
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
  "level": "INFO",
  "name": "Instance:StateChange",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "resourceId": "i-bp1ecr********5go2go",  
    "resourceType": "ALIYUN::ECS::Instance", 
    "state": "Running"                       
  }
}
```

The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|resourceId|The ID of the instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|resourceType|The type of the resource. Set the value to ALIYUN::ECS::Instance.|ALIYUN::ECS::Instance|
|state|The status of the instance. Valid values: -   Created: The instance is created. This event notification is sent only once when the instance is created.
-   Starting: The instance is being started.
-   Running: The instance is running.
-   Stopping: The instance is being stopped or restarted.
-   Stopped: The instance is stopped.
-   Deleted: The instance is released.

|Running|

## Release of a preemptible instance

Preemptible instances may be released due to fluctuations in market prices or insufficient resources. Five minutes before a preemptible instance is released, ECS sends an event notification to warn you about the interruption of the instance. For more information, see [Overview](/intl.en-US/Instance/Instance purchasing options/Preemptible instances/Overview.md).

The following example shows such an event notification in the JSON format:

```
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
  "level": "INFO",
  "name": "Instance:PreemptibleInstanceInterruption",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "instanceId": "i-bp1ecr********5go2go",  
    "action": "delete"                       
  }
}
```

The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|instanceId|The ID of the preemptible instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|action|The action on the preemptible instance. Set the value to delete.|delete|

## Hot migration of ECS instances on a dedicated host

You can call the [ModifyInstanceDeployment](/intl.en-US/API Reference/Dedicated hosts/ModifyInstanceDeployment.md) operation to perform hot migration of ECS instances between dedicated hosts. Hot migration of ECS instances is asynchronous, and the status of the ECS instances does not change during the migration. You can configure notifications for the Instance:LiveMigrationAcrossDDH event to receive updates about the migration progress.

The following examples show the event notifications in the JSON format:

-   Notification for the event that the hot migration starts:

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "INFO",
      "instanceName": "instance-event-subscription",
      "name": "Instance:LiveMigrationAcrossDDH",
      "userId": "169070********30",
      "eventTime": "20180608T092537.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
          "instanceId" : "i-bp1ecr********5go2go",
          "sourceDedicatedHostId" : "dh-2ze3lm********t8nr82",
          "destinationDedicatedHostId" : "dh-2ze3lm********t8nr83",
          "startTime" : "2018-06-08T01:25:37Z",
          "status" : "started"
      }
    }
    ```

-   Notification for the event that the hot migration is complete:

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "INFO",
      "instanceName": "instance-event-subscription",
      "name": "Instance:LiveMigrationAcrossDDH",
      "userId": "169070********30",
      "eventTime": "20180608T092545.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
          "instanceId" : "i-bp1ecr********5go2go",
          "sourceDedicatedHostId" : "dh-2ze3lm********t8nr82",
          "destinationDedicatedHostId" : "dh-2ze3lm********t8nr83",
          "startTime" : "2018-06-08T01:25:37Z",
          "endTime" : "2018-06-08T01:25:45Z",
          "status" : "accomplished"
      }
    }
    ```

-   Notification for the event that the hot migration fails:

    ```
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "INFO",
      "instanceName": "instance-event-subscription",
      "name": "Instance:LiveMigrationAcrossDDH",
      "userId": "169070********30",
      "eventTime": "20180608T092545.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
          "instanceId" : "i-bp1ecr********5go2go",
          "sourceDedicatedHostId" : "dh-2ze3lm********t8nr82",
          "destinationDedicatedHostId" : "dh-2ze3lm********t8nr83",
          "startTime" : "2018-06-08T01:25:37Z",
          "endTime" : "2018-06-08T01:25:45Z",
          "status" : "failed"
      }
    }
    ```


The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|instanceId|The ID of the instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|sourceDedicatedHostId|The ID of the source dedicated host.|dh-2ze3lm\*\*\*\*\*\*\*\*t8nr82|
|destinationDedicatedHostId|The ID of the destination dedicated host.|dh-2ze3lm\*\*\*\*\*\*\*\*t8nr83|
|startTime|The start time of the migration. It is in UTC.|2018-06-08T01:25:37Z|
|endTime|The end time of the migration. It is in UTC.|2018-06-08T01:25:45Z|
|status|The status of the hot migration. Valid values: -   started: The migration starts.
-   failed: The migration fails.
-   accomplished: The migration is complete.

|accomplished|

## Changes in the performance mode of burstable instances

If the performance mode of a burstable instance changes, ECS sends a notification for the Instance:PerformanceModeChange event.

The following example shows such an event notification in the JSON format:

```
{
    "ver": "1.0",
    "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
    "product": "ECS",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
    "level": "INFO",
    "name": "Instance:PerformanceModeChange",
    "userId": "169070********30",
    "eventTime": "20190409T121826.922+0800",
    "regionId": "cn-hangzhou",
    "content": {
        "instanceId" : "i-bp1ecr********5go2go",
        "creditSpecification" : "Unlimited",
        "operator" : "System"
    }
}
```

The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|instanceId|The ID of the instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|creditSpecification|The new performance mode of the burstable instance. Valid values: -   Standard: standard mode
-   Unlimited: unlimited mode

|Standard|
|operator|The operator that triggers the event. Valid values: -   User: You change the performance mode of the instance by using the ECS console or by calling API operations.
-   System: The system automatically changes the performance mode of the instance. The performance mode of your burstable instance may be automatically changed if the instance depletes its CPU credits, if the No Fees for Stopped Instances \(VPC-Connected\) feature is triggered, or if you have overdue payments in your account. For more information, see [Switch the performance mode of a burstable instance](/intl.en-US/Instance/Instance type families/Burstable instance types/Switch the performance mode of a burstable instance.md).

|User|

## Limited performance of burstable instances

When a burstable instance depletes its CPU credits, the instance is limited to its baseline performance and runs in standard mode. An Instance:BurstablePerformanceRestricted event is generated.

**Note:** Each Instance:BurstablePerformanceRestricted event spans a period of one hour. That means the interval between the start time and end time of the event is 1 hour. This event indicates only that the instance gets limited to its baseline performance during the event period, but does not necessarily indicate that the instance keeps limited to its baseline performance throughout the period. If the instance keeps limited to its baseline performance for an extended period of time, an Instance:BurstablePerformanceRestricted event is generated every hour.

The following example shows the event notification in the JSON format:

```
{
    "ver": "1.0",
    "id": "2256A988-0B26-4E2B-820A-8A0580D0B8E5",
    "product": "ECS",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
    "level": "INFO",
    "name": "Instance:BurstablePerformanceRestricted",
    "userId": "169070********30",
    "eventTime": "20190409T121826.922+0800",
    "regionId": "cn-hangzhou",
    "content": {
        "instanceId" : "i-bp1ecr********5go2go",
        "intervalStart" : "2019-11-11T11:00Z",
        "intervalEnd" : "2019-11-11T12:00Z"
    }
}
```

The following table describes the subparameters contained in the content parameter.

|Subparameter|Description|Example|
|------------|-----------|-------|
|instanceId|The ID of the instance.|i-bp1ecr\*\*\*\*\*\*\*\*5go2go|
|intervalStart|The start time of the event. It is in UTC.|2019-11-11T11:00Z|
|intervalEnd|The end time of the event. It is in UTC.|2019-11-11T12:00Z|

## Appendix: Notifications for instance-related system events

|Impact|Event type and code|Event notification name and code|
|------|-------------------|--------------------------------|
|The instance is restarted.|Instance restart due to system maintenance: SystemMaintenance.Reboot|-   Instance restart scheduled \(system maintenance\): Instance:SystemMaintenance.Reboot:Scheduled
-   Scheduled instance restart being executed \(system maintenance\): Instance:SystemMaintenance.Reboot:Executing
-   Scheduled instance restart completed \(system maintenance\): Instance:SystemMaintenance.Reboot:Executed
-   Scheduled instance restart avoided \(system maintenance\): Instance:SystemMaintenance.Reboot:Avoided
-   Scheduled instance restart canceled \(system maintenance\): Instance:SystemMaintenance.Reboot:Canceled
-   Scheduled instance restart failed \(system maintenance\): Instance:SystemMaintenance.Reboot:Failed |
|The instance is unexpectedly restarted.|Instance restart due to system errors: SystemFailure.Reboot|-   Instance restart being executed \(system error\): Instance:SystemFailure.Reboot:Executing
-   Instance restart completed \(system error\): Instance:SystemFailure.Reboot:Executed |
|The instance is unexpectedly restarted.|Instance restart due to instance errors: InstanceFailure.Reboot|-   Instance restart being executed \(instance error\): Instance:InstanceFailure.Reboot:Executing
-   Instance restart completed \(instance error\): Instance:InstanceFailure.Reboot:Executed |
|The instance is redeployed.|Instance redeployment due to system maintenance: SystemMaintenance.Redeploy|-   Instance redeployment scheduled \(system maintenance\): Instance:SystemMaintenance.Redeploy:Scheduled
-   Scheduled instance redeployment being executed \(system maintenance\): Instance:SystemMaintenance.Redeploy:Executing
-   Scheduled instance redeployment completed \(system maintenance\): Instance:SystemMaintenance.Redeploy:Executed
-   Scheduled instance redeployment avoided \(system maintenance\): Instance:SystemMaintenance.Redeploy:Avoided
-   Scheduled instance redeployment canceled \(system maintenance\): Instance:SystemMaintenance.Redeploy:Canceled |
|The instance is redeployed.|Instance redeployment due to system errors: SystemFailure.Redeploy|-   Instance redeployment scheduled \(system error\): Instance:SystemFailure.Redeploy:Scheduled
-   Instance redeployment being executed \(system error\): Instance:SystemFailure.Redeploy:Executing
-   Instance redeployment completed \(system error\): Instance:SystemFailure.Redeploy:Executed
-   Instance redeployment avoided \(system error\): Instance:SystemFailure.Redeploy:Avoided
-   Instance redeployment canceled \(system error\): Instance:SystemFailure.Redeploy:Canceled |
|The instance is restarted and the damaged local disk is isolated.|Instance restart and local disk replacement due to system maintenance: SystemMaintenance.RebootAndIsolateErrorDisk|-   Instance restart and local disk isolation being inquired \(system maintenance\): Instance:SystemMaintenance.RebootAndIsolateErrorDisk:Inquiring
-   Instance restart and local disk isolation being executed \(system maintenance\): Instance:SystemMaintenance.RebootAndIsolateErrorDisk:Executing
-   Instance restart and local disk isolation completed \(system maintenance\): Instance:SystemMaintenance.RebootAndIsolateErrorDisk:Executed
-   Instance restart and local disk isolation avoided \(system maintenance\): Instance:SystemMaintenance.RebootAndIsolateErrorDisk:Avoided
-   Instance restart and local disk isolation canceled \(system maintenance\): Instance:SystemMaintenance.RebootAndIsolateErrorDisk:Canceled |
|The instance is restarted and the damaged local disk is restored.|Instance restart and local disk re-initialization due to system maintenance: SystemMaintenance.RebootAndReInitErrorDisk|-   Instance restart and local disk re-initialization being inquired \(system maintenance\): Instance:SystemMaintenance.RebootAndReInitErrorDisk:Inquiring
-   Instance restart and local disk re-initialization being executed \(system maintenance\): Instance:SystemMaintenance.RebootAndReInitErrorDisk:Executing
-   Instance restart and local disk re-initialization completed \(system maintenance\): Instance:SystemMaintenance.RebootAndReInitErrorDisk:Executed
-   Instance restart and local disk re-initialization avoided \(system maintenance\): Instance:SystemMaintenance.RebootAndReInitErrorDisk:Avoided
-   Instance restart and local disk re-initialization canceled \(system maintenance\): Instance:SystemMaintenance.RebootAndReInitErrorDisk:Canceled |
|The instance is released.|Automatic instance release due to instance creation failures: SystemFailure.Delete|-   Automatic instance release being executed \(instance creation failure\): Instance:SystemFailure.Delete:Executing
-   Automatic instance release completed \(instance creation failure\): Instance:SystemFailure.Delete:Executed
-   Automatic instance release avoided \(instance creation failure\): Instance:SystemFailure.Delete:Avoided |

