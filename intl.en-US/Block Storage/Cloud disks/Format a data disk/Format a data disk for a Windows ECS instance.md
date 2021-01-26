---
keyword: [format, Alibaba Cloud, ECS, partition a disk in Windows]
---

# Format a data disk for a Windows ECS instance

This topic describes how to create a partition of the Master Boot Record \(MBR\) format for a new data disk attached to a Windows ECS instance. Then, it describes how to mount an NTFS file system to the partition. You can create multiple partitions for a data disk based on your business needs.

The following risks may occur when you format a data disk:

-   Partitioning and formatting data disks are high-risk operations. Exercise caution. The procedure in this topic applies only to new data disks. If your data disk contains data, create a snapshot for the data disk to avoid data loss. For more information, see [Create a snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).
-   You can partition only **data disks** that are attached to ECS instances. **System disks** cannot be partitioned. If you forcibly use a third-party tool to partition the system disk, unknown risks such as system failure and data loss may occur. You can only expand or add partitions for the system disk that has been extended. For more information, see [Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md).

## Procedure

The following procedure applies only to data disks not greater than 2 TiB in size. For information about how to format a data disk greater than 2 TiB in size, see [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md). In the following example, the ECS instance runs the Windows Server 2012 R2 64-bit operating system. A single MBR partition is created for a 20 GiB data disk that is attached to the ECS instance.

1.  Connect to the instance. For more information, see [Connect to an ECS instance]().

2.  On the Windows Server desktop, right-click the **Start** icon, and select **Disk Management**.

3.  Find the unformatted data disk \(Disk 2 in this example\), which is in the **Offline** state.

4.  Right-click the space around Disk 2, and select **Online**.

    After Disk 2 goes online, Disk 2 enters the **Not Initialized** state.

5.  Right-click the space around Disk 2, and select **Initialize Disk**.

6.  In the Initialize Disk dialog box, select **Disk 2**, and select one of the following partition formats:

    -   Currently, MBR is most frequently used. This format only supports data disks up to 2 TiB in size with a maximum of four primary partitions. If you want to divide a disk into more than four partitions, you must use a primary partition as a partition to be expanded and create logical partitions in the primary partition.
    -   GUID Partition Table \(GPT\) is a new partition format, which cannot be recognized by early Windows versions. The data disk size that GPT supports depends on the operating system and the file system. In Windows, GPT supports up to 128 primary partitions.
    In this example, select MBR, and click **OK**.

7.  In the Disk Management window, right-click the **Unallocated** space of Disk 2, and then select **New Simple Volume**.

8.  In the New Simple Volume wizard, perform the following operations:

    1.  Click **Next**.

    2.  Specify the size of the simple volume. If you want to create only one primary partition, use the default value. Click **Next**.

    3.  Select a drive letter. In this example, select F. Click **Next**.

    4.  Specify the formatting settings, including file system, size of allocation unit, and volume label. Determine whether to enable **Quick Formatting** and **File and Folder Compression**. In this example, use the default settings. Click **Next**.

    5.  Start to create a simple volume. When the information shown in the following figure appears in the wizard, a new simple volume is created. Click **Finish** to close the New Simple Volume wizard.

        ![New Simple Volume wizard](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0195461161/p5102.png)


After Disk 2 is partitioned and formatted, its status is displayed in the **Disk Management** window.

![Disk Management](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4772909951/p5103.png)

In **This PC**, you can view a new drive named **New Volume \(F:\)**. The data disk is ready for use.

