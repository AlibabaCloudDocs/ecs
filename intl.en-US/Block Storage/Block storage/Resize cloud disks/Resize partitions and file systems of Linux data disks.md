# Resize partitions and file systems of Linux data disks {#concept_z11_xsh_ydb .concept}

When you resize cloud disks, only the storage capacity is extended. File systems are not affected. You must follow the steps in this topic to resize file systems to extend the capacity for ECS instances.

## Preparations {#section_vjz_tg3_vlw .section}

Before you resize the partition and file system of a data disk, you must complete the following operations.

1.  [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) for data backup, to prevent data loss caused by misoperations.
2.  Use the ECS console or API to [Resize cloud disks offline](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize cloud disks offline.md#).
3.  Connect to the ECS instance remotely. For more information about connection methods, see [Methods to connect to an ECS instance](../../../../reseller.en-US/Instances/Connect to instances/Overview.md#).

## Check the partition format and the file system type {#section_jdz_a9a_my1 .section}

In the following example, the data disk is an ultra disk, the ECS instance operating system is CentOS 7.5 64-bit, and the data disk name is /dev/vdb.

1.  Run the `fdisk -lu <DeviceName\>` command to check whether the disk is partitioned.

    In the example, the disk has partition /dev/vdb1. `" System"="Linux"` indicates that the partition scheme of the disk is MBR. If `"System"="GPT"` is displayed, it indicates that the partition scheme of the disk is GPT.

    ``` {#codeblock_rt0_ob6_ww6}
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

2.  Run the `blkid <PartionName\>` command to check the file system type.

    In the example, the file system of /dev/vdb1 is ext4.

    ``` {#codeblock_mxg_qw8_ocw}
    [root@ecshost ~]# blkid /dev/vdb1
    /dev/vdb1: UUID="e97bf1e2-fc84-4c11-9652-73********24" TYPE="ext4"
    ```

    **Note:** No results are returned if a data disk does not have partitions or file systems, or if a data disk has partitions, but not file systems.

3.  Run the following command to check the status of the file system.

    -   For the ext\* file system: `e2fsck -n <dst\_dev\_part\_path\>`
    -   For the xfs file system: `xfs_repair -n <dst\_dev\_part\_path\>`
    In the example, the file system is in the clean state. If the file system is not in the clean state, troubleshoot the file system.

    ``` {#codeblock_i6g_2gi_2bs}
    [root@ecshost ~]# e2fsck -n /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Warning! /dev/vdb1 is mounted.
    Warning: skipping journal recovery because doing a read-only filesystem check.
    /dev/vdb1: clean, 11/1310720 files, 126322/5242624 blocks
    ```


## Select a method to resize partitions or file systems {#section_2ua_pt6_4qe .section}

Select proper operations based on the partition format and file system conditions.

|Scenario|Operation|
|--------|---------|
|A data disk has partitions and file systems.| -   To resize the existing MBR partitions of the data disk, see [Option 1: Resize existing MBR partitions](#).
-   If the new disk space is used to add new MBR partitions, see [Option 2: Add and format MBR partitions](#).
-   To resize the existing GPT partitions of the data disk, see [Option 3: Resize existing GPT partitions](#).
-   If the new disk space is used to add new GPT partitions, see [Option 4: Add and format GPT partitions](#).

 |
|A new data disk does not have partitions or file systems.|[Partition and format a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#) or [Partition and format data disk more than 2 TiB](reseller.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#) after you resize the disk space in the console.|
|A data disk has file systems, but not partitions.|[Resize a file system](#) after you resize the disk space in the console.|
|A data disk is not attached to any instance.|After you attach the data disk to an instance, perform the steps in this topic to resize the data disk.|

**Note:** If an existing partition of a data disk is created by using MBR, you cannot resize the data disk to greater than or equal to 2 TiB. To prevent data loss, we recommend that you create a cloud disk larger than 2 TiB. Format a GPT partition as specified in [Partition and format data disk more than 2 TiB](reseller.en-US/Block Storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#) and copy the data in the MBR partition to the GPT partition.

## Option 1: Resize existing MBR partitions {#section_vvb_gcs_bhm .section}

**Note:** To prevent data loss, we do not recommend that you resize partitions and file systems when they are attached to ECS instances. Detach the attached partitions \(unmount\) first. After you resize the partitions and they can be normally used, attach the partitions \(mount\) again. The following operation methods are recommended for different Linux kernel versions:

-   If the instance kernel version is earlier than 3.6, detach the partition, modify the partition table, and then resize the file system.
-   If the instance kernel version is 3.6 or later, modify the partition table, notify the kernel of updating the partition table, and then resize the file system.

To resize an existing MBR partition, perform the following steps:

Step 1: Modify the partition table

1.  Run the `fdisk -lu /dev/vdb` command and record the start and end sectors of the existing partition.

    In this example, the start sector of /dev/vdb1 is 2,048 and the end sector is 41,943,039.

    ``` {#codeblock_y7s_lg2_9mv}
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

2.  View the mount path of the data disk. Detach the partition based on the returned file path and wait until the partition is fully detached.

    ``` {#codeblock_b9z_gmj_5um}
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb1
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

3.  Run the fdisk command to delete the existing partition.

    1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
    2.  Enter p to display the partition table.
    3.  Enter d to delete the partition.
    4.  Enter p to confirm that the partition has been deleted.
    5.  Enter w to save changes and exit.
    ``` {#codeblock_28y_5ck_z16}
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
    WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
    The kernel still uses the old table. The new table will be used at
    the next reboot or after you run partprobe(8) or kpartx(8)
    Syncing disks.
    ```

4.  Run the fdisk command to create a partition.

    1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
    2.  Enter p to display the partition table.
    3.  Enter n to create a partition.
    4.  Enter p to set the partition as the primary partition.
    5.  Enter <partition number\> to select a partition number. 1 is selected in the example.

        **Warning:** The start sector of the new partition must be equal to that of the existing partition. The end sector must be greater than that of the existing partition. Otherwise, the resize operation may fail.

    6.  Enter w to save changes and exit.
    In the example, /dev/vdb1 is extended from 20 GiB to 40 GiB.

    ``` {#codeblock_a4w_96v_3of}
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
    Partition 1 of type Linux and of size 30 GiB is set
    Command (m for help): p
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 62916607 31457280 83 Linux
    Command (m for help): w
    The partition table has been altered!
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

5.  Run the `lsblk /dev/vdb` command to confirm that the partition table has been added.
6.  Run the `e2fsck -n /dev/vdb1` command to confirm that the file system after the resize operation is in the clean state.

Step 2: Notify the kernel of updating the partition table

Run the `partprobe <dst_dev_path>` or `partx -u <dst_dev_path>` command to notify kernel that the partition table has been modified and needs to be synchronized.

Step 3: Resize the file system

-   For the ext\* file system \(such as ext3 and ext4\): Run the `resize2fs /dev/vdb1` command.

    ``` {#codeblock_e7j_9x0_xf4}
    [root@ecshost ~]# resize2fs /dev/vdb1
    resize2fs 1.42.9 (28-Dec-2013)
    Resizing the filesystem on /dev/vdb1 to 7864320 (4k) blocks.
    The filesystem on /dev/vdb1 is now 7864320 blocks long.
    ```

-   For the xfs file system: run the `mount /dev/vdb1 /mnt/` command first, and then the `xfs_growfs /dev/vdb1` command.

    ``` {#codeblock_5e0_g7h_otl}
    [root@ecshost ~]# mount /dev/vdb1 /mnt/
    [root@ecshost ~]# xfs\_growfs /dev/vdb1
    meta-data=/dev/vdb1              isize=512    agcount=4, agsize=1310720 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=1        finobt=0 spinodes=0
    data     =                       bsize=4096   blocks=5242880, imaxpct=25
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
    log      =internal               bsize=4096   blocks=2560, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    data blocks changed from 5242880 to 7864320
    ```


## Option 2: Add and format MBR partitions {#section_gg7_ilv_h3j .section}

If the new disk space is used to add a new MBR partition, perform the following steps:

1.  Run the `fdisk -u /dev/vdb` command to create a partition.

    In the example, partition /dev/vdb2 is created for the newly added 20 GiB disk space.

    ``` {#codeblock_or8_07t_e4r}
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

2.  Run the `lsblk /dev/vdb` command to view the partition.

    ``` {#codeblock_3u7_ycf_95m}
    [root@ecshost ~]# lsblk /dev/vdb
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vdb    253:16   0  40G  0 disk
    ├─vdb1 253:17   0  20G  0 part
    └─vdb2 253:18   0  20G  0 part
    ```

3.  Format the new partition.
    -   To create an ext4 file system, run the `mkfs.ext4 /dev/vdb2` command.

        ``` {#codeblock_bzg_w8d_3pe}
        [root@ecshost ~]# mkfs.ext4 /dev/vdb2
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        1310720 inodes, 5242880 blocks
        262144 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=2153775104
        160 block groups
        32768 blocks per group, 32768 fragments per group
        8192 inodes per group
        Superblock backups stored on blocks:
                32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
                4096000
        
        Allocating group tables: done
        Writing inode tables: done
        Creating journal (32768 blocks): done
        Writing superblocks and filesystem accounting information: done
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="e3f336dc-d534-4fdd-****-b6ff1a55bdbb" TYPE="ext4"
        ```

    -   To create an ext3 file system, run the `mkfs.ext3 /dev/vdb2` command.

        ``` {#codeblock_r80_vxx_d62}
        [root@ecshost ~]# mkfs.ext3 /dev/vdb2
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        1310720 inodes, 5242880 blocks
        262144 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=4294967296
        160 block groups
        32768 blocks per group, 32768 fragments per group
        8192 inodes per group
        Superblock backups stored on blocks:
                32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
                4096000
        
        Allocating group tables: done
        Writing inode tables: done
        Creating journal (32768 blocks): done
        Writing superblocks and filesystem accounting information: done
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="dd5be97d-a630-4593-****-5056def914ea" SEC_TYPE="ext2" TYPE="ext3"
        ```

    -   To create an xfs file system, run the `mkfs.xfs -f /dev/vdb2` command.

        ``` {#codeblock_tzg_2uj_usi}
        [root@ecshost ~]# mkfs.xfs -f /dev/vdb2
        meta-data=/dev/vdb2              isize=512    agcount=4, agsize=1310720 blks
                 =                       sectsz=512   attr=2, projid32bit=1
                 =                       crc=1        finobt=0, sparse=0
        data     =                       bsize=4096   blocks=5242880, imaxpct=25
                 =                       sunit=0      swidth=0 blks
        naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
        log      =internal log           bsize=4096   blocks=2560, version=2
                 =                       sectsz=512   sunit=0 blks, lazy-count=1
        realtime =none                   extsz=4096   blocks=0, rtextents=0
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="66251477-3ae4-4b44-****-5604420dbecb" TYPE="xfs"
        ```

    -   To create a btrfs file system, run the `mkfs.btrfs /dev/vdb2` command.

        ``` {#codeblock_zje_bhf_paj}
        [root@ecshost ~]# mkfs.btrfs /dev/vdb2
        btrfs-progs v4.9.1
        See http://btrfs.wiki.kernel.org for more information.
        
        Label:              (null)
        UUID:               6fb5779b-57d7-4aaf-bf09-82b46f54a429
        Node size:          16384
        Sector size:        4096
        Filesystem size:    20.00GiB
        Block group profiles:
          Data:             single            8.00MiB
          Metadata:         DUP               1.00GiB
          System:           DUP               8.00MiB
        SSD detected:       no
        Incompat features:  extref, skinny-metadata
        Number of devices:  1
        Devices:
           ID        SIZE  PATH
            1    20.00GiB  /dev/vdb2
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="6fb5779b-57d7-4aaf-****-82b46f54a429" UUID_SUB="9bdd889a-ab69-4653-****-d1b6b8723378" TYPE="btrfs"
        ```

4.  Run the `mount /dev/vdb2 /mnt` command to attach the file system to the data disk.
5.  Run the `df -h` command to check the current capacity and usage of the data disk.

    If information about the new file system is displayed, it indicates that the attach operation is successful.

    ``` {#codeblock_zb6_5zt_gtk}
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


## Option 3: Resize existing GPT partitions {#section_oi9_qp8_f04 .section}

To resize an existing GPT partition, perform the following steps: In the example, a data disk of 1 TiB is used and then extended to 32 TiB. The existing partition is /dev/vdb1.

1.  Run the fdisk command to view information about the partition to be extended.

    ``` {#codeblock_7se_li5_o6n}
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
     1         2048   2147483647   1024G  Microsoft basic mnt                    
    ```

2.  View the mount path of the data disk. Detach the partition based on the returned file path and wait until the partition is fully detached.

    ``` {#codeblock_tl5_yci_a49}
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb1
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

3.  Use the parted tool to allocate space for the partition.
    1.  Run the `parted /dev/vdb` command to start the parted tool.
    2.  \(Optional\) Run the `help` command to view the help information.
    3.  Run the `print` command to view the number \(Number\) and capacity \(Size\) of the partition to be extended.

        In the example, partition 1 is to be extended and its existing capacity is 1100 GiB. The new capacity will be allocated to partition 1.

    4.  Run the `resizepart <partition number> <capacity allocation percentage>` command to resize the partition.

        `resizepart 1 100%` is used in the example.

    5.  Run the `print` command to check whether the number \(Number\) and capacity \(Size\) of the partition has been changed.

        ``` {#codeblock_hw4_cmz_08o}
        [root@ecshost ~]# parted /dev/vdb
        GNU Parted 3.1
        Using /dev/vdb
        Welcome to GNU Parted! Type 'help' to view a list of commands.
        
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  1100GB  1100GB  ext4         mnt
        (parted) resizepart 1 100%
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  35.2TB  35.2TB  ext4         mnt                    
        ```

    6.  Run the `quit` command to exit the parted tool.
4.  Run the `fsck -f /dev/vdb1` command to check whether the file system is consistent.

    ``` {#codeblock_r7a_3jb_gkh}
    [root@ecshost ~]# fsck -f /dev/vdb1
    fsck from util-linux 2.23.2
    e2fsck 1.42.9 (28-Dec-2013)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/vdb1: 11/67108864 files (0.0% non-contiguous), 4265369/268435200 blocks
    ```

5.  Resize the file system.
    -   For the ext\* file system \(such as ext3 and ext4\): run the `resize2fs /dev/vdb1` command, and attach the partition again.

        ``` {#codeblock_vgo_hmt_rmq}
        [root@ecshost ~]# resize2fs /dev/vdb1
        resize2fs 1.42.9 (28-Dec-2013)
        Resizing the filesystem on /dev/vdb1 to 8589934331 (4k) blocks.
        The filesystem on /dev/vdb1 is now 8589934331 blocks long.
        [root@ecshost ~]# mount /dev/vdb1 /mnt/
        ```

    -   For the xfs file system: run the `mount /dev/vdb1 /mnt/` command first, and then the `xfs_growfs /dev/vdb1` command.

        ``` {#codeblock_rhq_ahw_m6f}
        [root@ecshost ~]# mount /dev/vdb1 /mnt/
        [root@ecshost ~]# xfs\_growfs /dev/vdb1
        ```


## Option 4: Add and format GPT partitions {#section_4hl_5l7_87s .section}

If the newly added disk space is used to add a new GPT partition, perform the following steps: In the example, a data disk of 32 TiB is used. The existing partition /dev/vdb1 has a 4.8 TiB capacity. The /dev/vdb2 partition is to be created.

1.  Run the fdisk command to view information about the existing partition.

    ``` {#codeblock_nrd_kr0_4x1}
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

2.  Use the parted tool to create a new partition and allocate space for it.
    1.  Run the `parted /dev/vdb` command to start the parted tool.
    2.  Run the `print free` command to view the disk space to be allocated. Record the start and end sectors and capacity of the existing partition.

        In the example, the start sector of /dev/vdb1 is 1,049 KB, the end sector is 5,278 GB, and the capacity is 5,278 GiB.

        ``` {#codeblock_k7q_ebl_6pw}
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

    3.  Run the `mkpart <partition name> <start sector> <capacity allocation percentage>` command.

        In the example, the /dev/vdb2 partition named test is created. The start sector of the new partition is the end sector of the existing partition. The new capacity is allocated to the new partition.

    4.  Run the `print` command to check whether the capacity \(Size\) of the partition changes.

        ``` {#codeblock_g8z_sg6_22e}
        (parted) mkpart test 5278GB 100%
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

    5.  Run the `quit` command to exit the parted tool.
3.  Create a file system for the new partition.

    -   To create an ext4 file system, run the `mkfs.ext4 /dev/vdb2` command.
    -   To create an ext3 file system, run the `mkfs.ext3 /dev/vdb2` command.
    -   To create an xfs file system, run the `mkfs.xfs -f /dev/vdb2` command.
    -   To create a btrfs file system, run the `mkfs.btrfs /dev/vdb2` command.
    In the example, an xfs file system is created.

    ``` {#codeblock_sb7_qm1_env}
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

4.  Run the `fdisk -l` command to view partition capacity changes.

    ``` {#codeblock_bve_5oy_ggu}
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

5.  Run the blkid command to view the file system types.

    ``` {#codeblock_yc6_imy_avh}
    [root@ecshost ~]# blkid
    /dev/vda1: UUID="ed95c595-4813-480e-****-85b1347842e8" TYPE="ext4"
    /dev/vdb1: UUID="21e91bbc-7bca-4c08-****-88d5b3a2303d" TYPE="ext4" PARTLABEL="mnt" PARTUUID="576235e0-5e04-4b76-****-741cbc7e98cb"
    /dev/vdb2: UUID="a7dcde59-8f0f-4193-****-362a27192fb1" TYPE="xfs" PARTLABEL="test" PARTUUID="464a9fa9-3933-4365-****-c42de62d2864"  
    ```

6.  Attach the new partition.

    ``` {#codeblock_8if_42j_r60}
    [root@ecshost ~]# mount /dev/vdb2 /mnt
    ```


## Related operations {#section_nop_fuk_f6y .section}

-   [Extend the file system of the Linux system disk](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend the file system of the Linux system disk.md#)
-   [Extend a Windows file system](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend a Windows file system.md#)

