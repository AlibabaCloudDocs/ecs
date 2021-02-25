# Create RAID arrays for Linux

This topic uses an ECS instance running the Ubuntu operating system to show how to use the msadm command of the Linux operating system to create a 100-GiB RAID array for multiple data disks.

You have created multiple cloud disks and attached them to the ECS instance. We recommend that you create cloud disks of the same capacity and type. For more information about the procedure to create pay-as-you-go cloud disks, see [Create a disk](/intl.en-US/Block Storage/Cloud disks/Create a cloud disk/Create a disk.md) and [Attach a data disk](/intl.en-US/Block Storage/Cloud disks/Attach a data disk.md). For more information about the procedure to create subscription cloud disks, see [Create a subscription disk]().

Independent Array of Independent Disks \(RAID\) combines multiple cloud disks into a disk array group. Compared with a cloud disk, a RAID array offers higher capacity, read/write bandwidth, reliability, and availability.

We recommend that you use RAID 0 or RAID 1 mode and partition cloud disks in the same size to improve usage of disk space. We recommend that you do not use RAID 5 or RAID 6 mode, because parity check data in RAID5 or RAID6 mode consumes the IOPS of cloud disks and causes performance deterioration.

The following table lists the advantages, disadvantages and application scenarios of RAID 0 and RAID 1 modes.

|Mode|Advantage|Disadvantage|Scenario|
|----|---------|------------|--------|
|RAID 0|Uses striping technology to allocate I/O loads to different cloud disks. High disk space increases throughput directly. The capacity and bandwidth in the array are the sum of the capacity and bandwidth of different disks.|A damaged disk may cause loss of all data because no data redundancy is available.|Has high requirements for I/O performance and is applicable when data is backed up in other methods or no data backup is needed.|
|RAID 1|Provides higher data redundancy because data is stored in different cloud disks in mirroring mode. The lowest capacity and bandwidth of cloud disks are the capacity and bandwidth of the RAID array.|The write performance is poor because data must be written to multiple cloud disks at the same time.|Focuses more on fault tolerance than I/O performance in key applications.|

## Procedure

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the lsblk command to view information of all cloud disks on the ECS instance.

    ```
    root@lvs06:~# lsblk
    ```

3.  Run the mdadm command to create the /dev/md0 RAID array.

    -   Run the following command to create RAID 0 mode:

        ```
        root@raid06:~# mdadm --create /dev/md0 --level=0 --raid-devices=5 /dev/vd\[bcdef\]
        ices=5 /dev/vd[bcdef]
        mdadm: Defaulting to version 1.2 metadata
        mdadm: array /dev/md0 started
        ```

        `--level=0` indicates RAID 0 mode and /dev/vd\[bcdef\] indicates that the RAID array consists of the /dev/vdb, /dev/vdc, /dev/vdd, /dev/vde, and/dev/vdf cloud disks.

    -   Run the following command to create RAID 1 mode:

        ```
        root@raid06:~# mdadm --create /dev/md0 --level=1 --raid-devices=5 /dev/vd\[bcdef\]
        ```

        `--level=1` indicates RAID 1 mode.

4.  Run the mdadm command to view information of the newly created /dev/md0 RAID array.

    ```
    root@raid06:~# mdadm --detail /dev/md0
    /dev/md0:
            Version : 1.2
      Creation Time : Sun May 1912:31:532019
         Raid Level : raid0
         Array Size : 104775680 (99.92 GiB 107.29 GB)
       Raid Devices : 5
      Total Devices : 5
        Persistence : Superblock is persistent
    
        Update Time: Sun May 1912: 31: 532019
              State : clean
     Active Devices : 5
    Working Devices : 5
     Failed Devices : 0
      Spare Devices : 0
    
         Chunk Size : 512K
    
               Name : raid06:0  (local to host raid06)
               UUID : 59b65ca6:ad8ffc30:ee439c6b:db6ba***
             Events : 0Number   Major   Minor   RaidDevice State
           0253160      active sync   /dev/vdb
           1253321      active sync   /dev/vdc
           2253482      active sync   /dev/vdd
           3253643      active sync   /dev/vde
           4253804      active sync   /dev/vdf                        
    ```

5.  Run the mkfs command to create a file system such as ext4 on the RAID array.

    You can also create a file system of other types.

    ```
    root@raid06:~# mkfs.ext4 /dev/md0
    mke2fs 1.42.13 (17-May-2015)
    Creating filesystem with261939204k blocks and 6553600 inodes
    Filesystem UUID: 4fc55c24-d780-40d5-a077-03b484519***
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872
    
    Allocating group tables: done
    Writing inode tables: done
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done                        
    ```

6.  Run the following command using root permissions to create a profile containing RAID information and configure the RAID array to be automatically reassembled when the ECS instance starts.

    ```
    root@raid06:~# sudo mdadm --detail --scan \| sudo tee -a /etc/mdadm/mdadm.conf
    ```

7.  \(Optional\) Create a mount point such as /media/raid0.

    You can also attach the cloud disk to an existing directory.

    ```
    root@raid06:~# mkdir /media/raid0
    ```

8.  Run the mount command to attach a file system. For example, you can attach the /dev/md0 file system to the /media/raid0 directory.

    ```
    root@raid06:~# mount /dev/md0 /media/raid0
    ```

9.  Run the df command to view the mount point information of the RAID array.

    In the returned information, the file system must be attached to the specified mount point.

    ```
    root@raid06:~# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    udev            7.9G     07.9G   0% /dev
    tmpfs           1.6G  3.5M  1.6G   1% /run
    /dev/vda1        40G   23G   15G  61% /
    tmpfs           7.9G     0  7.9G   0% /dev/shm
    tmpfs           5.0M  4.0K  5.0M   1% /run/lock
    tmpfs           7.9G     07.9G   0% /sys/fs/cgroup
    tmpfs           1.6G     01.6G   0% /run/user/0
    /dev/md0         99G   60M   94G   1% /media/raid0
    ```


To configure the RAID array to be automatically loaded each time the ECS instance starts, add the following information to the /etc/fstab profile.

1.  Add auto-start settings to the/etc/fstab profile.

    ```
    root@raid06:~# echo /dev/md0 /media/rad0 defaults,nofail,nobootwait 0 2 \>\> /etc/fstab
    ```

    **Note:** To configure the ECS instance to start when the RAID array is not attached, add nofail settings. Even if an error occurs when you stall a cloud disk, nofail settings allow the ECS instance to start. If you are using the Ubuntu operating system, you also can add nobootwait settings.

2.  Run the mount command to attach all file systems to the /etc/fstab profile:

    ```
    root@raid06:~# mount -a
    ```


