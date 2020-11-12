---
keyword: [replace the operating system, replace the image, re-install the system, re-install the Windows system, re-install the Linux system]
---

# Replace a system disk \(non-public images\)

You can replace the operating system of an instance by replacing its system disk. To replace the system disk, you must assign a new system disk to the ECS instance. The original system disk is released and the system disk ID is updated. The disk category, the IP addresses of the instance, and MAC addresses of the elastic network interfaces \(ENIs\) that are bound to the instance remain unchanged. If you want to use a different operating system, you can replace the system disk to replace the operating system.

-   After the system disk is replaced, the original system disk is released. We recommend that you create snapshots to back up disk data before you replace the system disk. For more information, see [Create a snapshot](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).

    **Note:** Create snapshots during off-peak hours to minimize the impact on your business. It takes about 20 minutes to create the initial snapshot of a 40 GiB system disk. We recommend that you plan accordingly before you create a snapshot.

-   The instance is in the **Stopped** state. For information about how to stop an instance, see [Stop an instance](/intl.en-US/Instance/Manage instances/Stop an instance.md).

    **Warning:**

    -   When you stop an instance, services that run on the instance may be interrupted. Proceed with caution.
    -   If the instance is a pay-as-you-go instance and is in the No Fees for Stopped Instances \(VPC-Connected\) state, it may not be able to start after you replace the system disk. We recommend that you select **Retain Instance and Continue Charging After Instance Is Stopped** when you stop the instance.

It is a high-risk operation to replace a system disk. Before you perform this operation, read and understand the following precautions:

