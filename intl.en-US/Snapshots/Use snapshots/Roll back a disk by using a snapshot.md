---
keyword: [backup, Alibaba Cloud, data backup, disaster recovery, ]
---

# Roll back a disk by using a snapshot

This topic describes how to roll back a disk by using a snapshot. When the system does not respond or an incorrect operation is performed, you can roll back a disk to a previous version by using its snapshots. Before you roll back a disk, you must have created at least a snapshot of the disk. If you roll back system disks, the current SSH key pairs or usernames and passwords of the instances remain bound to the disks after the disks are rolled back.

Before you roll back a disk by using a snapshot, take note of the following items:

-   A snapshot of the disk to be rolled back is created, and no new snapshot is being created for the disk. For more information, see [Create a normal snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md)or [Create a local snapshot](/intl.en-US/Snapshots/Use snapshots/Create a local snapshot.md).

    **Warning:** The rollback operation is irreversible. After a disk is rolled back, the data that you added, deleted, or changed from the creation of the snapshot to the time when the disk is rolled back is lost. To avoid data losses caused by incorrect operations, we recommend that you create a snapshot for the current disk before you roll back the disk.

-   The disk has not been released.
-   After you replace the system disk, snapshots of the previous system disk cannot be used to roll back the new system disk.
-   If you use a disk to create a dynamic extended volume or redundant array of independent disks \(RAID\), you must stop all I/O operations on the disk before you roll back the disk.
-   The disk is attached to an ECS instance and the instance is in the Stopped state. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md) and [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

    **Note:** A pay-as-you-go instance in a VPC may not be restarted after its disk is rolled back if the No Fees for Stopped Instances \(VPC-Connected\) feature is enabled. We recommend that you select **Retain Instance and Continue Charging After Instance Is Stopped** when you stop the instance.


## Roll back a disk by using a snapshot

You can roll back a disk from the **Snapshots** or **Instances** page. The following example shows how to roll back a disk from the **Instances** page.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance whose disk you want to roll back and click **Manage** in the **Actions** column.

5.  Click the **Snapshot** tab on the **Instance Details** page.

6.  Find the snapshot and click **Roll Back Disk** in the **Actions** column.

    **Note:** You can roll back only one disk at a time. Other disks that are attached to the instance are not affected. After the disk is rolled back, the disk is restored to the status of the entire disk at a certain point in time, instead of the status of a partition or a directory.

7.  In the dialog box that appears, click **OK**.

    **Note:**

    -   Before you click **OK**, we recommend that you click **Create Snapshot** to back up the latest data.
    -   If you select **Start Instance Immediately after Rollback**, the instance automatically starts after the disk is rolled back.

## \(Optional\) Synchronize data after a disk is rolled back

If you roll back a disk by using Snapshot A that was created at the point in time T1 and you need to synchronize the data that you added, deleted, and changed after T1, you can perform the following operations.

![Synchronize data](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7665319951/p40777.png)

1.  Create Snapshot B for the original disk at the point in time T2.

2.  Roll back the original disk by using Snapshot A.

3.  Create a new disk by using Snapshot B.

    For more information, see [Create a disk from a snapshot](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk from a snapshot.md).

4.  Attach the new disk to the same ECS instance.

    For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).

5.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

6.  View the new disk.

    -   Windows instances: The new disk is displayed in the system.
    -   Linux instances: Run the mount command to mount the new disk.
7.  Copy useful data from the new disk to the original disk.

8.  Release the new disk.


-   After a disk is rolled back, the host configuration file and the configuration data such as the hostname, SSH, password, network, system source, and clock source are initialized. You must reconfigure the information.
-   If you resize a disk after you create a snapshot for the disk, the size of the disk is also rolled back after you roll back the disk. To make the disk revert to the size before the rollback, you must log on to the instance to resize the file system again.
    -   [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md)
    -   [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md)

**Related topics**  


[ResetDisk](/intl.en-US/API Reference/Disk/ResetDisk.md)

