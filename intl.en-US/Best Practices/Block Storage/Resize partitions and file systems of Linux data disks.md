---
keyword: [Alibaba Cloud, ECS, disk resizing, extend disk capacity, Elastic Bock Storage]
---

# Resize partitions and file systems of Linux data disks

When you resize disks, only the storage capacity of the disks is extended. File systems of the ECS instances are not affected. Perform the operations in this topic to resize file systems to extend the capacity of ECS instances.

1.  A snapshot is created to back up data.

    To prevent data loss caused by incorrect operations, we recommend that you create a snapshot to back up your data. For more information, see [Create a snapshot for a disk](/intl.en-US/Snapshots/Use snapshots/Create a normal snapshot.md).

2.  A data disk is resized in the console.

    If no data disks are resized, see [Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md) or [Resize disks offline for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks offline for Linux instances.md) to resize a data disk.

3.  Remotely connect to an ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

The following configurations are used in the examples of this topic:

-   Operating system of the ECS instance: Alibaba Cloud Linux 2.1903 LTS 64-bit public image
-   Data disk: ultra disk
-   Device name of the data disk: /dev/vdb

Adjust the commands or parameter settings based on the actual operating system and device name of the data disk.

## Check the partition table format and the file system type

1.  Run the following command to check the partition table format of the data disk:

    ```
    fdisk -lu /dev/vdb
    ```

    In this example, the disk has a partition named /dev/vdb1.

    -   If the value of `System` is `Linux`, the data disk uses the MBR partition table format.
    -   If the value of `System` is `GPT`, the data disk uses the GPT partition table format.
    ```
    [root@ecshost ~]# fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

2.  Run the following command to check the file system type of the existing partition:

    ```
    blkid /dev/vdb1
    ```

    In this example, the file system type of /dev/vdb1 is ext4.

    ```
    [root@ecshost ~]# blkid /dev/vdb1
    /dev/vdb1: UUID="e97bf1e2-fc84-4c11-9652-73********24" TYPE="ext4"
    ```

    **Note:** No results are returned if a data disk does not have partitions or file systems, or if a data disk has partitions but no file systems.

3.  Run the following command to check the status of the file system:

    -   ext\* file system:

        ```
        e2fsck -n /dev/vdb1
        ```

    -   XFS file system:

        ```
        xfs_repair -n /dev/vdb1
        ```

    **Note:** In this example, the file system is in the clean state, which indicates that the file system is normal. If the file system is not in the clean state, troubleshoot the file system.

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# e2fsck -n /dev/vdb1
    Warning! /dev/vdb1 is mounted.
    Warning: skipping journal recovery because doing a read-only filesystem check.
    /dev/vdb1: clean, 11/1310720 files, 126322/5242624 blocks
    ```


## Choose a method to resize partitions or file systems

Choose a resizing method based on the partition format and file system type.

