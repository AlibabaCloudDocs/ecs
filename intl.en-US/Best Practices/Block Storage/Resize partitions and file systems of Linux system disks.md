# Resize partitions and file systems of Linux system disks

This topic describes how to use the growpart and resize2fs tools to resize partitions and file systems of Linux system disks.

Before you resize partitions and file systems of system disks, make sure that the following requirements are met:

1.  A snapshot is created to back up data.

    To prevent data loss caused by incorrect operations, we recommend that you create a snapshot to back up your data. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a snapshot for a disk.md).

2.  A data disk is resized in the console.

    If no data disks are resized, see [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md) or [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md) to resize a data disk.

3.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).
4.  The growpart or xfsprogs tool is installed based on your operating system.

    -   Alibaba Cloud Linux 2 and CentOS 7

        Run the `yum install <Package name\>` command to install the tools.

        ```
        yum install cloud-utils-growpart xfsprogs -y
        ```

    -   Ubuntu 14, Ubuntu 16, Ubuntu 18, and Debian 9

        Run the `apt install <Package name\>` command to install the tools.

        ```
        apt install cloud-guest-utils xfsprogs -y
        ```

    -   Debian 8, openSUSE 42.3, openSUSE 13.1, and SUSE Linux Enterprise Server 12 SP2

        Use the upstream version of the growpart or xfsprogs tool.

    **Note:** If the partition or file system cannot be resized due to issues with the growpart or xfsprogs tool, we recommend that you re-install the tool.

5.  Run the `uname -a` command to check the kernel version of the instance operating system.
    -   If the kernel version of your instance operating system is 3.6.0 or later, see the "[Procedure for instances with kernels 3.6.0 or later](#section_gxq_3tw_dhb)" section of this topic.
    -   If the kernel version of an instance operating system such as CentOS 6, Debian 7, or SUSE Linux Enterprise Server 11 SP4 is earlier than 3.6.0, you must restart the instance by using the console or by calling an API operation to resize the partition or file system. For more information, see the "[Procedure for instances with kernels earlier than 3.6.0](#section_vxq_3tw_dhb)" section of this topic.

The procedures in this topic apply to disks that have the following partition formats and file system types:

-   Partition formats: master boot record \(MBR\) and GUID Partition Table \(GPT\)
-   File system types: ext, XFS, and Btrfs

## Procedure for instances with kernels 3.6.0 or later

In this example, Alibaba Cloud Linux 2.1903 LTS 64-bit is used to describe how to resize partitions and file systems.

**Note:** The commands used in the following examples also apply to CentOS 7.

1.  Run the following command to check the size of the system disk:

    ```
    fdisk -l
    ```

    In the following example command output, the size of the /dev/vda disk is 100 GiB:

    ```
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes, 209715200 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000bad2b
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83886046    41941999   83  Linux
    ```

2.  Run the following command to check the size of the partition and the type of the file system:

    ```
    df -Th
    ```

    In the following example command output, the size of the /dev/vda1 partition is 40 GiB, and the type of the file system is ext4:

    ```
    [root@ecshost ~]# df -Th
    Filesystem     Type      Size  Used Avail Use% Mounted on
    devtmpfs       devtmpfs  869M     0  869M   0% /dev
    tmpfs          tmpfs     879M     0  879M   0% /dev/shm
    tmpfs          tmpfs     879M  460K  878M   1% /run
    tmpfs          tmpfs     879M     0  879M   0% /sys/fs/cgroup
    /dev/vda1      ext4       40G  1.8G   36G   5% /
    tmpfs          tmpfs     176M     0  176M   0% /run/user/0
    ```

3.  Run the following command to resize partitions:

    ```
    growpart <DeviceName\> <PartionNumber\>
    ```

    In the following example command output, the first partition /dev/vda1 of the system disk is resized:

    ```
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=83883999 end=83886047 new: size=209713119 end=209715167
    ```

    **Note:** If the `unexpected output in sfdisk --version [sfdisk, from util-linux 2.23.2]` error is prompted when you run the `growpart /dev/vda 1` command, try to change the character encoding to fix the problem. For more information, see [FAQ](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md).

4.  Resize the file system.

    Run the `df -Th` command to check the type of the file system. Then, use one of the following methods to resize the file system based on the type of the file system:

    -   If the type of the file system is ext such as ext3 and ext4, run the following command to resize the file system:

        ```
        resize2fs <PartitionName\>
        ```

        In the following example command output, the file system of the /dev/vda1 partition is resized:

        ```
        [root@ecshost ~]# resize2fs /dev/vda1
        resize2fs 1.42.9 (28-Dec-2013)
        Filesystem at /dev/vda1 is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 7
        The filesystem on /dev/vda1 is now 26214139 blocks long.
        ```

    -   If the type of the file system is XFS, run the following command to resize the file system:

        ```
        xfs_growfs <mountpoint\>
        ```

        In the following example command output, the file system of the /dev/vda1 partition is resized. The mount point of the /dev/vda1 partition is the / root directory.

        ```
        [root@ecshost ~]# xfs_growfs /
        meta-data=/dev/vda1              isize=512    agcount=13, agsize=1310656 blks
                 =                       sectsz=512   attr=2, projid32bit=1
                 =                       crc=1        finobt=1, sparse=1, rmapbt=0
                 =                       reflink=1
        data     =                       bsize=4096   blocks=15728379, imaxpct=25
                 =                       sunit=0      swidth=0 blks
        naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
        log      =internal log           bsize=4096   blocks=2560, version=2
                 =                       sectsz=512   sunit=0 blks, lazy-count=1
        realtime =none                   extsz=4096   blocks=0, rtextents=0
        data blocks changed from 15728379 to 20971259
        ```

        **Note:** The commands may vary based on versions of the xfs\_growfs tool. Run `xfs_growfs --help` to check the corresponding commands.