-   You must redeploy the runtime environment on the new system disk. Your services may be stopped for an extended period of time.
-   Snapshots of the original system disk cannot be used to roll back the new system disk.
-   Manual snapshots are not released and can continue to be used to create custom images. If the Delete Automatic Snapshots While Releasing Disk feature is enabled on the original system disk, automatic snapshots are automatically deleted.
-   For example, assume that the original and new operating systems are Linux systems, data disks are attached to the instance, and automatic partition mounting at system startup is enabled. After the system disk is replaced, the mounting configuration of the data disk partitions in the original system disk is lost. You must manually update configurations in the /etc/fstab file. For more information, see the [What to do next](#postreq_whatToDoNext) section.
-   If you want to replace the system disk between different operating system families, take note of the following items:
    -   For regions outside mainland China, you cannot replace a system disk with a disk of a different operating system family. The system supports only replacement among different Linux distributions or among different Windows Server versions.
    -   Make sure that the hostname of the instance meets the requirements of the new operating system, and delete invalid characters. For more information about how to modify the hostname, see [Modify the properties of an instance](/intl.en-US/Instance/Manage instances/Modify the properties of an instance.md) or [ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md).
    -   When you replace a Windows Server operating system with a Linux operating system, you can select an SSH key pair for authentication. For this step, you must have an existing SSH key pair. For more information, see [Create an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Create an SSH key pair.md).
    -   Linux systems that use the default configuration do not recognize files in the NTFS format and Windows Server systems that use the default configuration do not recognize files in the ext3, ext4, or XFS format. You can select one of the following recommendations based on your data disks:
        -   If your data disks do not contain important data, re-initialize the data disks and format them to file systems that are supported by the new operating system. For more information, see [Re-initialize a data disk](/intl.en-US/Block Storage/Cloud disks/Reinitialize a cloud disk/Re-initialize a system disk.md).
        -   If your data disks contain important data, separately install software identifiers such as NTFS-3G when Windows Server is replaced with Linux, or Ext2Read and Ext2Fsd when Linux is replaced with Windows Server.
-   If you want to replace the operating system with Windows Server, take note of the following items:
    -   The system disk must have at least 1 GiB space reserved. Otherwise, the ECS instance may not be able to start after the system disk is replaced.
    -   Microsoft no longer offers support for Windows Server 2003. To ensure your data security, we recommend that you do not use Windows Server 2003 for your ECS instances. Alibaba Cloud no longer provides Windows Server 2003 images. For more information, see [Offline announcement of Windows Server 2003 system image](https://www.alibabacloud.com/help/faq-detail/59513.htm).
    -   If your instance is a non-I/O optimized instance, you can call only the ReplaceSystemDisk operation to replace the operating system with only the specified Windows Server public images. For more information, see [Replace the system disk \(public images\)](/intl.en-US/Block Storage/Cloud disks/Change the operating system/Replace the system disk (public images).md).

In addition to replacing system disks one by one in the ECS console, you can also use the ACS-ECS-BulkyReplaceSystemDisk public template of OOS to replace multiple system disks at a time. For more information, go to the [OOS console](https://oos.console.aliyun.com/cn-hangzhou/execution/create/ACS-ECS-BulkyReplaceSystemDisk).

## Procedure

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the instance for which you want to replace the system disk.

5.  In the **Actions** column, choose **More** \> **Disk and Image** \> **Replace System Disk**.

6.  In the message that appears, read the precautions for replacing the system disk, and then click **OK**.

7.  On the Change Operating System page, configure the following parameters:

    1.  **Image**: Select **Custom Image**, **Shared Image**, or **Marketplace Image**, and select an image version.

    2.  **System Disk**: The category of the system disk cannot be changed. Configure the capacity of the system disk based on your business needs and the new image. The new capacity must be greater than or equal to the current capacity of the system disk.

        The minimum disk capacity is determined by the current disk capacity and the image type, while the maximum disk capacity is 500 GiB.

        |Image|Size range of a resized system disk \(GiB\)|
        |:----|:------------------------------------------|
        |CoreOS and FreeBSD|\[Max\{30, the size of the system disk before resizing\}, 500\]|
        |Other Linux distributions|\[Max\{20, the size of the system disk before resizing\}, 500\]|
        |Windows Server|\[Max\{40, the size of the system disk before resizing\}, 500\]|

        **Note:** If you have renewed and downgraded your instance, the system disk capacity cannot be modified until the next subscription period starts.

    3.  **Security Settings**:

        -   Windows Server instances support only password authentication.
        -   If the instance is an I/O optimized instance and the operating system is Linux, you can use a password or an SSH key pair for authentication.
    4.  Read and select **ECS Service Terms**.

    5.  **Price**: The fees of the image and the system disk are included. For more information about prices of system disks, see [Pricing](https://www.alibabacloud.com/product/ecs#pricing).

    6.  Confirm settings and click **Create Order**.


It takes about 10 minutes to replace the system disk. After the system disk is replaced, the instance automatically enters the **Running** state. Click the instance ID to go to the **Instance Details** page and view the new image.

After the system disk is replaced, you can perform the following operations:

-   Optional. After the system disk is replaced, the automatic snapshot policy applied to the original disk automatically becomes invalid and you must configure an automatic snapshot policy for the new system disk. For more information, see [Apply or disable an automatic snapshot policy](/intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md).
-   You must ensure that your snapshot quota is sufficient to configure an automatic snapshot policy for the new system disk. You can delete unneeded snapshots of the original system disk. For more information, see [Delete a snapshot](/intl.en-US/Snapshots/Use snapshots/Delete a snapshot.md).
-   Optional. For Linux instances only: Write the new partition information to the /etc/fstab file of the new system disk and mount the partitions. Data disks do not need to be formatted and partitioned. The following list provides the corresponding procedure. For more information about the specific commands, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md).

    1.  Recommended. Back up the /etc/fstab file.
    2.  Write the new partition information to the /etc/fstab file.
    3.  View the new partition information in the /etc/fstab file.
    4.  Run the `mount` command to mount the partitions.
    5.  Run the `df -h` command to query the file system space and usage.
    After the partitions are mounted, you can use the data disks without restarting the instance.


**Related topics**  


[ReplaceSystemDisk](/intl.en-US/API Reference/Disk/ReplaceSystemDisk.md)

