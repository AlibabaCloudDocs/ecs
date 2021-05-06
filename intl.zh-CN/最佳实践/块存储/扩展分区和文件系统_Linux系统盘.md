# 扩展分区和文件系统\_Linux系统盘

本文提供了如何使用growpart和resize2fs等工具完成Linux系统盘扩展分区和文件系统的操作指导。

在扩展系统盘分区和文件系统前，请提前完成以下工作。

1.  已创建快照备份数据。

    为防止操作失误导致数据丢失，建议您操作前使用快照备份数据。具体操作请参见[创建一个云盘快照](/intl.zh-CN/快照/使用快照/创建一个云盘快照.md)。

2.  已在控制台上扩容云盘。

    若尚未扩容，请参见[在线扩容云盘（Linux系统）](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)或[离线扩容云盘（Linux系统）](/intl.zh-CN/块存储/扩容云盘/离线扩容云盘（Linux系统）.md)。

3.  远程连接ECS实例。连接方式请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。
4.  根据操作系统安装growpart或者xfsprogs扩容格式化工具。

    -   Alibaba Cloud Linux 2、CentOS 7

        运行`yum install <package\_name\>`命令安装工具，示例如下。

        ```
        yum install cloud-utils-growpart xfsprogs -y
        ```

    -   Ubuntu 14、Ubuntu 16、Ubuntu 18、Debian 9

        运行`apt install <package\_name\>`命令安装工具，示例如下。

        ```
        apt install cloud-guest-utils xfsprogs -y
        ```

    -   Debian 8、OpenSUSE 42.3、OpenSUSE 13.1、SUSE Linux Enterprise Server 12 SP2

        请使用上游版本（upstream）的growpart或者xfsprogs工具。

    **说明：** 当出现因扩容格式化工具问题导致的扩容失败时，建议您卸载工具后重新安装。

