---
keyword: [ECS, disk resizing, extend a partition]
---

# Resize disks offline for Linux instances

You can resize a system disk or a data disk to extend its capacity. If your Linux ECS instance does not support online resizing of disks, you can resize the disks on the instance offline. You must restart the instance after you resize a disk offline for the change to take effect. This will cause your business to be interrupted for a short period of time. We recommend that you resize disks offline at off-peak hours.

The disk to be resized offline and the instance to which the disk is attached meet the following requirements.

|Resource|Requirement|
|--------|-----------|
|Instance|-   The instance is in the **Running** \(Running\) or **Stopped** \(Stopped\) state.
-   The version of the Linux kernel of the instance is 3.6.0 or later. You can run the `uname -a` command to check the kernel version.

If the version of the Linux kernel is earlier than 3.6.0, you can extend partitions of a disk on the instance. For more information, see [Procedure for instances with kernels earlier than 3.6.0](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md) and [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md). |
|Disk|-   The disk is in the **In Use** \(In Use\) state.
-   The disk is an enhanced SSD \(ESSD\), a standard SSD, or an ultra disk.
-   After you renew a subscription instance and downgrade its configurations, you cannot resize the subscription disks on the instance for the remainder of the current billing cycle.

**Note:** A disk in the master boot record \(MBR\) partition format cannot be resized to 2 TiB or greater in size. To resize an MBR disk to larger than 2 TiB, we recommend that you create a new disk larger than 2 TiB, partition and format the new disk the GUID Partition Table \(GPT\) format, and then copy data from the original MBR disk to the new GPT disk. For more information about how to use the GPT format to partition and format disks, see [Partition and format a data disk larger than 2 TiB](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md). |

The following table lists configurations of the instance and disks that are used in the examples of this topic.

|Resource|Description|
|--------|-----------|
|Image used by the instance|Alibaba Cloud Linux 2.1903 LTS 64-bit public image|
|System disk|/dev/vda: uses the MBR partition format and ext4 file system, and is resized from 40 GiB to 60 GiB.|
|Data disks|-   /dev/vdb: uses the MBR partition format and ext4 file system, and is resized from 40 GiB to 60 GiB.
-   /dev/vdc: uses the GPT partition format and xfs file system, and is resized from 40 GiB to 60 GiB. |

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


## Step 3: View the disk partitions

Log on to the ECS instance to view the partition types \(MBR and GPT\) and file system types \(such as ext4 and xfs\) of the system disk and data disks. Subsequent resizing operations vary based on the types of the partitions and file systems.

1.  Connect to the ECS instance. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

2.  Run the following command view the disks attached to the instance:

    ```
    fdisk -lu
    ```

    The following figure shows a partition of the system disk \(/dev/vda\) and two partitions of data disks \(/dev/vdb and /dev/vdc\).

    ![View the partitions of the disks](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2256420061/p135832.png)

    |No.|Partition|Description|
    |---|---------|-----------|
    |①|`/dev/vda1`|The partition of the system disk. The **System** value of **Linux** indicates that the partition is in the MBR format.|
    |②|`/dev/vdb1`|A partition of a data disk. The **System** value of **Linux** indicates that the partition is in the MBR format.|
    |③|`/dev/vdc1`|A partition of a data disk. The **System** value of **GPT** indicates that the partition is in the GPT format.|

3.  Run the following command to check the file system types of the existing partitions:

    ```
    df -Th
    ```

    An output similar to the following one is displayed:

    ![View the file systems](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135833.png)


## Step 4: Resize partitions

When you view the disk partitions, you can find that the partitions and file systems within the ECS instance have not been resized. This step describes how to resize the partitions of the resized disk within the ECS instance.

1.  Install the gdisk tool on the ECS instance.

    You must perform this step if the partitions are in the GPT format. Skip this step if the partitions are in the MBR format.

    ```
    yum install gdisk -y
    ```

2.  Install the growpart tool.

    -   Run the following command if the instance runs a CentOS 7 or later operating system:

        ```
        yum install -y cloud-utils-growpart
        ```

    -   Run the following command if the instance runs a Debian 9 or later operating system or a Ubuntu 14 or later operating system:

        ```
        apt install -y cloud-guest-utils
        ```

