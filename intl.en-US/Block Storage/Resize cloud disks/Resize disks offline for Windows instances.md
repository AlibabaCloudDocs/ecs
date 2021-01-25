# Resize disks offline for Windows instances

You can resize a system disk or data disk to extend its capacity. If your Windows instance does not support online resizing of disks, you can resize the disks of the instance offline. After you resize a disk on an instance offline, you must restart the instance for the changes to take effect.

The disk to be resized offline and the Windows instance to which it is attached meet the following requirements.

|Resource|Requirement|
|--------|-----------|
|Instance|-   The instance is in the **Running** \(Running\) or **Stopped** \(Stopped\) state.
-   If the instance runs a Windows Server 2003 operating system, only data disks of the instance can be resized and the system disk cannot. |
|Disk|-   The disk is in the **In Use** \(In Use\) state.
-   The disk is an enhanced SSD, a standard SSD, or an ultra disk.
-   The disk is formatted with an NTFS file system.
-   After you renew a subscription instance and downgrade its configurations, you cannot resize the subscription disks attached to the instance during the remainder of the current billing cycle.
-   When you resize a disk of a specific category, the specified new disk capacity must not exceed the maximum single-disk capacity allowed for the disk category. For more information, see the "Elastic Block Storage limits" section in [Limits](/intl.en-US/Product Introduction/Limits.md)

**Note:**

If an existing partition of a disk is in the master boot record \(MBR\) format, the disk cannot be resized to 2 TiB or greater in size. If you want to resize a disk that has an MBR partition to more than 2 TiB, use one of the following methods:

-   \(Recommended\) Create a disk of more than 2 TiB, and format the disk to GUID Partition Table \(GPT\) partitions. Then, copy the data from the MBR partition to the GPT partitions. For more information about how to format the disk to GPT partitions, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md).
-   Covert the MBR partition to a GPT partition within the instance. The risk of data loss may occur when you change the partition format. Proceed with caution. For more information, see [Convert the partition format of a data disk on a Windows instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md). |

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


## Step 2: Resize the disk, and restart or start the instance in the console.

1.  On the Instances page, click the instance ID. The **Instance Details** tab appears. Click **Cloud Disk**.

2.  Find the disk to be resized and choose **More** \> **Resize Disk** in the **Actions** column.

    To batch resize disks, log on to the ECS console by using your Alibaba Cloud account and choose **Storage & Snapshots** \> **Disks** in the left-side navigation pane. On the Disks page, select the disks that you want to resize, and then click **Resize Disk** in the lower part of the page. Disks that are attached to the same instance cannot be batch resized.

3.  On the **Resize Disks** page, set the **Size after Resize** parameter.

    The specified **Size after Resize** value cannot be less than the current capacity.

4.  Verify the price. Read and select ECS Service Terms, and then click **Confirm**.

5.  Read the notes, and click **I have read the notes. Resize** to complete the payment.

6.  Restart or start the instance in the ECS console.

    **Note:**

    -   If your instance is in the **Running** \(Running\) state, you must restart the instance in the console. If your instance is in the **Stopped** \(Stopped\) state, you must start the instance in the console.
    -   The disk resizing operation takes effect only after you restart or start the instance by using the console or by calling the RebootInstance operation. If the ECS instance is restarted from within the instance itself, the disk capacity does not change.
    The following procedure demonstrates how to restart an instance.

    1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

    2.  Find the instance to be restarted, and choose **More** \> **Instance Status** \> **Restart** in the **Actions** column.

    3.  In the **Restart Instance** dialog box, click **OK**.


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

