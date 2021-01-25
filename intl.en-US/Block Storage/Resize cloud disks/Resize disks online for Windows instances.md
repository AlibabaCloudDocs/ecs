---
keyword: [disk resizing, hot disk resizing, resize a disk for a Windows instance, increase the storage capacity of a Windows instance]
---

# Resize disks online for Windows instances

You can resize a system disk or a data disk to extend its capacity. This topic describes how to resize a disk for a Windows instance without stopping the instance.

The disk to be resized online and the instance to which the disk is attached meet the following requirements.

|Resource|Requirement|
|--------|-----------|
|Instance|-   The instance is I/O optimized.
-   The instance does not run Windows Server 2003.
-   Disks on instances of the ecs.ebmc4.8xlarge, ecs.ebmhfg5.2xlarge, and ecs.ebmg5.24xlarge instance types cannot be resized online.
-   The instance is in the **Running** \(Running\) state.
-   The version of the Red Hat virtio SCSI driver is later than 58011. For information about how to check the version of a Red Hat virtio SCSI driver and upgrade the driver, see [Update Red Hat virtio drivers of Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Update Red Hat virtio drivers of Windows instances.md).

**Note:** If your ECS instance does not meet the requirements to resize disks online, you can resize its disks offline. For more information, see [Resize disks offline for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Windows instances.md). |
|Disk|-   The disk is in the **In Use** \(In Use\) state.
-   The disk is an enhanced SSD \(ESSD\), a standard SSD, or an ultra disk.
-   The disk is formatted as New Technology File System \(NTFS\).
-   After you renew a subscription instance and downgrade its configurations, you cannot resize the subscription disks attached to the instance for the remainder of the current billing cycle.
-   When you resize a disk of a specific category, the specified new disk capacity cannot exceed the maximum single-disk capacity allowed for the disk category. For more information, see the "Elastic Block Storage limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md).

**Note:**

If an existing partition of a disk is in the master boot record \(MBR\) format, the disk cannot be resized to 2 TiB or greater in size. If you want to resize a disk that has an MBR partition to more than 2 TiB, use one of the following methods:

-   \(Recommended\) Create a disk of more than 2 TiB, and format the disk to GUID Partition Table \(GPT\) partitions. Then, copy the data from the MBR partition to the GPT partitions. For more information about how to format the disk to GPT partitions, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md).
-   Covert the MBR partition to a GPT partition within the instance. The risk of data loss may occur when you change the partition format. Proceed with caution. For more information, see [Convert the partition format of a data disk on a Windows instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md). |

The following table lists configurations of the instance and disks that are used in the examples of this topic.

|Resource|Description|
|--------|-----------|
|Image used by the instance|Windows Server 2012 R2 64-bit|
|System disk|Is formatted as NTFS and resized from 40 GiB to 60 GiB.|
|Data disk|Is formatted as NTFS and resized from 40 GiB to 60 GiB.|

## Step 1: Create a snapshot

Create a snapshot for the disk to back up the disk data before you resize the disk.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance whose disk you want to resize, and click the instance ID.

5.  On the **Instance Details** page, click **Disks** in the left-side navigation pane.

6.  Find the disk that you want to resize, and click **Create Snapshot** in the **Actions** column.

7.  In the dialog box that appears, enter a snapshot name, specify tags, and then click **Create**.

8.  Click **Snapshots** in the left-side navigation pane to view the snapshot.

    When **100%** appears in the **Progress** column corresponding to the snapshot, the snapshot is created. You can continue to perform subsequent operations.


## Step 2: Resize the disk in the ECS console

1.  On the **Instance Details** page, click **Disks** in the left-side navigation pane.

2.  Find the disk that you want to resize and choose **More** \> **Resize Disk** in the **Actions** column.

    To batch resize disks, log on to the ECS console with your Alibaba Cloud account and choose **Storage & Snapshots** \> **Disks** in the left-side navigation pane. On the Disks page, select the disks that you want to resize, and then click **Resize Disk** in the lower part of the page. Disks that are attached to the same instance cannot be batch resized.

3.  On the **Resize Disks** page, select **Online Resizing**, and set the **Size after Resize** parameter.

    The specified **Size after Resize** value must not be less than the current capacity.

4.  Verify the price. Read and select *ECS Service Terms*, and then click **Confirm**.

5.  Read the notes, and click **I have read the notes. Resize** to complete the payment.


**Note:** After you resize the disk in the ECS console, you must resize the partitions and file systems of the disk within the instance before you can use the new capacity of the disk.

## Step 3: Resize the file system of the system disk or data disk partition

After you resize a disk in the ECS console, the file systems of the disk partitions are not resized. You must connect to the instance to extend file systems. The disk is formatted as NTFS and will be resized from 40 GiB to 60 GiB. This procedure describes how to resize the file system of a system disk partition.

1.  Connect to the ECS instance. For more information, see [Connect to a Windows instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance by using VNC.md).

2.  On the Windows Server desktop, right-click the **Start** icon and select **Disk Management**.

    ![Disk Management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6766431061/p140800.png)

3.  In the **Disk Management** dialog box, choose **Action** \> **Rescan Disks** to view the unallocated disk capacity.

    ![caozuo1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9082909951/p86770.png)

    Disk 0 is the system disk, and Disk 1 is a data disk.

4.  Right-click the blank space in the **Disk 0** section and select **Extend Volume...**

    **Note:** If you are resizing the file system of a data disk partition, right-click the blank space in the data disk \(for example, **Disk 1**\) section to extend the file system.

    ![kuozhan](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9082909951/p86807.png)

5.  Extend the volume as instructed in the **Extend Volume Wizard** dialog box.

    The new space is automatically added to the original volume. The following figure shows the result.

    ![kuozhan2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0182909951/p86808.png)

    After the disk is resized, check whether the new capacity of the disk is consistent with the expected results.

    -   If the resizing succeeds and the business programs in the instance can run properly, the resizing operation is complete.
    -   If the resizing fails, use the backup snapshot to roll back the disk.

## \(Optional\) Step 4: Create new partitions on the data disk

If you want to create new partitions in the new disk space, complete the following procedure.

1.  Connect to the ECS instance. For more information, see [Connect to a Windows instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance by using VNC.md).

2.  On the Windows Server desktop, right-click the **Start** icon and select **Disk Management**.

3.  In the **Disk Management** dialog box, choose **Action** \> **Rescan Disks** to view the unallocated disk capacity.

    ![caozuo1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9082909951/p86770.png)

    Disk 0 is the system disk, and Disk 1 is a data disk.

4.  Right-click the blank space in the **Disk 1** section and select **New Simple Volume...**

    ![jiandan1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0182909951/p86817.png)

5.  Extend the volume as instructed in the New Simple Volume Wizard dialog box.

    A new partition is created in the new disk space.


**Related topics**  


[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

[ResizeDisk](/intl.en-US/API Reference/Disk/ResizeDisk.md)

[AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md)