|Scenario|Resizing method|
|--------|---------------|
|The data disk has partitions and file systems.|-   To resize the existing MBR partitions of the data disk, see [\#section\_vvb\_gcs\_bhm](#section_vvb_gcs_bhm).
-   To resize the disk to create more MBR partitions, see [\#section\_gg7\_ilv\_h3j](#section_gg7_ilv_h3j).
-   To resize the existing GPT partitions of the data disk, see [\#section\_oi9\_qp8\_f04](#section_oi9_qp8_f04).
-   To resize the disk to create more GPT partitions, see [\#section\_4hl\_5l7\_87s](#section_4hl_5l7_87s). |
|The new data disk does not have partitions or file systems.|After you resize the data disk in the console, see [Format a data disk for a Linux instance](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Format a data disk for a Linux instance.md) or [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md).|
|The raw data disk has a file system but no partitions.|After you resize the data disk in the console, see [Option 5: Resize the file system of a raw data disk](#section_f88_ax7_y8i).|
|The data disk is not attached to instances.|After you attach the data disk to an instance, perform the following operations in this topic to resize the data disk.|

**Note:**

-   If a data disk contains an MBR partition, the data disk cannot be resized to 2 TiB or larger. To prevent data loss, we recommend that you create a disk larger than 2 TiB, format a GPT partition, and then copy the data in the MBR partition to the GPT partition. For more information, see [Partition and format a data disk larger than 2 TiB in size](/intl.en-US/Block Storage/Cloud disks/Format a data disk/Partition and format a data disk larger than 2 TiB in size.md).
-   If data disks fail to be resized due to a problem of the resizing or formatting tool, you can upgrade the tool version or re-install the tool.

## Option 1: Resize existing MBR partitions

**Note:** To prevent data loss, we recommend that you do not resize partitions and file systems that are mounted to ECS instances. Unmount the mounted partitions \(umount\) first. After the partitions are resized and can be used properly, mount the partitions \(mount\) again. We recommend that you use the following methods for different Linux kernel versions:

-   If the instance kernel version is earlier than 3.6, unmount the partition, modify the partition table, and then resize the file system.
-   If the instance kernel version is 3.6 or later, modify the corresponding partition table, notify the kernel to update the partition table, and then resize the file system.

Perform the following operations to resize an existing MBR partition:

1.  Modify the partition table.

    1.  Run the following command to view the partition information, and record the start and end sectors of the existing partition:

        ```
        fdisk -lu /dev/vdb
        ```

        In this example, the start sector number of the /dev/vdb1 partition is 2048, and the end sector number is 41943039.

        ```
        [root@ecshost ~]# fdisk -lu /dev/vdbDisk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x9277b47b
        
        Device Boot Start End Blocks Id System
        /dev/vdb1 2048 41943039 20970496 83 Linux
        ```

    2.  View the mount path of the data disk. Unmount the partition based on the returned file path and wait until the partition is unmounted.

        View the mount information.

        ```
        mount | grep "/dev/vdb"
        ```

        Cancel the mounting of the data disk.

        ```
        umount /dev/vdb1
        ```

        View the operation result.

        ```
        mount | grep "/dev/vdb"
        ```

        A command output similar to the following one is displayed:

        ```
        [root@ecshost ~]# mount | grep "/dev/vdb"
        /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
        [root@ecshost ~]# umount /dev/vdb1
        [root@ecshost ~]# mount | grep "/dev/vdb"
        ```

    3.  Run the fdisk command to delete the existing partition.

        **Warning:** If errors occur when you delete a partition, data stored on the partition may be deleted. To avoid data loss, back up important data such as user data in a database before you delete a partition.

        1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
        2.  Enter p to show the partition table.
        3.  Enter d to delete the partition.
        4.  Enter p to confirm whether the partition is deleted.
        5.  Enter w to save changes and exit.
        The following sample code shows that the partition is deleted:

        ```
        [root@ecshost ~]# fdisk -u /dev/vdbWelcome to fdisk (util-linux 2.23.2).
        Changes will remain in memory only, until you decide to write them.
        Be careful before using the write command.
        Command (m for help): p
        Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x9277b47b
        Device Boot Start End Blocks Id System
        /dev/vdb1 2048 41943039 20970496 83 Linux
        Command (m for help): d
        Selected partition 1
        Partition 1 is deleted
        Command (m for help): p
        Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x9277b47b
        Device Boot Start End Blocks Id System
        Command (m for help): w
        The partition table has been altered!
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

    4.  Run the fdisk command to create a partition.

        1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
        2.  Enter p to show the partition table.
        3.  Enter n to create a partition.
        4.  Enter p to select the primary partition type.
        5.  Enter <partition number\> to select the partition number. In this example, 1 is selected.
        6.  Set the start and end sector numbers for the new partition.

            **Warning:** The start sector number of the new partition must be the same as that of the existing partition. The end sector number must be greater than that of the existing partition. Otherwise, the resizing operation fails.

        7.  Enter w to save changes and exit.
        The following sample code shows that the partition is resized. In this example, the /dev/vdb1 partition is resized from 20 GiB to 40 GiB.

        ```
        [root@ecshost ~]# fdisk -u /dev/vdb
        Welcome to fdisk (util-linux 2.23.2).
        Changes will remain in memory only, until you decide to write them.
        Be careful before using the write command.
        Command (m for help): p
        Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x9277b47b
        Device Boot Start End Blocks Id System
        Command (m for help): n
        Partition type:
        p primary (0 primary, 0 extended, 4 free)
        e extended
        Select (default p): p
        Partition number (1-4, default 1): 1
        First sector (2048-83886079, default 2048):
        Using default value 2048
        Last sector, +sectors or +size{K,M,G} (2048-83886079, default 83886079):
        Partition 1 of type Linux and of size 40 GiB is set
        Command (m for help): w
        The partition table has been altered!
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

    5.  Run one of the following commands to notify the kernel to update the partition table:

        ```
        partprobe /dev/vdb
        ```

        ```
        partx -u /dev/vdb1
        ```

    6.  Run the following command to verify that the partition table is added:

        ```
        lsblk /dev/vdb
        ```

    7.  Run the following command to check the file system again and verify whether the file system is in the clean state after the partition is resized:

        ```
        e2fsck -f /dev/vdb1
        ```

        **Note:** If the file system is not in the clean state after you run the preceding command, you can run the `e2fsck -n /dev/vdb1` command to check the file system again.

2.  Resize the file system.

    -   For an ext\* file system such as ext3 or ext4, run the following commands in sequence to resize the ext\* file system and remount the partition:

        Resize the ext\* file system.

        ```
        resize2fs /dev/vdb1
        ```

        Mount the partition to /mnt.

        ```
        mount /dev/vdb1 /mnt
        ```

    -   For an XFS file system, run the following commands in sequence to remount the partition and then resize the XFS file system:

        Mount the partition to /mnt.

        ```
        mount /dev/vdb1 /mnt
        ```

        Resize the XFS file system.

        ```
        xfs_growfs /mnt
        ```

        **Note:** The new version xfs\_growfs identifies the device to be resized based on the mount point. Example: `xfs_growfs /mnt`. You can run the `xfs_growfs --help` command to check how to use xfs\_growfs of different versions.


## Option 2: Add and format MBR partitions

If you want to resize the disk to create more MBR partitions, perform the following operations to resize the file system of the instance:

1.  Run the following command to create a partition:

    ```
    fdisk -u /dev/vdb
    ```

    The following sample code shows that a partition is created. In this example, the /dev/vdb2 partition is created for the newly added 20 GiB disk.

    ```
    [root@ecshost ~]# fdisk -u /dev/vdb
    Welcome to fdisk (util-linux 2.23.2).
    
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write commad.
    
    Command (m for help): p
    
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x2b31a2a3
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vdb1            2048    41943039    20970496   83  Linux
    
    Command (m for help): n
    Partition type:
       p   primary (1 primary, 0 extended, 3 free)
       e   extended
    Select (default p): p
    Partition number (2-4, default 2): 2
    First sector (41943040-83886079, default 41943040):
    Using default value 41943040
    Last sector, +sectors or +size{K,M,G} (41943040-83886079, default 83886079):
    Using default value 83886079
    Partition 2 of type Linux and of size 20 GiB is set
    
    Command (m for help): w
    The partition table has been altered!
    
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

2.  Run the following command to view the partition:

    ```
    lsblk /dev/vdb
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# lsblk /dev/vdb
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vdb    253:16   0  40G  0 disk
    ├─vdb1 253:17   0  20G  0 part
    └─vdb2 253:18   0  20G  0 part
    ```

3.  Create a file system:

    -   Run the following command to create an ext4 file system:

        ```
        mkfs.ext4 /dev/vdb2
        ```

    -   Run the following command to create an XFS file system:

        ```
        mkfs.xfs -f /dev/vdb2
        ```

    -   Run the following command to create a Btrfs file system:

        ```
        mkfs.btrfs /dev/vdb2
        ```

4.  Run the following command to view the information about the file system:

    ```
    blkid /dev/vdb2
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# blkid /dev/vdb2
    /dev/vdb2: UUID="e3f336dc-d534-4fdd-****-b6ff1a55bdbb" TYPE="ext4"
    ```

5.  Run the following command to mount the partition:

    ```
    mount /dev/vdb2 /mnt
    ```

6.  Run the following command to view the space and usage of the data disk:

    ```
    df -h
    ```

    If information about the new file system is displayed, the partition is mounted.

    ```
    [root@ecshost ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 3.9G 0 3.9G 0% /dev
    tmpfs 3.9G 0 3.9G 0% /dev/shm
    tmpfs 3.9G 460K 3.9G 1% /run
    tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
    /dev/vdb2 9.8G 37M 9.2G 1% /mnt
    tmpfs 783M 0 783M 0% /run/user/0
    ```


## Option 3: Resize existing GPT partitions

Perform the following operations to resize an existing GPT partition:

1.  View the mount path of the data disk. Unmount the partition based on the returned file path and wait until the partition is unmounted.

    View the mount information.

    ```
    mount | grep "/dev/vdb"
    ```

    Cancel the mounting of the data disk.

    ```
    umount /dev/vdb1
    ```

    View the operation result.

    ```
    mount | grep "/dev/vdb"
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb1
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

2.  Use the Parted tool to allocate capacity for the existing GPT partition.

    1.  Run the following command to start the Parted partition tool:

        ```
        parted /dev/vdb
        ```

        To view the Parted tool instructions, run the `help` command.

    2.  Run the following command to view the partition information, and record the partition number and start sector value of the existing partition:

        ```
        print
        ```

        If `Fix/Ignore/Cancel?` or `Fix/Ignore?` is displayed, enter Fix.

        In this example, the size of the existing partition is 1 TiB. The partition number \(the value of `Number`\) is `1`. The start sector number \(the value of `Start`\) is `1049kB`.

        ![resize-gpt-start](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1314488951/p70886.png)

    3.  Run the following command to delete the existing partition:

        ```
        rm <Partition number>
        ```

        In this example, the partition number of the existing partition is `1`. Therefore, the following command is used:

        ```
        rm 1
        ```

    4.  Run the following command to recreate the primary partition:

        ```
        mkpart primary <Start sector number of the existing partition> <Percentage of allocated capacity>
        ```

        In this example, the start sector number of the existing partition is `1049kB`, and the 3 TiB total capacity is allocated to the partition. Therefore, the following command is used:

        ```
        mkpart primary 1049kB 100%
        ```

    5.  Run the following command to check whether the new partition is created:

        ```
        print
        ```

        The following figure shows that the new GPT partition number is still 1, but the capacity of the partition is increased to 3 TiB.

        ![The GPT partitioning result](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1314488951/p71219.png)

    6.  Run the following command to exit the Parted tool:

        ```
        quit
        ```

    The following sample code shows the process.

    ```
    [root@ecshost ~]# parted /dev/vdb
    GNU Parted 3.1
    Using /dev/vdb
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Error: The backup GPT table is not at the end of the disk, as it should be.
    This might mean that another operating system believes the disk is smaller.
    Fix, by moving the backup to the end (and removing the old backup)?
    Fix/Ignore/Cancel? Fix
    Warning: Not all of the space available to /dev/vdb appears to be used, you can
    fix the GPT to use all of the space (an extra 4294967296 blocks) or continue
    with the current setting?
    Fix/Ignore? Fix
    Model: Virtio Block Device (virtblk)
    Disk /dev/vdb: 3299GB
    Sector size (logical/physical): 512B/512B
    Partition Table: gpt
    Disk Flags:
    
    Number  Start   End     Size    File system  Name     Flags
     1      1049kB  1100GB  1100GB  ext4         primary
    
    (parted) rm 1
    (parted) mkpart primary 1049kB 100%
    (parted) print
    Model: Virtio Block Device (virtblk)
    Disk /dev/vdb: 3299GB
    Sector size (logical/physical): 512B/512B
    Partition Table: gpt
    Disk Flags:
    
    Number  Start   End     Size    File system  Name     Flags
     1      1049kB  3299GB  3299GB  ext4         primary
    
    (parted) quit
    Information: You may need to update /etc/fstab.
    ```

3.  Run the following command to check the file system for consistency:

    ```
    fsck -f /dev/vdb1
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# fsck -f /dev/vdb1
    fsck from util-linux 2.23.2
    e2fsck 1.43.5 (04-Aug-2017)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/vdb1: 11/67108864 files (0.0% non-contiguous), 4265369/268434944 blocks
    ```

4.  Resize the file system corresponding to the partition and remount the partition.

    -   ext\* file system such as ext3 and ext4:

        Run the following command to resize the ext\* file system of the new partition:

        ```
        resize2fs /dev/vdb1
        ```

        Run the following command to remount the partition:

        ```
        mount /dev/vdb1 /mnt
        ```

    -   XFS file system:

        Run the following command to remount the partition:

        ```
        mount /dev/vdb1 /mnt
        ```

        Run the following command to resize the XFS file system:

        ```
        xfs_growfs /mnt
        ```

        **Note:** The new version xfs\_growfs identifies the device to be resized based on the mount point. Example: `xfs_growfs /mnt`. You can run the `xfs_growfs --help` command to check how to use xfs\_growfs of different versions.


## Option 4: Add and format GPT partitions

If you want to resize the disk to create more GPT partitions, perform the following operations to resize the file system of the instance: In this example, a 32 TiB data disk is used. The existing partition /dev/vdb1 has a 4.8 TiB capacity. The /dev/vdb2 partition is to be created.

1.  Run the following command to view the information of existing partitions in the data disk:

    ```
    fdisk -l
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000b1b45
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83875364    41936658+  83  Linux
    WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
    
    Disk /dev/vdb: 35184.4 GB, 35184372088832 bytes, 68719476736 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: gpt
    Disk identifier: BCE92401-F427-45CC-8B0D-B30EDF279C2F
    
    #         Start          End    Size  Type            Name
     1         2048  10307921919    4.8T  Microsoft basic mnt                    
    ```

2.  Use the Parted tool to create a partition and allocate capacity for it.

    1.  Run the following command to start the Parted tool:

        ```
        parted /dev/vdb
        ```

    2.  Run the following command to view the disk capacity to be allocated. Record the start and end sectors and capacity of the existing partition.

        ```
        print free
        ```

        In this example, the start sector number of /dev/vdb1 is 1,049 KB, the end sector number is 5,278 GB, and the capacity is 5,278 GiB.

        ```
        (parted) print free
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
                17.4kB  1049kB  1031kB  Free Space
         1      1049kB  5278GB  5278GB  ext4         mnt
                5278GB  35.2TB  29.9TB  Free Space                    
        ```

    3.  Run the following command to set the start and end sectors and capacity of the existing partition:

        ```
        mkpart <The partition name> <The start and end sector numbers> <The percentage of the allocated capacity>
        ```

        In this example, the /dev/vdb2 partition named test is created. The start sector number of the new partition is the end sector number of the existing partition. The new capacity is allocated to the new partition.

        ```
        mkpart test 5278GB 100%
        ```

    4.  Run the following command to check whether the capacity \(Size\) of the partition is changed:

        ```
        print
        ```

        A command output similar to the following one is displayed:

        ```
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  5278GB  5278GB  ext4         mnt
         2      5278GB  35.2TB  29.9TB               test                    
        ```

    5.  Run the following command to exit the Parted tool:

        ```
        quit
        ```

3.  Create a file system for the new partition.

    -   Run the following command to create an ext4 file system:

        ```
        mkfs.ext4 /dev/vdb2
        ```

    -   Run the following command to create an ext3 file system:

        ```
        mkfs.ext3 /dev/vdb2
        ```

    -   Run the following command to create an XFS file system:

        ```
        mkfs.xfs -f /dev/vdb2
        ```

    -   Run the following command to create a Btrfs file system:

        ```
        mkfs.btrfs /dev/vdb2
        ```

    In this example, an XFS file system is created.

    ```
    [root@ecshost ~]# mkfs -t xfs /dev/vdb2
    meta-data=/dev/vdb2              isize=512    agcount=28, agsize=268435455 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=1        finobt=0, sparse=0
    data     =                       bsize=4096   blocks=7301444096, imaxpct=5
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
    log      =internal log           bsize=4096   blocks=521728, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0               
    ```

4.  Run the following command to view changes of the partition capacity:

    ```
    fdisk -l
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000b1b45
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83875364    41936658+  83  Linux
    WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
    
    Disk /dev/vdb: 35184.4 GB, 35184372088832 bytes, 68719476736 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: gpt
    Disk identifier: BCE92401-F427-45CC-8B0D-B30EDF279C2F
    
    #         Start          End    Size  Type            Name
     1         2048  10307921919    4.8T  Microsoft basic mnt
     2  10307921920  68719474687   27.2T  Microsoft basic test  
    ```

5.  Run the following command to view the file system types:

    ```
    blkid
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# blkid
    /dev/vda1: UUID="ed95c595-4813-480e-****-85b1347842e8" TYPE="ext4"
    /dev/vdb1: UUID="21e91bbc-7bca-4c08-****-88d5b3a2303d" TYPE="ext4" PARTLABEL="mnt" PARTUUID="576235e0-5e04-4b76-****-741cbc7e98cb"
    /dev/vdb2: UUID="a7dcde59-8f0f-4193-****-362a27192fb1" TYPE="xfs" PARTLABEL="test" PARTUUID="464a9fa9-3933-4365-****-c42de62d2864"  
    ```

6.  Mount the new partition.

    ```
    mount /dev/vdb2 /mnt
    ```


## Option 5: Resize the file system of a raw data disk

If a raw data disk contains a file system but no partitions, perform the following operations to resize the file system:

1.  View the mount path of the data disk and unmount the partition based on the returned file path.

    View the mount information.

    ```
    mount | grep "/dev/vdb"
    ```

    Cancel the mounting of the data disk.

    ```
    umount /dev/vdb
    ```

    View the operation result.

    ```
    mount | grep "/dev/vdb"
    ```

    A command output similar to the following one is displayed:

    ```
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

2.  Run one of the following commands based on the file system type:

    -   For an ext\* file system, run the resize2fs command as the root user to resize the file system.

        ```
        resize2fs /dev/vdb
        ```

    -   For an XFS file system, run the xfs\_growfs command as the root user to resize the file system.

        ```
        xfs_growfs /mnt
        ```

        **Note:** The new version xfs\_growfs identifies the device to be resized based on the mount point. Example: `xfs_growfs /mnt`. You can run the `xfs_growfs --help` command to check how to use xfs\_growfs of different versions.

3.  Mount the disk to the mount point.

    ```
    mount /dev/vdb /mnt
    ```

4.  Run the `df -h` command to view the result of data disk resizing.

    ```
    df -h
    ```

    The following command output shows that the file system has a larger capacity, which indicates that the file system is resized.

    ```
    [root@ecshost ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 3.9G 0 3.9G 0% /dev
    tmpfs 3.9G 0 3.9G 0% /dev/shm
    tmpfs 3.9G 460K 3.9G 1% /run
    tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
    /dev/vdb 98G 37G 61G 37% /mnt
    tmpfs 783M 0 783M 0% /run/user/0
    ```


**Related topics**  


[Resize disks online for Linux instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Linux instances.md)

[Resize disks online for Windows instances](/intl.en-US/Block Storage/Resize cloud disks/Resize disks online for Windows instances.md)

[Resize partitions and file systems of Linux system disks](/intl.en-US/Best Practices/Block Storage/Resize partitions and file systems of Linux system disks.md)