3.  Run the following command to resize partitions:

    ```
    growpart /dev/vda 1
    ```

    In this example, the partition of the system disk is resized. Use a space to separate `/dev/vda` and `1`. To resize other partitions, modify the command accordingly. An output similar to the following one is displayed:

    ![growpart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135834.png)

    **Note:** When you perform this step, the `unexpected output in sfdisk --version [sfdisk, from util-linux 2.23.2]` error may be prompted. For information about how to troubleshoot the error, see FAQ.


## Step 5: Resize file systems

This step describes how to resize the file system of a partition within an ECS instance.

1.  Resize the file systems within the ECS instance based on the file system types that you obtained.

    -   To resize ext\* \(such as ext4\) file systems, run the following commands.

        To resize the file system of the /dev/vda1 partition of the system disk, run the following command:

        ```
        resize2fs /dev/vda1    
        ```

        To resize the file system of the /dev/vdb1 partition of a data disk, run the following command:

        ```
        resize2fs /dev/vdb1          
        ```

        **Note:** `/dev/vda1` and `/dev/vdb1` are partition names. Change the commands based on your partition names.

    -   To resize xfs file systems, run the following command:

        ```
        xfs_growfs /media/vdc
        ```

        **Note:** `/media/vdc` is the mount point of the `/dev/vdc1` partition. Change the command based on the mount point of your partition.

2.  Run the following command to check the resizing results:

    ```
    df -Th
    ```

    An output similar to the following one is displayed:

    ![Check the resizing results](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5082909951/p135835.png)

    After the disk is resized, check whether the new capacity of the disk is as expected.

    -   If the file systems are resized and the business programs in the instance can run properly, the resizing operation is complete.
    -   If the file systems fail to be resized, use the snapshot that you created in Step 1 to roll back the disk.

## FAQ

-   Problem description: When the `growpart /dev/vda 1` command is run, the `unexpected output in sfdisk --version [sfdisk, from util-linux 2.23.2]` error is prompted.

    Solution:

    1.  Run the following command to change the character encoding type of the ECS instance:

        ```
        LANG=en_US.UTF-8
        ```

    2.  If the problem persists, run the `reboot` command to restart the ECS instance.
    3.  If the problem persists after the instance is restarted, run the following command to modify the local environment variable, and then restart the instance again:

        ```
        localectl set-locale LANG=en_US.UTF-8
        ```

    If you are using a CentOS 8 image and the preceding solution cannot solve the problem, run the following command to change the character encoding type:

    ```
    export LANGUAGE=en_US.UTF-8
    ```

-   Problem description: When the `growpart /dev/vda 1` command is run, the `-bash: growpart: command not found` error is prompted.

    Solution:

    1.  Run the `uname -a` command to check the version of the Linux kernel. The procedure described in this topic applies to Linux kernel 3.6.0 and later.

        If the version of the Linux kernel is earlier than 3.6.0, you can extend partitions of a disk on the instance. For more information, see [Procedure for instances with kernels earlier than 3.6.0](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md) and [Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md).

    2.  Install the growpart tool.
        -   Run the following command if the instance runs a CentOS 7 or later operating system:

            ```
            yum install -y cloud-utils-growpart
            ```

        -   Run the following command if the instance runs a Debian 9 or later operating system or a Ubuntu 14 or later operating system:

            ```
            apt install -y cloud-guest-utils
            ```


## Other scenarios for disk resizing

-   If you want to create partitions on the resized data disk, see [Option 2: Add and format MBR partitions](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_gg7_ilv_h3j) or [Option 4: Add and format GPT partitions](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_4hl_5l7_87s).
-   If no partition is created on your data disk and a file system is created on the raw device, extend the file system. For more information, see [Option 5: Resize the file system of a raw data disk](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.mdsection_f88_ax7_y8i).

**Related topics**  


[RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md)

[ResizeDisk](/intl.en-US/API Reference/Disk/ResizeDisk.md)

[AttachDisk](/intl.en-US/API Reference/Disk/AttachDisk.md)

