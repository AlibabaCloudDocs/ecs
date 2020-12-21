---
keyword: [pay-as-you-go disk, subscription disk, create a disk, disk billing, add data disks]
---

# Create a disk

You can create a subscription or pay-as-you-go data disk to increase the storage space of your ECS instance.

The following table describes the limits that apply to disks that use different billing methods.

|Disk type|Limits|
|---------|------|
|Pay-as-you-go disk|-   The total number of pay-as-you-go data disks that you can create in a region in your account cannot be greater than five times the total number of pay-as-you-go instances in that region in your account. For more information, see the "Elastic Block Storage limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).
-   For more information about the pay-as-you-go billing method, see [Pay-as-you-go](/intl.en-US/Pricing/Billing methods/Pay-as-you-go.md). |
|Subscription disk|-   When you create a subscription disk, you must attach it to a subscription instance. You cannot create standalone subscription disks.
-   Subscription disks cannot be detached. They expire and are released along with the instances to which they are attached. If you want to release a subscription disk, you can convert it to a pay-as-you-go disk, and then detach and release it. |

In addition, you must take note of the following items:

-   You cannot merge multiple disks by formatting them because they are independent of each other. Therefore, we recommend that you determine the number and capacity of disks before you create them.
-   We recommend that you do not use Logical Volume Manager \(LVM\) to create logical volumes on multiple disks. This is because a snapshot can back up data of only a single disk. If you create a logical volume on multiple disks by using LVM, data discrepancies will occur when you roll back these disks.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the upper-right corner of the Disks page, click **Create Disk**.

4.  On the disk creation page, configure parameters for the disk.

    ![Create a pay-as-you-go data disk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8745721061/p4412.png)

    |Parameter|Description|
    |---------|-----------|
    |Attach|Specify whether to attach the created disks to ECS instances.    -   **Not Attach**: only creates disks and does not attach the disks to ECS instances.

If you select this option, only pay-as-you-go disks can be created. The disks and the ECS instances to which you want to attach the disks must reside within the same zone. Proceed with caution when you specify **Region**.

    -   **Attach to ECS Instance**: creates disks and attaches the disks to the specified ECS instance.

If you select this option, you must specify **ECS Instance** by selecting a destination region and an ECS instance. |
    |Billing Method|Specify the billing method of the disks.    -   **Pay-As-You-Go**: Pay-as-you-go disks can be attached to subscription or pay-as-you-go instances.
    -   **Subscription**: Subscription disks must be attached to subscription instances. |
    |Storage|Select a disk category and specify the disk capacity.The following section describes other information:

    -   **Performance Level**: You can set performance levels only for enhanced SSDs \(ESSDs\). You can select a performance level based on the capacity of an ESSD. The disk performance varies with the capacity of the ESSD and the performance level. For more information, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).
    -   **Create from Snapshot**: You can select a snapshot to create disks. Then, the created disks contain data from the snapshot.

For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

    -   **Disk Encryption**: Disk encryption is suitable for scenarios that require data security and regulatory compliance. If you select this option, data stored on the disk is automatically encrypted. |
    |Quantity|Select the number of disks that you want to create.**Note:**

    -   You can attach a maximum of 16 data disks to an ECS instance. When you purchase disks for an instance, take note of the number of data disks attached to the instance.
    -   Pay-as-you-go disks have capacity quotas. The total capacity that you purchase cannot exceed the capacity quota. You can use the following formula to calculate the total disk capacity: Total capacity = Capacity of a single disk × Number of disks. After you configure the disk category, the purchased capacity and the remaining capacity are displayed on the disk creation page. |
    |Release|Specify whether to release automatic snapshots of the disks along with them or release the disks along with the instance to which they are attached. This parameter is available only when you select **Attach to ECS Instance**.|
    |Terms of Service|Read and select ECS Terms of Service.|
    |Others \(Optional\)|Specify the disk name, description, tags, and resource group for easy management.|

5.  Confirm the configuration information and disk fees, and then click **Preview**.

6.  In the Preview dialog box, confirm the purchase information and click **Create**.

    After the disks are created, you can view the created disks on the Disks page. However, you cannot use the disks on ECS instances. If you want to use the disks, you must perform subsequent operations.


The following table describes the operations that you must perform before you can use the created disks.

|Scenario|What to do next|
|--------|---------------|
|You select **Attach to ECS Instance** when you create the disks|Perform the following operations to partition and format the disks:-   Use the GUID Partition Table \(GPT\) format to partition the disks. Disks larger than 2 TiB in size support the GPT partition format. For more information, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB.md).
-   Use the Master Boot Record \(MBR\) format to partition the disks. Disks larger than 2 TiB in size do not support the MBR partition format. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) or [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md). |
|You select **Not Attach** when you create the disks|Perform the following operations to attach, partition, and format data disks:1.  [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md)
2.  Perform the following operations to partition and format the disks:
    -   Use the GUID Partition Table \(GPT\) format to partition the disks. Disks larger than 2 TiB in size support the GPT partition format. For more information, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB.md).
    -   Use the Master Boot Record \(MBR\) format to partition the disks. Disks larger than 2 TiB in size do not support the MBR partition format. For more information, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) or [Format a data disk for a Windows ECS instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Windows ECS instance.md). |

**Related topics**  


[CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md)

[RunInstances](/intl.en-US/API Reference/Instances/RunInstances.md)

[CreateInstance](/intl.en-US/API Reference/Instances/CreateInstance.md)

