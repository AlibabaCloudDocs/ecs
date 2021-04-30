---
keyword: [snapshot, new disk, ECS, replicate a disk]
---

# Create a disk from a snapshot

If you want to use data stored on an existing or a released disk to perform data extraction or fault analysis, you can use a snapshot of the disk to create disks. You can create disks from snapshots of system disks or data disks.

A snapshot is created from a system disk or data disk. The snapshot ID is obtained. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).

When you create a disk from a snapshot, take note of the following items:

-   Disks are independent of each other and cannot be merged by formatting. Therefore, we recommend that you determine the number and capacity of disks that you need before you create them.
-   We recommend that you do not use Logical Volume Manager \(LVM\) to create logical volumes on multiple disks. This is because a snapshot can back up data of only a single disk. If you create a logical volume on multiple disks by using LVM, data discrepancies may occur when you roll back these disks.
-   If you want to attach the new disk to the Elastic Compute Service \(ECS\) instance to which the disk from which the snapshot was created was attached, you must change the UUID of the new disk. For more information, see [Modify the UUID of a disk](/intl.en-US/Best Practices/Block Storage/Modify the UUID of a disk.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the upper-right corner of the **Disks** page, click **Create Disk**.

4.  On the Disk page, click **Create from Snapshot** and select the snapshot from which you want to create disks.

    ![Create from Snapshot](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6968679161/p4416.png)

5.  Configure other parameters for the disks.

    |Parameter|Description|
    |---------|-----------|
    |Attach|Specify whether to attach the created disks to ECS instances.     -   **Not Attach**: only creates disks without attaching them to ECS instances.

If you select this option, only pay-as-you-go disks can be created. The disks and the ECS instances to which you want to attach the disks must reside within the same zone. Proceed with caution when you specify **Region**.

    -   **Attach to ECS Instance**: creates disks and attaches the disks to the specified ECS instance.

If you select this option, you must specify **ECS Instance** by selecting a destination region and an ECS instance. |
    |Billing Method|Specify the billing method of the disks.     -   **Pay-As-You-Go**: Pay-as-you-go disks can be attached to subscription or pay-as-you-go instances.
    -   **Subscription**: Subscription disks must be attached to subscription instances. |
    |Storage|Select a disk category and specify the disk capacity. You must specify a disk capacity of at least the same size as the snapshot. If the disk capacity that you specify is greater than the snapshot size, you must re-partition the disk to ensure that the excessive disk capacity can be used.

**Note:** If the snapshot is less than 2,048 GiB in size and you want to specify a disk capacity of greater than 2,048 GiB, make sure that the source disk of the snapshot uses the GUID Partition Table \(GPT\) partition format. If the source disk does not use GPT, we recommend that you specify a disk capacity of less than 2,048 GiB to avoid data loss during partitioning. For more information, see [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md).

The following section describes other parameters:

    -   **Performance Level**: You can set performance levels only for enhanced SSDs \(ESSDs\). You can select a performance level based on the capacity of an ESSD. The disk performance varies with the capacity of the ESSD and the performance level. For more information, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).
    -   **Disk Encryption**: Disk encryption is suitable for scenarios that require data security and regulatory compliance. If you select this option, data stored on the created disks is automatically encrypted. |
    |Quantity|Select the number of disks that you want to create. **Note:**

    -   When you create disks, take note of the number of data disks on the instance to which you want to attach the disks.Typically, a maximum of 16 data disks can be attached to a single instance. For some instance families such as g6se, more than 16 data disks can be attached to a single instance. For more information, see the "Elastic Block Storage \(EBS\) limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).
    -   Pay-as-you-go disks have capacity quotas. The total capacity that you purchase cannot exceed the capacity quota. You can use the following formula to calculate the total disk capacity: Total capacity = Capacity of a single disk × Number of disks. After you configure the disk category, the purchased capacity and the remaining capacity are displayed on the Disk page. |
    |Release|Specify whether to release the automatic snapshots of the disks along with them or release the disks along with the instance to which they are attached. This parameter is available only when you select **Attach to ECS Instance**.|
    |Terms of Service|Read and select ECS Terms of Service.|
    |Others \(Optional\)|Specify the Disk Name, Description, Tags, and Resource Group parameters for easy management.|

6.  Confirm the configuration information and fees and click **Preview**.

7.  In the Preview message, confirm the purchase information and click **Create**.

    After the disks are created, you can view the created disks on the Disks page. However, these disks cannot be directly used on ECS instances. You must perform the following operations before you can use the disks on ECS instances.


The following table describes the operations that you must perform before you can use the created disks.

|Scenario|What to do next|
|--------|---------------|
|You select **Attach to ECS Instance** when you create the disks|-   Windows: No operations are required.
-   Linux: Log on to the instance and run the `mount` command:

    ```
mount <Disk partition> <Mount point>
    ```

**Note:** If you want to attach a new disk to the ECS instance to which the disk from which the snapshot was created was attached, you must change the UUID of the new disk before you can attach it to the ECS instance. For more information, see [Modify the UUID of a disk](/intl.en-US/Best Practices/Block Storage/Modify the UUID of a disk.md). |
|You select **Not Attach** when you create the disks|-   Windows: [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).
-   Linux:

    1.  [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md)
    2.  Log on to the instance and run the `mount` command:

        ```
mount <Disk partition> <Mount point>
        ```

**Note:** If you want to attach a new disk to the ECS instance to which the disk from which the snapshot was created was attached, you must change the UUID of the new disk before you can attach it to the ECS instance. For more information, see [Modify the UUID of a disk](/intl.en-US/Best Practices/Block Storage/Modify the UUID of a disk.md). |

**Related topics**  


[CreateDisk](/intl.en-US/API Reference/Disk/CreateDisk.md)