5.  运行`uname -a`命令查看实例的内核版本。
    -   如果内核版本大于等于3.6.0，请参见[高内核版本的操作步骤](#section_gxq_3tw_dhb)。
    -   如果内核版本小于3.6.0，如CentOS 6、Debian 7和SUSE Linux Enterprise Server 11 SP4等发行版，需要经过一次控制台重启或者API重启才能完成分区扩容。请参见[低内核版本的操作步骤](#section_vxq_3tw_dhb)。

本文的操作步骤适用于以下分区和文件系统格式的云盘。

-   分区格式支持MBR、GPT
-   文件系统支持ext\*、xfs、btrfs

## 扩展高内核版本实例的系统盘分区和文件系统

本节以Alibaba Cloud Linux 2.1903 LTS 64位操作系统为例，说明扩展分区和文件系统的步骤。

**说明：** 本示例操作命令同样适用于CentOS 7系统。

1.  运行以下命令查看现有云盘大小。

    ```
    fdisk -l
    ```

    以下示例返回云盘（/dev/vda）容量是100GiB。

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

2.  运行以下命令查看云盘分区大小和文件系统类型。

    ```
    df -Th
    ```

    以下示例返回分区（/dev/vda1）容量是40GiB，文件系统类型为ext4。

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

3.  运行以下命令扩容分区。

    ```
    growpart <DeviceName\> <PartionNumber\>
    ```

    示例命令表示扩容系统盘的第一个分区（/dev/vda1）。

    ```
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=83883999 end=83886047 new: size=209713119 end=209715167
    ```

    **说明：** 如果您在运行`growpart /dev/vda 1`时，系统提示`unexpected output in sfdisk --version [sfdisk，来自 util-linux 2.23.2]`，可以尝试修改字符编码解决问题。具体操作，请参见[常见问题](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)。

4.  扩展文件系统。

    根据文件系统类型选择以下扩展方式，请使用`df -Th`命令查看文件系统类型。

    -   ext\*文件系统（例如ext3和ext4）：运行以下命令扩展文件系统。

        ```
        resize2fs <PartitionName\>
        ```

        示例命令表示为扩容系统盘的/dev/vda1分区的文件系统。

        ```
        [root@ecshost ~]# resize2fs /dev/vda1
        resize2fs 1.42.9 (28-Dec-2013)
        Filesystem at /dev/vda1 is mounted on /; on-line resizing required
        old_desc_blocks = 3, new_desc_blocks = 7
        The filesystem on /dev/vda1 is now 26214139 blocks long.
        ```

    -   xfs文件系统：运行以下命令扩展文件系统。

        ```
        xfs_growfs <mountpoint\>
        ```

        示例命令表示为扩容系统盘的/dev/vda1分区的文件系统。其中根目录（/）为/dev/vda1的挂载点。

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

        **说明：** 不同版本的xfs\_growfs命令可能存在差异，您可以运行`xfs_growfs --help`查看对应的命令。

5.  运行以下命令检查云盘扩容结果。

    ```
    df -h
    ```

    以下示例返回分区（/dev/vda1）容量是100GiB，表示已经成功扩容。

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


## 扩展低内核版本实例的系统盘分区和文件系统

本节以CentOS 6操作系统为例，说明扩展分区和文件系统的步骤。

1.  切换CentOS 6的yum软件源。

    CentOS 6操作系统版本结束了生命周期（EOL），如果您需要在CentOS 6上通过yum安装软件，需要先切换yum软件源。具体操作，请参见[CentOS 6 EOL如何切换源](/intl.zh-CN/镜像/常见问题/CentOS 6 EOL如何切换源.md)。

2.  运行以下命令安装dracut-modules-growroot工具。

    ```
    yum install -y dracut-modules-growroot
    ```

    **说明：** 如果您使用的是其他软件包管理器，请将yum修改为对应的命令。

3.  运行以下命令覆盖已有的initramfs文件。

    ```
    dracut -f
    ```

4.  运行以下命令查看云盘和分区信息。

    -   查看云盘大小：

        ```
        fdisk -l
        ```

        以下示例返回云盘（/dev/vda）容量是100GiB。

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

    -   查看云盘分区和文件系统类型：

        ```
        df -Th
        ```

        以下示例返回分区（/dev/vda1）容量是20 GiB，文件系统类型为ext4。

        ```
        [root@ecshost ~]# df -h
        Filesystem     Type      Size  Used Avail Use% Mounted on
        /dev/vda1      ext4       20G  1.1G   18G   6% /
        tmpfs          tmpfs     7.8G     0  7.8G   0% /dev/shm
        ```

5.  运行以下命令扩容分区。

    ```
    growpart <DeviceName\> <PartionNumber\>
    ```

    示例命令表示扩容系统盘的第一个分区（/dev/vda1）。

    ```
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

6.  在控制台重启实例。

    **说明：** 只能通过控制台重启实例或者调用API RebootInstance重启实例，扩容操作才能生效。具体操作，请参见[重启实例](/intl.zh-CN/实例/管理实例/重启实例.md)和[RebootInstance](/intl.zh-CN/API参考/实例/RebootInstance.md)。

7.  再次远程连接实例。

8.  扩展文件系统。

    根据文件系统类型选择以下扩展方式，您可以通过运行`df -h`如何查看文件系统类型。

    -   ext\*文件系统（例如ext3和ext4）：运行以下命令扩展文件系统。

        ```
        resize2fs <PartitionName\>
        ```

        示例命令表示为扩容系统盘的/dev/vda1分区的文件系统。

        ```
        [root@ecshost ~]# resize2fs /dev/vda1
        resize2fs 1.41.12 (17-May-2010)
        Filesystem at /dev/vda1 is mounted on /; on-line resizing required
        old desc_blocks = 2, new_desc_blocks = 7
        Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
        The filesystem on /dev/vda1 is now 26213807 blocks long.
        ```

    -   xfs文件系统：运行以下命令扩展文件系统。

        ```
        xfs_growfs <mountpoint\>
        ```

        示例命令表示为扩容系统盘的/dev/vda1分区的文件系统。其中根目录（/）为/dev/vda1的挂载点。

        ```
        [root@ecshost ~]# xfs_growfs /
        ```

        **说明：** 不同版本的xfs\_growfs命令可能存在差异，请运行`xfs_growfs --help`查看对应的命令。

9.  运行以下命令查看云盘分区大小。

    ```
    df -h
    ```

    以下示例返回分区（/dev/vda1）容量是100GiB，表示已经成功扩容。

    ```
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.1G   93G   2% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```


**相关文档**  


[在线扩容云盘（Linux系统）](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)

[离线扩容云盘（Linux系统）](/intl.zh-CN/块存储/扩容云盘/离线扩容云盘（Linux系统）.md)

[扩展分区和文件系统\_Linux数据盘](/intl.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.md)