5.  Run the following command to view the results of disk resizing:

    ```
    df -h
    ```

    In the following example command output, the size of the /dev/vda1 partition is 100 GiB. This indicates that the partition is resized.

    ```
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    devtmpfs        869M     0  869M   0% /dev
    tmpfs           879M     0  879M   0% /dev/shm
    tmpfs           879M  492K  878M   1% /run
    tmpfs           879M     0  879M   0% /sys/fs/cgroup
    /dev/vda1        99G  1.8G   93G   2% /
    tmpfs           176M     0  176M   0% /run/user/0
    ```


## Procedure for instances with kernels earlier than 3.6.0

In this example, CentOS 6 is used to describe how to resize partitions and file systems.

1.  Change the source address of a YUM repository on CentOS 6:

    CentOS 6 has reached its end of life \(EOL\). To install the software package on CentOS 6 by using YUM, you must change the source address of a YUM repository. For more information, see [Change the CentOS 6 source address](/intl.en-US/Images/FAQ/Change the CentOS 6 source address.md).

2.  Run the following command to install the dracut-modules-growroot tool:

    ```
    yum install -y dracut-modules-growroot
    ```

    **Note:** If a package manager other than YUM is used, change yum in the preceding command based on the package manager.

3.  Run the following command to overwrite the existing initramfs file:

    ```
    dracut -f
    ```

4.  Run the following command to check the disk and partition information:

    -   Check the size of the disk:

        ```
        fdisk -l
        ```

        In the following example command output, the size of the /dev/vda disk is 100 GiB:

        ```
        [root@ecshost ~]# fdisk -l
        Disk /dev/vda: 107.4 GB, 107374182400 bytes
        255 heads, 63 sectors/track, 13054 cylinders
        Units = cylinders of 16065 * 512 = 8225280 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk identifier: 0x0003a7b4
        
           Device Boot      Start         End      Blocks   Id  System
        /dev/vda1   *           1        2611    20970496   83  Linux
        ```

    -   Check the partition of the disk and the type of the file system:

        ```
        df -Th
        ```

        In the following example command output, the size of the /dev/vda1 partition is 20 GiB, and the type of the file system is ext4:

        ```
        [root@ecshost ~]# df -h
        Filesystem     Type      Size  Used Avail Use% Mounted on
        /dev/vda1      ext4       20G  1.1G   18G   6% /
        tmpfs          tmpfs     7.8G     0  7.8G   0% /dev/shm
        ```

5.  Run the following command to resize partitions:

    ```
    growpart <DeviceName\> <PartionNumber\>
    ```

    In the following example command output, the first partition /dev/vda1 of the system disk is resized:

    ```
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

6.  Restart the instance in the ECS console.

    **Note:** The resize operation does not take effect until you restart the instance by using the console or by calling the RebootInstance operation. For more information, see [Restart an instance](/intl.en-US/Instance/Manage instance status/Restart an instance.md) and [RebootInstance](/intl.en-US/API Reference/Instances/RebootInstance.md).

7.  Connect to the instance.

8.  Resize the file system.

    Run the `df -h` command to check the type of the file system. Then, use one of the following methods to resize the file system based on the type of the file system:

    -   If the type of the file system is ext such as ext3 and ext4, run the following command to resize the file system:

        ```
        resize2fs <PartitionName\>
        ```

        In the following example command output, the file system of the /dev/vda1 partition is resized.

        ```
        [root@ecshost ~]# resize2fs /dev/vda1
        resize2fs 1.41.12 (17-May-2010)
        Filesystem at /dev/vda1 is mounted on /; on-line resizing required
        old desc_blocks = 2, new_desc_blocks = 7
        Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
        The filesystem on /dev/vda1 is now 26213807 blocks long.
        ```

    -   If the type of the file system is XFS, run the following command to resize the file system:

        ```
        xfs_growfs <mountpoint\>
        ```

        In the following example command output, the file system of the /dev/vda1 partition is resized. The mount point of the /dev/vda1 partition is the / root directory.

        ```
        [root@ecshost ~]# xfs_growfs /
        ```

        **Note:** The commands may vary based on versions of the xfs\_growfs tool. Run `xfs_growfs --help` to check the corresponding commands.

9.  Run the following command to check the size of the disk partition:

    ```
    df -h
    ```

    In the following example command output, the size of the /dev/vda1 partition is 100 GiB. This indicates that the partition is resized.

    ```
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.1G   93G   2% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```


**Related topics**  


[Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md)

[Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md)

[Resize partitions and file systems of Linux data disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux data disks.md)

