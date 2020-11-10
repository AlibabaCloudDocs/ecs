---
keyword: [partition, partition and format, larger than 2 TiB, data disk, parted, GPT]
---

# Partition and format a data disk larger than 2 TiB

This topic describes how to partition and format a data disk larger than 2 TiB in different operating systems.

-   A data disk is attached to an ECS instance. For more information, see [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md).
-   A remote connection is established to the ECS instance. For more information about how to connect to an ECS instance, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

-   The amount of time required to create a snapshot of a data disk is proportional to the volume of data stored on the data disk. The more data stored on the disk, the longer it takes to create a snapshot.
-   Alibaba Cloud Elastic Block Storage \(EBS\) supports the master boot record \(MBR\) and GUID partition table \(GPT\) partition formats. MBR is applicable to data disks up to 2 TiB in size and can be used to create up to four primary partitions. If you want to partition a data disk larger than 2 TiB, you must use the GPT partition format.

    **Note:** Conversion between MBR and GPT may cause data loss. When you create a disk from a snapshot or resize a disk, and you expect the resulting disk size to exceed 2 TiB, we recommend that you check whether the disk uses the MBR partition format. If the disk uses the MBR partition format and you want to retain the disk data when you change the partition format, we recommend that you create and attach a new data disk to the instance. Partition and format the new data disk to GPT, and then copy data from the original data disk to the new data disk.

-   To partition and format a data disk larger than 2 TiB, we recommend that you use the partition tools, partition format, and file systems described in the following table.

    |Operating system|Partition tool|Partition format|File system|
    |:---------------|:-------------|----------------|:----------|
    |Windows|**Disk Management**|GPT|NTFS|
    |Linux|parted|GPT|ext4 or XFS|


## Partition and format a data disk larger than 2 TiB on a Windows instance

This section describes how to partition and format a data disk larger than 2 TiB on a Windows instance. Windows Server 2012 R2 64-bit is used in this example.

1.  On the Windows Server desktop, press Win+R.

2.  In the Run dialog box, enter diskmgmt.msc and click **OK** to open Disk Management.

3.  Find the disk to be partitioned and formatted. **Disk 1** is used in this example. The disk is in the **Offline** state.

4.  Right-click the blank next to **Disk 1** and select **Online**.

    After **Disk 1** comes online, it enters the **Not Initialized** state.

5.  Right-click the blank next to **Disk 1** and select **Initialize Disk**.

6.  In the Initialize Disk dialog box, select **Disk 1** and select **GPT \(GUID Partition Table\)** as the disk partition format.

7.  In the Disk Management window, right-click the **Unallocated** section of **Disk 1**, and then select **New Simple Volume** to create a 4 TiB volume in the NTFS format.

8.  In the New Simple Volume Wizard window, click **Next** and perform the following operations:

    1.  Specify Volume Size: Specify the size of the simple volume. If you want to create only one primary partition, use the default value. Click **Next**. You can also divide **Disk 1** into multiple partitions.

        **Note:** In theory, the maximum NTFS volume size is 264−1 clusters. However, the maximum NTFS volume size implemented in Windows XP Pro is 232−1 clusters. For example, if the cluster size is 64 KiB, the maximum NTFS volume size is 256 TiB. If the cluster size is 4 KiB, the maximum NTFS volume size is 16 TiB. NTFS automatically selects a cluster size based on the disk capacity.

    2.  Assign Drive Letter or Path: Select a drive letter. D is used in this example. Click **Next**.

    3.  Format Partition: Select the formatting settings such as the file system, allocation unit size, and volume label, and then determine whether to select **Perform a quick format** and **Enable file and folder compression**. In this example, **Perform a quick format** is selected. Click **Next**.

    4.  After a new simple volume is created, click **Finish** to close the New Simple Volume Wizard window.


## Convert the partition format of a data disk on a Windows instance

**Note:** Conversion between partition formats may cause data loss. Make sure that you have backed up the data on the disk before you convert the disk to a different partition format.

This section describes how to convert the partition format of a 3 TiB data disk on a Window instance. Windows Server 2012 R2 64-bit is used in this example.

1.  On the Windows Server desktop, right-click the **Start** icon and select **Disk Management**.

2.  Find the disk to be converted. **Disk 2** is used in this example.

