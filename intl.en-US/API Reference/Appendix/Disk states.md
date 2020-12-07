# Disk states

This topic describes the status and information of disks supported by ECS.

|State|Description|
|:----|:----------|
|Creating|Creating. After a disk is created by calling the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md), [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md), or [CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md) operation, the disk enters the Creating state. |
|Available|Unattached. After a pay-as-you-go disk is created by calling the [CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md) operation or a pay-as-you-go data disk is detached by calling the [DetachDisk](/intl.en-US/API Reference/Disk/DetachDisk.md) operation, the disk enters the Unattached state. |
|In\_Use|In use. The stable status of a disk is changed in the following ways:

 -   A subscription data disk is created by using [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md), [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md), or [CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md).
-   A system or data disk is created by calling the [RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md) and [CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md) operations.
-   A pay-as-you-go data disk is attached by using [AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md). |
|ReIniting|Initializing. After you reinitialize a system or data disk by calling the [ReInitDisk](/intl.en-US/API Reference/Disk/ReInitDisk.md) operation, the disk enters the Initializing state. |
|Detaching|Detaching. After a pay-as-you-go data disk is detached by calling the [DetachDisk](/intl.en-US/API Reference/Disk/DetachDisk.md) operation, the disk enters the Detaching state. |
|Deleting[\*](#p_ServiceStatus)|Deleting. After a pay-as-you-go data disk is released by calling the [DeleteDisk](/intl.en-US/API Reference/Disk/DeleteDisk.md) operation, the disk enters the Deleting state. |
|Deleted[\*](#p_ServiceStatus)|Deleted. When a pay-as-you-go data disk is released by calling the [DeleteDisk](/intl.en-US/API Reference/Disk/DeleteDisk.md) operation, the disk enters the Deleted state. |

\* The error message returned because Deleting and Deleted are unavailable states. You cannot query the list of disks in these states by calling the [DescribeDisks](/intl.en-US/API Reference/Disk/DescribeDisks.md) operation.

