---
keyword: [ECS, disk resizing, extend a partition]
---

# Resize disks online for Linux instances

You can resize system and data disks to extend their capacities. This topic describes how to resize a disk for a Linux instance when the instance is running.

The following table describes the requirements that must be met before you resize a disk online for a Linux instance.

|Resource|Requirement|
|--------|-----------|
|Instance|-   The instance is I/O optimized.
-   The public image used by the instance supports online resizing of disks. For more information about images that support online resizing of disks, see [Operating systems that support online resizing](#section_cqo_5zn_ine).
-   Disks on instances of the ecs.ebmc4.8xlarge, ecs.ebmhfg5.2xlarge, and ecs.ebmg5.24xlarge instance types cannot be resized online.
-   The instance is in the **Running** \(Running\) state.
-   The version of the Linux kernel of the instance is 3.6.0 and later. You can run the `uname -a` command to check the kernel version.

If the version of the Linux kernel is earlier than 3.6.0, you can extend partitions of a disk on the instance. For more information, see [Procedure for instances with kernels earlier than 3.6.0](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md) and [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md).


**Note:** If your Elastic Compute Service \(ECS\) instance does not meet the requirements of online disk resizing, you can resize its disks offline. For more information, see [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md). |
|Disk|-   The disk is in the **In Use** \(In Use\) state.
-   The disk is an enhanced SSD \(ESSD\), a standard SSD, or an ultra disk.
-   After you renew a subscription instance and downgrade its configurations, you cannot resize the subscription disks on the instance for the remainder of the current billing cycle.
-   When you resize a disk of a specific category, the specified new disk capacity cannot exceed the maximum single-disk capacity allowed for the disk category. For more information, see the "Elastic Block Storage \(EBS\) limits" section of the [Limits](/intl.en-US/Product Introduction/Limits.md) topic.

**Note:** A disk in the master boot record \(MBR\) partition format cannot be resized to 2 TiB or larger. To resize an MBR disk to larger than 2 TiB, we recommend that you create a disk larger than 2 TiB, partition and format the new disk to the GUID Partition Table \(GPT\) format, and then copy data from the original MBR disk to the new GPT disk. For more information about how to use the GPT format to partition and format disks, see [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md). |

The following table describes configurations of the instance and disks that are used in the examples of this topic.

|Resource|Description|
|--------|-----------|
|Image used by the instance|Alibaba Cloud Linux 2.1903 LTS 64-bit public image|
|System disk|/dev/vda: uses the MBR partition format and ext4 file system, and the capacity is extended from 40 GiB to 60 GiB.|
|Data disk|-   /dev/vdb: uses the MBR partition format and ext4 file system, and the capacity is extended from 40 GiB to 60 GiB.
-   /dev/vdc: uses the GPT partition format and XFS file system, and the capacity is extended from 40 GiB to 60 GiB. |

## Step 1: Create a snapshot

Create a snapshot for the disk to back up the data stored in the disk before you resize the disk.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Find the instance whose disk you want to resize and click the instance ID.

5.  On the **Instance Details** page, click the **Cloud Disk** tab.

6.  Find the disk that you want to resize and click **Create Snapshot** in the **Actions** column.

7.  In the dialog box that appears, enter a snapshot name, select tags from the drop-down list, and then click **Create**.

8.  Click the **Snapshot** tab to view the snapshot.

    When **100%** appears in the **Progress** column corresponding to the snapshot, the snapshot is created. You can continue to perform subsequent operations.


## Step 2: Resize the disk in the ECS console

1.  On the **Instance Details** page, click the **Cloud Disk** tab.

2.  Find the disk that you want to resize and choose **More** \> **Resize Disk** in the **Actions** column.

    To batch resize disks, log on to the ECS console by using your Alibaba Cloud account and choose **Storage & Snapshots** \> **Disks** in the left-side navigation pane. On the Disks page, select the disks that you want to resize and click **Resize Disk** in the lower part of the page. Disks that are attached to the same instance cannot be batch resized.

3.  On the **Resize Disks** page, select **Online Resizing** and set the **Size after Resize** parameter.

    The specified **Size after Resize** value must not be less than the current capacity.

4.  Verify the price. Read and select *ECS Service Terms*, and then click **Confirm**.

5.  Read the notes, click **I have read the notes. Resize**, and then complete the payment.


**Note:**

-   After you resize the disk in the ECS console, you must resize the partitions and file systems of the disk within the instance before you can use the new capacity of the disk.
-   If you use Logical Volume Manager \(LVM\) to manage partitions of the disk, you must use LVM to resize the partitions and file systems after you resize the disk in the console. For more information, see [Resize an LV](/intl.en-US/Best Practices/Block Storage/Use LVs for Linux/Resize an LV.md).

## Step 3: View the disk partitions

Log on to the ECS instance to view the partition types \(MBR and GPT\) and file system types \(such as ext4 and XFS\) of the system disk and data disks. Subsequent resize operations vary based on the types of the partitions and file systems.

1.  Log on to the ECS instance. For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Run the following command to view the disks attached to the instance:

    ```
    fdisk -lu
    ```

    The following figure shows the /dev/vda1 partition of the system disk and the /dev/vdb1 and /dev/vdc1 partitions of data disks.

    ![View the partitions of the disks.](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2256420061/p135832.png)

    |No.|Partition|Description|
    |---|---------|-----------|
    |①|`/dev/vda1`|A partition of the system disk. A value of **Linux** for **System** indicates that the partition is in the MBR format.|
    |②|`/dev/vdb1`|A partition of a data disk. A value of **Linux** for **System** indicates that the partition is in the MBR format.|
    |③|`/dev/vdc1`|A partition of a data disk. A value of **GPT** for **System** indicates that the partition is in the GPT format.|

    **Note:** If the disk capacity is still 40 GiB in the command output \(`Disk /dev/vda: 42.9 GB` in the figure\), the resize operation fails. We recommend that you restart the instance in the console.

3.  Run the following command to check the file system types of existing partitions:

    ```
    df -Th
    ```

    A command output similar to the following one is returned.

    ![View the file systems](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135833.png)


## Step 4: Resize partitions

When you view the disk partitions, you can find that the partitions and file systems within the ECS instance are not resized. This step describes how to resize the partitions of the resized disk within the ECS instance.

1.  Install the gdisk tool on the ECS instance.

    You must perform this step if the partitions are in the GPT format. Skip this step if the partitions are in the MBR format.

    ```
    yum install gdisk -y
    ```

2.  Install the growpart tool.

    -   Run the following command if the instance that runs CentOS 7 and later:

        ```
        yum install -y cloud-utils-growpart
        ```

    -   Run the following commands if the instance that runs Debian 9 and later or Ubuntu 14 and later:

        Update the software source.

        ```
        apt-get update
        ```

        Install cloud-guest-utils.

        ```
        apt-get install -y cloud-guest-utils
        ```

3.  Run the following command to resize partitions:

    ```
    growpart /dev/vda 1
    ```

    In this example, the /dev/vda1 partition of the system disk is resized. Use a space to separate `/dev/vda` from `1`. To resize other partitions, modify the command based on your actual needs. A command output similar to the following one is returned.

    ![growpart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135834.png)

    **Note:** When you run the growpart /dev/vda 1 command, the `unexpected output in sfdisk --version [sfdisk, from util-linux 2.23.2]` error may be prompted. For information about how to troubleshoot this problem, see the "Troubleshooting" section of this topic.


## Step 5: Resize file systems

This step describes how to resize the file system of a partition within an ECS instance.

1.  Resize the file systems within the ECS instance based on the file system types.

    -   To resize ext \(such as ext4\) file systems, run the following commands.

        Resize the file system of the /dev/vda1 partition of the system disk.

        ```
        resize2fs /dev/vda1    
        ```

        Resize the file system of the /dev/vdb1 partition of a data disk.

        ```
        resize2fs /dev/vdb1          
        ```

        **Note:** `/dev/vda1` and `/dev/vdb1` are partition names. Replace them with your actual partition names.

    -   To resize XFS file systems, run the following command:

        ```
        xfs_growfs /media/vdc
        ```

        **Note:** `/media/vdc` is the mount point of the `/dev/vdc1` partition. Replace it with the actual mount point of your partition.

2.  Run the following command to check the resize results:

    ```
    df -Th
    ```

    A command output similar to the following one is returned.

    ![Check the resize results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135835.png)

    After the disk is resized, check whether the new capacity of the disk is as expected.

    -   If the file systems are resized and the business programs in the instance can run normally, the resize operation is complete.
    -   If the file systems fail to be resized, use the snapshot that you created in Step 1 to roll back the disk.

## Operating systems that support online resizing

The following Linux public images and custom images derived from these public images support online resizing:

-   Alibaba Cloud Linux: Alibaba Cloud Linux 2.1903 LTS 64-bit
-   CentOS:
    -   CentOS 6: CentOS 6.8 and later
    -   CentOS 7: CentOS 7.2 and later
    -   CentOS 8 and later
-   Red Hat Enterprise Linux \(RHEL\):
    -   RHEL 6: RHEL 6.9 and later
    -   RHEL 7: RHEL 7.4 and later
    -   RHEL 8 and later
-   Ubuntu: Ubuntu 16 and later
-   Debian: Debian 8 and later
-   SUSE: SUSE 12 SP2 and later
-   openSUSE: openSUSE 42.3 and later

## Troubleshooting

-   **Problem description**: When the `growpart /dev/vda 1` command is being run, the `unexpected output in sfdisk --version [sfdisk, from util-linux 2.23.2]` error is prompted.

    **Solution**:

    1.  Run the `locale` command to view the character encoding type of the ECS instance. If the character encoding type is not en\_US.UTF-8, switch it to en\_US.UTF-8.
        1.  Run the following command to switch the character encoding type:

            ```
            LANG=en_US.UTF-8
            ```

        2.  If the problem persists, run the following command to switch the character encoding type:

            ```
            export LC_ALL=en_US.UTF-8
            ```

        3.  If the problem still persists, run the following command to switch the character encoding type:

            ```
            localectl set-locale LANG=en_US.UTF-8
            ```

        4.  If the preceding solutions cannot solve the problem, run the following command to switch the character encoding type:

            ```
            export LANGUAGE=en_US.UTF-8
            ```

    2.  If the problem remains unsolved, run the `reboot` command to restart the ECS instance.
    **Note:**

    After you resize the partition by switching the character encoding type, we recommend that you switch back to the original character encoding type.

-   **Problem description**: When the `growpart /dev/vda 1` command is being run, the `-bash: growpart: command not found` error is prompted.

    **Solution**:

    1.  Run the `uname -a` command to check the version of the Linux kernel. The procedure described in this topic applies to Linux kernel 3.6.0 and later.

        If the version of the Linux kernel is earlier than 3.6.0, you can extend partitions of a disk on the instance. For more information, see [Procedure for instances with kernels earlier than 3.6.0](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md) and [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md).

    2.  Install the growpart tool.
        -   Run the following command if the instance that runs CentOS 7 and later:

            ```
            yum install -y cloud-utils-growpart
            ```

        -   Run the following command if the instance that runs Debian 9 and later or Ubuntu 14 and later:

            ```
            apt install -y cloud-guest-utils
            ```

-   **Problem description**: You cannot install the growpart tool on instances that run CentOS 6.5 to resize partitions.

    **Solution**: If the Linux kernel version of CentOS 6 is earlier than 3.6.0, you can perform the following steps to use the growpart tool on instances that run CentOS 6:

    1.  Change the source address of a YUM repository on CentOS 6. For more information, see [Change the CentOS 6 source address](/intl.en-US/Images/FAQ/Change the CentOS 6 source address.md).

        **Note:** CentOS 6 has reached its end of life \(EOL\). To install the software package on CentOS 6 by using YUM, change the source address of a YUM repository.

    2.  Install the dracut-modules-growroot tool on instances that run CentOS 6 to resize the partitions of disks. For more information, see [Procedure for instances with kernels earlier than 3.6.0](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md).

## Other scenarios for disk resizing

-   If you want to create partitions on a resized data disk, see [Option 2: Add and format MBR partitions](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_gg7_ilv_h3j) or [Option 4: Add and format GPT partitions](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_4hl_5l7_87s).
-   If a raw data disk contains a file system but no partitions, see [Option 5: Resize the file system of a raw data disk](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_f88_ax7_y8i).

**Related topics**  


[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

[ResizeDisk](/intl.en-US/API Reference/Disk/ResizeDisk.md)

[AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md)

