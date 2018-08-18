# 扩容数据盘\_Linux {#concept_z11_xsh_ydb .concept}

随着业务的增长，您的数据盘容量可能无法满足数据存储的需要，这时您可以使用 **磁盘扩容** 功能扩容数据盘。

**说明：** 

-   挂载在实例上的数据盘，只有当实例处于 **运行中** \(**Running**\) 或 **已停止**\(**Stopped**\) 状态时才可以扩容。**扩容这种数据盘需要在控制台上重启实例后才能使扩容后的容量生效，而重启实例会停止实例，中断您的业务，所以请您谨慎操作**。
-   建议在扩容数据盘之前手动创建快照，以备份数据。
-   无论数据盘的状态是 **待挂载** 还是 **使用中**，都可以执行磁盘扩容操作。
-   包年包月实例如果做过 [续费降配](../intl.zh-CN/产品定价/续费实例/续费降配.md#) 操作，当前计费周期的剩余时间内，实例上的包年包月云盘不支持扩容磁盘操作。
-   如果数据盘正在创建快照，则不允许执行扩容数据盘的操作。
-   磁盘扩容功能只能扩容数据盘，不能扩容系统盘或本地盘（本地 SSD 盘等）。

本文以一个高效云盘的数据盘和一个运行CentOS 7.3 64位的 ECS 实例为例，说明如何扩容数据盘并使扩容后的容量可用。

您可以按以下步骤完成扩容操作：

[步骤 1. 在控制台上扩容数据盘的磁盘空间](#ResizeInConsole)

[步骤 2. 登录实例扩容文件系统](#ResizeInInstance)

## 步骤 1. 在控制台上扩容数据盘的磁盘空间 {#ResizeInConsole .section}

按以下步骤在控制台上扩容数据盘的磁盘空间：

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  在左侧导航栏里，选择 **存储** \> **云盘**。

    **说明：** 如果您需要扩容的数据盘已经挂载在某个实例上，您可以单击 **实例**，找到相应实例后，进入实例详情页，并单击 **本实例磁盘**。

3.  选择地域。
4.  找到需要扩容的磁盘，并在 **操作** 列中，选择 **更多** \> **磁盘扩容**。
5.  在 磁盘扩容 页面上，设置 **扩容后容量**，在本示例中为30 GiB。扩容后容量只能比当前容量大。
6.  待页面上显示费用信息后，单击 **确定扩容**。

    **说明：** 扩容成功后，磁盘列表里即显示扩容后的容量。但是，如果您的数据盘已经挂载到实例上，只有在控制台上 [重启实例](intl.zh-CN/用户指南/实例/重启实例.md#) 后，登录实例才能看到新的磁盘空间容量。


在控制台上扩容数据盘的磁盘空间后，

-   如果数据盘已经挂载到实例上，您必须执行 [步骤 2. 登录实例扩容文件系统](#ResizeInInstance)。
-   如果数据盘未挂载到实例上，您必须先挂载数据盘（参见 [挂载云盘](intl.zh-CN/用户指南/云盘/挂载云盘.md#)），再根据数据盘的实际情况执行不同的操作：
    -   如果这是一个未格式化的数据盘，您必须格式化数据盘。详细信息，请参见 [Linux 格式化和挂载数据盘](../intl.zh-CN/个人版快速入门/步骤 4：格式化数据盘/Linux 格式化和挂载数据盘.md#)。
    -   如果这个数据盘之前已经格式化并分区，您必须 [步骤 2. 登录实例扩容文件系统](#ResizeInInstance)。

## 步骤 2. 登录实例扩容文件系统 {#ResizeInInstance .section}

在ECS控制台上完成磁盘扩容后，磁盘每个分区的文件系统并未扩容。您需要登录实例扩容文件系统。

在本示例中，假设数据盘挂载在一台Linux实例上，实例的操作系统为CentOS 7.3 64位，未扩容前的数据盘只有一个主分区（/dev/vdb1，ext4文件系统），文件系统的挂载点为 /resizetest，文件系统扩容完成后，数据盘仍然只有一个主分区。

1.  [使用用户名密码验证连接 Linux 实例](intl.zh-CN/用户指南/连接实例/使用用户名密码验证连接 Linux 实例.md#)。
2.  运行 `umount` 命令卸载主分区。

    ```
    umount /dev/vdb1
    ```

    **说明：** 使用 `df -h` 查看是否卸载成功，如果看不到 /dev/vdb1 的信息表示卸载成功。以下为示例输出结果。

    ```
    
    [root@iXXXXXX ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.5G 36G 4% /
    devtmpfs 487M 0 487M 0% /dev
    tmpfs 497M 0 497M 0% /dev/shm
    tmpfs 497M 312K 496M 1% /run
    tmpfs 497M 0 497M 0% /sys/fs/cgroup
    tmpfs 100M 0 100M 0% /run/user/0
    ```

3.  使用 `fdisk` 命令删除原来的分区并创建新分区：

    **说明：** 如果您使用 `parted` 工具操作分区，不能与 `fdisk` 交叉使用，否则会导致分区的起始扇区不一致。关于 `parted` 工具的使用说明可以参考[这里](#parted)。

    1.  运行命令 `fdisk -l` 罗列分区信息并记录扩容前数据盘的最终容量、起始扇区（First sector）位置。
    2.  运行命令 `fdisk [数据盘设备名]` 进入 `fdisk` 界面。本示例中，命令为 `fdisk /dev/vdb`。
    3.  输入 `d` 并按回车键，删除原来的分区。

        **说明：** 删除分区不会造成数据盘内数据的丢失。

    4.  输入 `n` 并按回车键，开始创建新的分区。
    5.  输入 `p` 并按回车键，选择创建主分区。因为创建的是一个单分区数据盘，所以只需要创建主分区。

        **说明：** 如果要创建4个以上的分区，您应该创建至少一个扩展分区，即选择 `e`。

    6.  输入分区编号并按回车键。因为这里仅创建一个分区，所以输入 1。
    7.  输入第一个可用的扇区编号：为了保证数据的一致性，First sector需要与原来的分区保持一致。在本示例中，按回车键采用默认值。

        **说明：** 如果发现First sector显示的位置和之前记录的不一致，说明之前可能使用 `parted` 来分区，那么就停止当前的 `fdisk` 操作，使用 [`parted`](#parted) 重新操作。

    8.  输入最后一个扇区编号：因为这里仅创建一个分区，所以按回车键采用默认值。
    9.  输入 `wq` 并按回车键，开始分区。

        ```
        
        [root@iXXXXXX ~]# fdisk /dev/vdb
        Welcome to fdisk (util-linux 2.23.2).
        Changes will remain in memory only, until you decide to write them.
        Be careful before using the write command.
        Command (m for help): d
        Selected partition 1
        Partition 1 is deleted
        Command (m for help): n
        Partition type:
        p primary (0 primary, 0 extended, 4 free)
        e extended
        Select (default p):
        Using default response p
        Partition number (1-4, default 1):
        First sector (2048-62914559, default 2048):
        Using default value 2048
        Last sector, +sectors or +size{K,M,G} (2048-62914559, default 62914559):
        Using default value 62914559
        Partition 1 of type Linux and of size 30 GiB is set
        Command (m for help): wq
        The partition table has been altered!
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

        **说明：** 如果您使用的是 `parted` 工具，进入 `parted` 界面后，输入 `p` 罗列当前的分区情况。如果有分区，则使用 rm+ 序列号来删除老的分区表，然后使用 `unit s` 定义起始位置，单位使用扇区个数计量，最后使用 `mkpart` 命令来创建即可，如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9677/5353_zh-CN.png)

4.  部分操作系统里，修改分区后可能会重新自动挂载文件系统。建议先执行 `df -h` 重新查看文件系统空间和使用情况。如果文件系统重新被挂载，执行 `umount [文件系统名称]` 再次卸载文件系统。
5.  检查文件系统，并变更文件系统大小。

    首先 使用 df 或 parted 查看文件系统类型 

    ```
    
    # 检查文件系统 选择已安装的命令执行
    df -Th | grep "^/dev"
    parted /dev/vdb1 'print'
    
    
    ```

    如果显示扩容的分区类型是 xfs 系列，使用 

    ```
    
    xfs_repair /dev/vdb1 # 检查文件系统
    xfs_growfs /dev/vdb1 # 变更
    xfs_info /dev/vdb1 # 查看文件系统
    
    
    ```

    以下为示例输出结果。

    ```
    
    [root@iXXXXXX ~]# xfs_repair /dev/vdb1
    Phase 1 - find and verify superblock...
    Phase 2 - using internal log
            - zero log...
            - scan filesystem freespace and inode maps...
            - found root inode chunk
    Phase 3 - for each AG...
            - scan and clear agi unlinked lists...
            - process known inodes and perform inode discovery...
            - agno = 0
            - agno = 1
            - agno = 2
            - agno = 3
            - process newly discovered inodes...
    Phase 4 - check for duplicate blocks...
            - setting up duplicate extent list...
            - check for inodes claiming duplicate blocks...
            - agno = 0
            - agno = 1
            - agno = 2
            - agno = 3
    Phase 5 - rebuild AG headers and trees...
            - reset superblock...
    Phase 6 - check inode connectivity...
            - resetting contents of realtime bitmap and summary inodes
            - traversing filesystem ...
            - traversal finished ...
            - moving disconnected inodes to lost+found ...
    Phase 7 - verify and correct link counts...
    done
    [root@iXXXXXX ~]# xfs_growfs /dev/vdb1
    meta-data=/dev/vdb1              isize=256    agcount=4, agsize=26214336 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=0        finobt=0
    data     =                       bsize=4096   blocks=104857344, imaxpct=25
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=0
    log      =internal               bsize=4096   blocks=51199, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    data blocks changed from 104857344 to 157286144
    ```


    否则如果显示为 ext 系列的格式， 使用以下命令 

    ```
    
    e2fsck -f /dev/vdb1 # 检查文件系统
    resize2fs /dev/vdb1 # 变更文件系统大小
    
    
    ```

    **说明：** 

    -   使用 `e2fsck` 时，由于系统需要检查并订正文件系统元数据，所以速度较慢、耗时较长，请耐心等待。
    -   正确使用 `e2fsck` 和 `resize2fs` 指令，不会造成原有数据丢失。
    以下为示例输出结果。

    ```
    
    [root@iXXXXXX ~]# e2fsck -f /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/vdb1: 11/1835008 files (0.0% non-contiguous), 159218/7339776 blocks
    [root@iXXXXXX ~]# resize2fs /dev/vdb1
    resize2fs 1.42.9 (28-Dec-2013)
    Resizing the filesystem on /dev/vdb1 to 7864064 (4k) blocks.
    The filesystem on /dev/vdb1 is now 7864064 blocks long.
    ```

6.  将扩容完成的文件系统挂载到原来的挂载点（如本示例中的 /resizetest）。

    ```
    mount /dev/vdb1 /resizetest
    ```

7.  查看文件系统空间和使用情况：运行命令 `df -h`。如果出现扩容后的文件系统信息，说明挂载成功，可以使用扩容后的文件系统了。

    **说明：** 挂载操作完成后，不需要在控制台上重启实例即可开始使用扩容后的文件系统。

    以下为示例输出结果。

    ```
    
    [root@iXXXXXX ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.5G 36G 4% /
    devtmpfs 487M 0 487M 0% /dev
    tmpfs 497M 0 497M 0% /dev/shm
    tmpfs 497M 312K 496M 1% /run
    tmpfs 497M 0 497M 0% /sys/fs/cgroup
    tmpfs 100M 0 100M 0% /run/user/0
    /dev/vdb1 30G 44M 28G 1% /resizetest
    ```


