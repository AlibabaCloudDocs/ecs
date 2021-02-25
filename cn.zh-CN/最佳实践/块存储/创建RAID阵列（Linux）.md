# 创建RAID阵列（Linux）

本文以Ubuntu系统ECS实例为例，介绍了如何使用Linux系统内置的mdadm命令为多块数据盘创建一个100GiB的RAID阵列。

您已经创建并挂载了多块云盘。建议您创建具有相同容量和相同类型的云盘。创建按量付费云盘的详细步骤请参见[创建云盘](/cn.zh-CN/块存储/云盘基础操作/创建云盘/创建云盘.md)和[挂载数据盘](/cn.zh-CN/块存储/云盘基础操作/挂载数据盘.md)，创建包年包月云盘请参见[创建包年包月云盘]()。

独立冗余磁盘阵列（Redundant Array of Independent Disks，简称RAID）是将多块云盘按一定的方式组成一个磁盘阵列组。相比单块云盘，RAID能够有效的提高磁盘的容量、读写带宽、可靠性和可用性。

建议您使用RAID0或者RAID1模式，每块云盘采用相同大小的分区，从而减少云盘空间浪费。由于RAID5或者RAID6模式的奇偶校验数据会占用云盘IOPS，带来性能阻碍，因此不推荐使用RAID5或者RAID6模式。

下表对比了RAID0和RAID1模式的优缺点以及适用场景。

|模式|优势|劣势|适用场景|
|--|--|--|----|
|RAID0|I/O在存储卷内以条带化的方式分布在各云盘上。增加云盘空间会直接增加吞吐量，阵列中的容量和带宽等于各个云盘容量和带宽之和。|单块云盘的损坏有可能造成整个虚拟盘数据丢失，缺乏数据冗余能力。|对I/O性能要求很高，并且已通过其他方式对备份数据，或者不需要备份数据的应用。|
|RAID1|数据以镜像的方式存储在各云盘上，可以获取更高的数据冗余性。阵列中的容量和带宽等于阵列中容量和带宽最小的云盘。|因为要同时向多块云盘写入数据，写性能较差。|容错能力比 I/O 性能更重要，例如在关键应用程序中。|

## 操作步骤

1.  以root权限远程连接ECS实例。连接方式请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  使用lsblk命令罗列ECS实例上所有云盘信息。

    ```
    root@lvs06:~# lsblk
    ```

3.  使用mdadm命令创建RAID阵列/dev/md0。

    -   创建RAID0模式可以执行如下命令

        ```
        root@raid06:~# mdadm --create /dev/md0 --level=0 --raid-devices=5 /dev/vd\[bcdef\]
        ices=5 /dev/vd[bcdef]
        mdadm: Defaulting to version 1.2 metadata
        mdadm: array /dev/md0 started
        ```

        `--level=0`选项表示用于将阵列条带化的RAID0模式，/dev/vd\[bcdef\]值表示使用/dev/vdb、/dev/vdc、/dev/vdd、/dev/vde和/dev/vdf五块云盘组成一个RAID阵列。

    -   创建RAID1模式可以执行如下命令

        ```
        root@raid06:~# mdadm --create /dev/md0 --level=1 --raid-devices=5 /dev/vd\[bcdef\]
        ```

        `--level=1`选项表示用于将阵列镜像化的RAID1模式。

4.  使用mdadm命令查看创建的RAID阵列/dev/md0信息。

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
    
        Update Time : Sun May 1912:31:532019
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

5.  使用mkfs命令在RAID阵列上创建一个文件系统，例如，ext4文件系统。

    您也可以创建其他类型的文件系统。

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

6.  使用root权限创建一份包含RAID信息的配置文件，设置RAID阵列在启动ECS实例时自动重组。

    ```
    root@raid06:~# sudo mdadm --detail --scan \| sudo tee -a /etc/mdadm/mdadm.conf
    ```

7.  （可选）创建挂载点，例如/media/raid0。

    您也可以将云盘挂载到已有目录下。

    ```
    root@raid06:~# mkdir /media/raid0
    ```

8.  使用mount命令挂载文件系统，例如将/dev/md0挂载至/media/rad0。

    ```
    root@raid06:~# mount /dev/md0 /media/raid0
    ```

9.  使用df命令查看RAID阵列的挂载信息。

    返回信息中，文件系统必须挂载到指定的挂载点。

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


如果您需要在每次启动ECS实例时设置自动加载RAID阵列，可以在/etc/fstab配置文件中添加如下信息。

1.  向/etc/fstab配置文件写入自启动设置。

    ```
    root@raid06:~# echo /dev/md0 /media/rad0 defaults,nofail,nobootwait 0 2 \>\> /etc/fstab
    ```

    **说明：** 如果您需要在未挂载RAID阵列的情况下启动ECS实例，可以添加nofail配置。即使在安装云盘时出现错误，nofail配置也允许启动ECS实例。如果您使用的是Ubuntu系统，还需要额外添加nobootwait配置。

2.  使用mount命令/etc/fstab配置文件中挂载所有文件系统。

    ```
    root@raid06:~# mount -a
    ```


