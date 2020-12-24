---
keyword: [event, system event, automation, notification message, physical machine faults, physical machine failure, breakdown, active O&M]
---

# Automatic recovery events of instances

If the underlying hardware that hosts an ECS instance fails, Alibaba Cloud performs a check within 1 minute to verify whether the failure can be reversed and whether the instance can be repaired. If the instance cannot be repaired, the instance is restarted within 5 minutes for failover. Metadata of the recovered instance is not changed, such as the instance ID, private IP address, and public IP address.

## Recovery modes

By default, when an ECS instance goes down unexpectedly or an active O&M plan is carried out, Alibaba Cloud automatically restarts the instance. You can customize the modes to recover an instance.

|Recovery mode|Description|System event value|Instance without local storage ①|Instance with local storage or supporting SGX-based encryption ②|
|-------------|-----------|------------------|--------------------------------|----------------------------------------------------------------|
|Automatically restart \(default\)|The instance is restarted automatically and restored to its previous lifecycle state.|SystemFailure.Reboot|Supported|Supported|
|Stop|The instance remains in the **Stopped** state. This mode is applicable to scenarios in which failover or node switchover is configured at the application layer. This mode can avoid service conflicts that may occur after the instance is automatically restarted.|SystemFailure.Stop|Supported|Supported|
|Automatically redeploy|The local disks of the instance are redeployed, the data on the local disks is deleted, and SGX-based encryption is reset.|SystemFailure.Redeploy|N/A|Supported|

-   ① Instances of the instance families without local storage, such as the g-series, c-series, and r-series instance families. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).
-   ② Instances of the following instance families:
    -   Instance families with local storage, such as the d-series, i-series, and gn5-series instance families
    -   Instance families that support Intel ® SGX-based encryption, such as the ebmhfg5 ECS Bare Metal Instance family with high clock speeds

## Limits

-   You can select how to automatically restore an ECS instance, but you cannot intervene with ongoing recovery.
-   You cannot manually restart an instance while automatic recovery is in process.

## Improve fault tolerance

To make full use of the automatic recovery feature and the failover operation of an instance, make sure that you have completed the following operations:

-   Configure core applications such as SAP HANA to automatically start on system startup. This helps avoid interruptions to your business operations.
-   Enable the automatic reconnection feature for your applications. For example, allow applications to automatically connect to MySQL, SQL Server, or Apache Tomcat.
-   Deploy multiple ECS instances in a cluster if you use Server Load Balancer \(SLB\). When an ECS instance is in the automatic recovery process, other ECS instances can continue to provide access to your services.
-   Back up data on the local disk on a regular basis to ensure that you have redundant copies available to redeploy your instance.

## What to do next

-   For more information about how to modify the recovery mode, see [Modify instance maintenance attributes](/intl.en-US/Instance/Manage instances/Modify instance maintenance attributes.md).
-   For more information about how to view automatic recovery events in the ECS console, see [View system event history](/intl.en-US/Deployment & Maintenance/System events/View system event history.md). For the values of automatic recovery system events, see the preceding section [Recovery modes](#section_9n3_eiq_3vb).

**Related topics**  


[DescribeInstanceHistoryEvents](/intl.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md)

[RedeployInstance](/intl.en-US/API Reference/Operations and monitoring/RedeployInstance.md)

[DescribeInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/DescribeInstanceMaintenanceAttributes.md)

[ModifyInstanceMaintenanceAttributes](/intl.en-US/API Reference/Operations and monitoring/ModifyInstanceMaintenanceAttributes.md)

