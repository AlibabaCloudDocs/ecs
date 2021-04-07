---
keyword: [detach a data disk, flexibly attach, SCU, ECS, Alibaba Cloud]
---

# Detach a data disk

You can detach a data disk from an ECS instance if the billing method of the data disk is pay-as-you-go. Local disks cannot be detached.

Before you detach a data disk, make sure that the following requirements are met:

-   The disk is billed on a pay-as-you-go basis. If you need to detach a subscription data disk, you must first change its billing method from subscription to pay-as-you-go. For more information, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md).
-   The disk is attached to an instance and **Status** of the disk is **In Use**.
-   To ensure data integrity, we recommend that you stop reading or writing file systems of the data disk to avoid data loss before you detach the data disk.
-   If the data disk is attached with file systems, you must connect to the ECS instance and detach the data disk or partitions from the operating system, as shown in the following table.

    |Operating system|Detach a data disk or partition|
    |:---------------|:------------------------------|
    |Linux|Run the `umount <Data disk partition>` command. Example: `umount /dev/vdb1`. If you have written the partition mount information to the /etc/fstab file, you must delete the information. Otherwise, you cannot connect to the instance after the instance is restarted. |
    |Windows Server|In the **Disk Management** dialog box, right-click the disk name such as **Disk 2** and select **Offline**.|


You can use one of the following methods to detach data disks in the ECS console:

-   Detach one or more disks from an instance. For more information, see the [Detach a data disk on the Instance Details page](#InstanceCloud) section.
-   Detach a specific disk. For more information, see the [Detach a data disk on the Disks page](#CloudCloud) section.

## Detach a data disk on the Instance Details page

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance from which you want to detach the disk and click the instance ID.

5.  On the **Instance Details** page, click the **Cloud Disk** tab.

6.  Find the disk and choose **More** \> **Detach** in the **Actions** column.

    Only disks that have the following properties can be detached:

    -   The value of **Status** is **In Use**.
    -   The value of **Detachable** is **Yes**.

        **Note:** If the value of **Detachable** corresponding to your disk is **No**, you must first change the billing method of the disk from subscription to pay-as-you-go. For more information, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md).

    -   The value of **Type \(All\)** is **Data Disk**.
7.  In the message that appears, click **OK**.


**Note:** You can repeat the preceding procedure to detach multiple disks.

When the value of **Status** becomes **Unattached**, the disk is detached.

## Detach a data disk on the Disks page

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.

3.  In the top navigation bar, select a region.

4.  Find the disk and choose **More** \> **Detach** in the **Actions** column.

    Only disks that have the following properties can be detached:

    -   The value of **Status** is **In Use**.
    -   The value of **Detachable** is **Yes**.

        **Note:** If the value of **Detachable** corresponding to your disk is **No**, you must first change the billing method of the disk from subscription to pay-as-you-go. For more information, see [Change billing methods of disks](/intl.en-US/Block Storage/Cloud disks/Change billing methods of disks.md).

    -   The value of **Type \(All\)** is **Data Disk**.
5.  In the message that appears, click **OK**.


When the value of **Status** becomes **Unattached**, the disk is detached.

You can release disks that are no longer needed. For more information, see [Release a disk](/intl.en-US/Block Storage/Cloud disks/Release a disk.md).

**Related topics**  


[DetachDisk](/intl.en-US/API Reference/Disk/DetachDisk.md)