3.  Right-click a simple volume and select **Delete Volume**.

4.  Right-click the blank next to Disk 2, and select **Convert to GPT Disk**.

5.  In the Disk Management window, right-click the **Unallocated** section of Disk 2, and then select **New Simple Volume** to create a 3 TiB volume in the NTFS format.

6.  In the New Simple Volume Wizard window, click **Next** and perform the following operations:

    1.  Specify Volume Size: Specify the size of the simple volume. If you want to create only one primary partition, use the default value. Click **Next**. You can also divide **Disk 2** into multiple partitions.

        **Note:** In theory, the maximum NTFS volume size is 264−1 clusters. However, the maximum NTFS volume size implemented in Windows XP Pro is 232−1 clusters. For example, if the cluster size is 64 KiB, the maximum NTFS volume size is 256 TiB. If the cluster size is 4 KiB, the maximum NTFS volume size is 16 TiB. NTFS automatically selects a cluster size based on the disk capacity.

    2.  Assign Drive Letter or Path: Select a drive letter. E is used in this example. Click **Next**.

    3.  Format Partition: Select the formatting settings such as the file system, allocation unit size, and volume label, and then determine whether to select **Perform a quick format** and **Enable file and folder compression**. In this example, **Perform a quick format** is selected. Click **Next**.

    4.  After a new simple volume is created, click **Finish** to close the New Simple Volume Wizard window.


## Partition and format a data disk larger than 2 TiB on a Linux instance

This section describes how to use the parted and e2fsprogs tools to partition and format a data disk larger than 2 TiB on a Linux instance. Alibaba Cloud Linux 2.1903 LTS 64-bit is used in this example. Assume that the data disk is a new 3 TiB empty disk and its device name is /dev/vdb.

Prerequisites: The parted and e2fsprogs tools are installed on your Linux instance.

```
[root@ecshost~ ]# yum install -y parted
[root@ecshost~ ]# yum install -y e2fsprogs
```

Perform the following operations to partition and format a data disk larger than 2 TiB and mount the file system:

1.  Run the `fdisk -l` command to check whether the data disk exists.

    The expected command output is similar to the following example. If different information is returned, the data disk is not attached to the instance.

    ```
    [root@ecshost~ ]# fdisk -l
    Disk /dev/vdb: 3221.2 GB, 3221225472000 bytes, 6291456000 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    ```

2.  Run the `parted /dev/vdb` command to start partitioning the disk.

    1.  Run the `mklabel gpt` command to convert the partition format from MBR to GPT.

    2.  Run the `mkpart primary 1 100%` command to create a primary partition and specify the start and end sectors for the partition.

    3.  Run the `align-check optimal 1` command to check partition alignment.

        **Note:** If `1 not aligned` is returned, the partition is not aligned. We recommend that you run the following commands and use the `(<optimal_io_size> + <alignment_offset>)/<physical_block_size>` formula to obtain the start sector number to align the partition for optimal performance. For example, if the start sector number is 1024, you can then run the `mkpart primary 1024s 100%` command to recreate a new primary partition.

        ```
        [root@ecshost~ ]# cat /sys/block/vdb/queue/optimal_io_size
        [root@ecshost~ ]# cat /sys/block/vdb/queue/minimum_io_size
        [root@ecshost~ ]# cat /sys/block/vdb/alignment_offset
        [root@ecshost~ ]# cat /sys/block/vdb/queue/physical_block_size
        ```

    4.  Run the `print` command to view the partition table.

        ```
        (parted) mklabel gpt
        (parted) mkpart primary 1 100%
        (parted) align-check optimal 1
        1 aligned
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 3221GB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        Number Start End Size File system Name Flags
        1 17.4kB 3221GB 3221GB primary
        ```

    5.  Run the `quit` command to exit the parted tool.

3.  Run the `partprobe` command to enable the system to re-read the partition table.

4.  Run one of the following commands to create a file system for the /dev/vdb1 partition:

    Run one of the following commands to create a file system based on your needs:

    -   Create an ext4 file system.

        ```
        [root@ecshost~ ]# mkfs -t ext4 /dev/vdb1
        ```

    -   Create an XFS file system.

        ```
        [root@ecshost~ ]# mkfs -t xfs /dev/vdb1
        ```

    **Note:**

    -   If the capacity of the data disk is 16 TiB, you must format the disk by using the specified version of e2fsprogs. For more information, see the [Appendix 1: Update e2fsprogs on a Linux instance](#e2fsprogs) section.
    -   If you want to disable the lazy init feature of an ext4 file system to avoid impact on the I/O performance of data disks, see the [Appendix 2: Disable the lazy init feature on a Linux instance](#LazyInit) section.
5.  Run the `mkdir /test` command to create a mount point named /test.

6.  Run the `mount /dev/vdd1 /test` command to mount the /dev/vdb1 partition to /test.

7.  Run the `df -h` command to view the current disk space and usage.

    If the command output shows information about the newly created file system, the mount operation is successful. You can use the new file system.

    ```
    [root@ecshost~ ]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 6.4G 31G 18% /
    devtmpfs 487M 0 487M 0% /dev
    tmpfs 497M 0 497M 0% /dev/shm
    tmpfs 497M 364K 496M 1% /run
    tmpfs 497M 0 497M 0% /sys/fs/cgroup
    tmpfs 100M 0 100M 0% /run/user/0
    /dev/vdb1 2.9T 89M 2.8T 1% /test
    ```

8.  \(Recommended\) Write new partition information to /etc/fstab so that the partition is automatically mounted at system startup.

    1.  Run the `cp /etc/fstab /etc/fstab.bak` command to back up etc/fstab.

    2.  Run the following command to write information of the new partition to /etc/fstab:

        ```
        echo `blkid /dev/vdb1 | awk '{print $2}' | sed 's/\"//g'` /test ext4 defaults 0 0 >> /etc/fstab
        ```

        **Note:** We recommend that you use a universally unique identifier \(UUID\) to reference the new partition in /etc/fstab. You can run the blkid command to obtain the UUID of the new partition.

    3.  Run the `cat /etc/fstab` command to check the information of /etc/fstab.

        If the new partition information appears in the command output, the write operation is successful.


The 3 TiB data disk is partitioned and formatted.

## Appendix 1: Update e2fsprogs on a Linux instance

If the disk capacity is 16 TiB, you must use e2fsprogs 1.42 or later to format the partitions of the disk to ext4. If e2fsprogs of a version earlier than 1.42 is used, the following error occurs:

```
mkfs.ext4: Size of device /dev/vdb too big to be expressed in 32 bits using a blocksize of 4096.            
```

Perform the following operations to install a later version of e2fsprogs. In this example, e2fsprogs 1.42.8 is used.

1.  Run the `rpm -qa | grep e2fsprogs` command to check the current e2fsprogs version.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5772909951/p4439.png)

    If the version is earlier than 1.42, perform the following operations to update the software.

2.  Run the following command to download e2fsprogs 1.42.8. You can visit [e2fsprogs](https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/?spm=a2c4g.11186623.2.14.Pb5baW) to obtain the latest software package.

    ```
    wget https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/e2fsprogs-1.42.8.tar.gz
    ```

3.  Run the following commands to compile the tool of a later version:

    ```
    tar xvzf e2fsprogs-1.42.8.tar.gz
    cd e2fsprogs-1.42.8
    ./configure
    make
    make install
    ```

4.  Run the following command to check whether e2fsprogs is updated:

    ```
    rpm -qa | grep e2fsprogs
    ```


## Appendix 2: Disable the lazy init feature on a Linux instance

By default, the lazy init feature of an ext4 file system is enabled. When this feature is enabled, the instance initiates a thread to continuously initialize the metadata of the ext4 file system. If you partition and format a data disk when this feature is enabled, the IOPS of the disk may be affected for a short period after the disk is formatted.

If you want to test the performance of a data disk immediately after the disk is formatted, run the following command to disable the lazy init feature when you format the file system:

```
mke2fs -O 64bit,has_journal,extents,huge_file,flex_bg,uninit_bg,dir_nlink,extra_isize -E lazy_itable_init=0,lazy_journal_init=0   /dev/vdb1
```

**Note:** If the lazy init feature is disabled, it may take an extended period of time to format the file system. For example, the file system of a 32 TiB data disk may take 10 to 30 minutes to format. Choose whether to disable the lazy init feature based on your business requirements.

