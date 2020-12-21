---
keyword: [分区, 分区格式化, 大于2 TiB, 数据盘, parted, GPT]
---

# 分区格式化大于2 TiB数据盘

本文介绍了如何在不同的操作系统里分区格式化一块大于2 TiB的数据盘。

-   数据盘已经挂载到实例上。具体操作请参见[挂载数据盘](/intl.zh-CN/块存储/云盘/挂载数据盘.md)。
-   远程登录实例。具体连接方法请参见[连接方式概述](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

-   创建快照的速度和数据的增量成正比，云盘占用的容量越大，创建快照的时间也会更长。
-   阿里云块存储支持的分区格式包括MBR（Master Boot Record）和GPT（Globally Unique Identifier Partition Table）。其中，MBR只支持处理不大于2 TiB的容量，且只支持划分4个主区。如果您需要使用大于2 TiB的数据盘，您必须采用GPT格式。

    **说明：** MBR和GPT分区格式间相互转换有数据丢失的风险。您在使用快照创建云盘或者扩容云盘容量，并且希望设置的新容量大于2 TiB时，建议您提前查询数据盘采用的分区格式是否为MBR。如果您需要保留数据，建议您重新创建并挂载一块数据盘，采用GPT分区格式后，再将已有数据拷贝至新的数据盘上。

-   大于2 TiB的数据盘请采用下表中描述的分区工具、分区格式和文件系统。

    |操作系统|分区工具|分区格式|文件系统|
    |:---|:---|----|:---|
    |Windows|**磁盘管理**|GPT|NTFS|
    |Linux|parted|GPT|ext4或xfs|


## 分区格式化Windows数据盘

此章节以Windows Server 2012 R2 64位操作系统为例，说明如何在Windows实例中分区格式化一块大于2 TiB的全新数据盘。

1.  在Windows Server桌面，键盘按下Win + R组合键。

2.  在运行窗口输入diskmgmt.msc并单击**确定**，打开磁盘管理。

3.  找到需要分区格式化的磁盘（本示例中为**磁盘 1**）。磁盘状态显示为**脱机**。

4.  右击**磁盘 1**周边空白处，单击**联机**。

    联机后，**磁盘 1**的状态显示为**没有初始化**。

5.  右键单击**磁盘 1**周边的空白区，在弹出菜单中，选择**初始化磁盘**。

6.  在初始化磁盘对话框里，选择**磁盘 1**，并选择磁盘分区形式为**GPT**。

7.  在磁盘管理窗口，右键单击**磁盘 1**的**未分配**区域，选择**新建简单卷**，创建一个4 TiB的NTFS格式的卷。

8.  在新建简单卷向导中，单击**下一步**，并完成以下操作。

    1.  指定卷大小：指定简单卷大小。如果您只要创建一个主区，使用默认值。单击**下一步**。您也可以把**磁盘 1**分成多个分区来使用。

        **说明：** NTFS卷上的最大尺寸，理论上，NTFS的最大卷包含2 64 -1个簇。实际上，WinXP Pro中，NTFS卷的最大限制是2 32 -1个簇。例如，如果是64 KiB的簇，那NTFS卷的最大尺寸就是约256 TiB。如果选择4 KiB的簇，那NTFS卷的最大尺寸就是约16 TiB。NTFS会根据磁盘的容量来自动选择簇的大小。

    2.  分配驱动器号和路径：选择一个驱动器号（即盘符），例如D。单击**下一步**。

    3.  格式化分区：选择格式化设置，包括文件系统、分配单元大小和卷标，确认是否**执行快速格式化**和**启用文件和文件夹压缩**。例如，选择**执行快速格式化**。单击**下一步**。

    4.  开始创建新简单卷：当向导对话框里显示已经完成新简单卷的创建时，单击**完成**，关闭新建简单卷向导。


## 更换Windows数据盘分区格式

**说明：** 转换分区格式有数据丢失的风险，请确认您已完成数据备份工作。

此章节以Windows Server 2012 R2 64位操作系统为例，假设需要操作的数据盘容量为3 TiB。

1.  在Windows Server桌面，右键单击**开始**图标，选择**磁盘管理**。

2.  找到需要分区格式化的磁盘（本示例中为**磁盘 2**）。

3.  右键单击一个简单卷，在弹出菜单中，选择**删除卷**。

4.  右键单击磁盘周边的空白区，在弹出菜单中，选择**转换成GPT磁盘**。

5.  在磁盘管理窗口，右键单击磁盘的**未分配**区域，选择**新建简单卷**，创建一个3 TiB的NTFS格式的卷。

6.  在新建简单卷向导中，单击**下一步**，并完成以下操作。

    1.  指定卷大小：指定简单卷大小。如果您只要创建一个主区，使用默认值。单击**下一步**。您也可以把**磁盘 2**分成多个分区来使用。

        **说明：** NTFS卷上的最大尺寸，理论上，NTFS的最大卷包含2 64 -1个簇。实际上，WinXP Pro中，NTFS卷的最大限制是2 32 -1个簇。例如，如果是64 KiB的簇，那NTFS卷的最大尺寸就是约256 TiB。如果选择4 KiB的簇，那NTFS卷的最大尺寸就是约16 TiB。NTFS会根据磁盘的容量来自动选择簇的大小。

    2.  分配驱动器号和路径：选择一个驱动器号（即盘符），例如E，单击**下一步**。

    3.  格式化分区：选择格式化设置，包括文件系统、分配单元大小和卷标，确认是否**执行快速格式化**和**启用文件和文件夹压缩**。例如，选择**执行快速格式化**。单击**下一步**。

    4.  开始创建新简单卷：当向导对话框里显示已经完成新简单卷的创建时，单击**完成**，关闭新建简单卷向导。


## 分区格式化Linux数据盘

此章节以Alibaba Cloud Linux 2.1903 LTS 64位操作系统为例，说明如何在Linux实例上使用Parted工具和e2fsprogs工具分区并格式化一个大容量数据盘。假设需要处理的数据盘是一个新建的3 TiB的空盘，设备名为/dev/vdb。

前提条件：请确认您的Linux实例上已经安装了Parted工具和e2fsprogs工具。

-   运行以下命令安装Parted工具：

    ```
    yum install -y parted
    ```

-   运行以下命令安装e2fsprogs工具：

    ```
    yum install -y e2fsprogs
    ```


按以下步骤分区格式化大容量数据盘，并挂载文件系统。

1.  远程连接ECS实例。

    如何连接ECS实例，具体操作请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  查看是否存在数据盘。

    运行以下命令：

    ```
    fdisk -l
    ```

    运行结果如下所示，应包含数据盘信息。如果没有，表示您未挂载数据盘。

    ```
    Disk /dev/vdb: 3221.2 GB, 3221225472000 bytes, 6291456000 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    ```

3.  使用Parted工具为数据盘进行分区。

    1.  运行以下命令开始分区。

        ```
        parted /dev/vdb
        ```

    2.  运行以下命令，将默认的MBR分区格式转为GPT分区格式。

        ```
        mklabel gpt
        ```

    3.  运行以下命令，划分一个主分区，并设置分区的开始位置和结束位置。

        ```
        mkpart primary 1 100%
        ```

    4.  运行以下命令，检查分区是否对齐。

        ```
        align-check optimal 1
        ```

        运行结果如下所示：

        ```
        1 aligned
        ```

        **说明：** 如果返回的是`1 not aligned`，说明分区未对齐，建议您运行以下命令 ，再根据`（<optimal_io_size>+<alignment_offset>）/<physical_block_size>`的公式计算出最佳分区模式的起始扇区值。假设1024为计算得出的推荐扇区值，则您可以运行`mkpart primary 1024s 100%`重新划分一个主分区。

        ```
        cat /sys/block/vdb/queue/optimal_io_size
        cat /sys/block/vdb/queue/minimum_io_size
        cat /sys/block/vdb/alignment_offset
        cat /sys/block/vdb/queue/physical_block_size
        ```

    5.  运行以下命令，查看分区表。

        ```
        print
        ```

    6.  运行以下命令，退出Parted工具。

        ```
        quit
        ```

    Parted工具分区结果如下所示。

    ![parted分区](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8108182061/p174095.png)

4.  运行以下命令，使系统重读分区表。

    ```
    partprobe
    ```

5.  运行以下命令，为/dev/vdb1分区创建一个文件系统。

    根据您的需求运行以下任一命令，创建文件系统。

    -   创建一个ext4文件系统。

        ```
        mkfs -t ext4 /dev/vdb1
        ```

    -   创建一个xfs文件系统。

        ```
        mkfs -t xfs /dev/vdb1
        ```

    **说明：**

    -   如果数据盘的容量为16 TiB，您需要使用指定版本的e2fsprogs工具包格式化，请参见[附录一：升级e2fsprogs工具包](#e2fsprogs)。
    -   如果您要关闭ext4文件系统的lazy init功能，避免该功能对数据盘I/O性能的影响，请参见[附录二：关闭lazy init功能](#LazyInit)。
6.  运行以下命令，创建一个名为/test的挂载点。

    ```
    mkdir /test
    ```

7.  运行以下命令，将分区/dev/vdb1挂载到/test。

    ```
    mount /dev/vdb1 /test
    ```

8.  运行以下命令，查看目前磁盘空间和使用情况。

    ```
    df -h
    ```

    如果返回结果里出现新建文件系统的信息，说明挂载成功，您可以使用新的文件系统了。

    ![查看df结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4439182061/p174102.png)

9.  （推荐）在/etc/fstab文件中写入新分区信息，启动开机自动挂载分区。

    1.  运行以下命令，备份etc/fstab。

    2.  运行以下命令，向/etc/fstab里写入新分区信息。

        ```
        echo `blkid /dev/vdb1 | awk '{print $2}' | sed 's/\"//g'` /test ext4 defaults 0 0 >> /etc/fstab
        ```

        **说明：**

        -   需要使用root用户运行此命令。如果您使用的是普通用户，可运行`su -`命令切换到root用户，然后运行此命令；或者直接运行`sudo vi /etc/fstab`命令编辑/etc/fstab文件。
        -   建议在/etc/fstab中使用全局唯一标识符UUID来引用新分区。您可以使用blkid命令获得新分区的UUID。
    3.  运行以下命令，查看/etc/fstab的信息。

        ```
        cat /etc/fstab
        ```

        如果返回结果里出现了写入的新分区信息，说明写入成功。


至此，您已经成功分区并格式化了一个3 TiB数据盘。

## 附录一：Linux实例升级e2fsprogs工具包

如果数据盘容量为16 TiB，您需要使用1.42及以上版本的e2fsprogs工具包完成ext4文件系统格式化。如果e2fsprogs版本低于1.42，会出现如下错误信息。

```
mkfs.ext4: Size of device /dev/vdb too big to be expressed in 32 bits using a blocksize of 4096.            
```

您需要按以下方式安装高版本的e2fsprogs，如本示例中使用的1.42.8。

1.  运行以下命令检查e2fsprogs当前的版本。

    ```
    rpm -qa | grep e2fsprogs
    ```

    运行结果如下所示。

    ![查询版本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4163359951/p4439.png)

    如果当前版本低于1.42，按以下步骤安装软件。

2.  运行以下命令下载1.42.8版本的e2fsprogs。您可以在 [e2fsprogs](https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/?spm=a2c4g.11186623.2.14.Pb5baW)找到最新的软件包。

    ```
    wget https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/e2fsprogs-1.42.8.tar.gz
    ```

3.  依次运行以下命令，编译高版本的工具。

    1.  运行以下命令，解压软件包。

        ```
        tar xvzf e2fsprogs-1.42.8.tar.gz
        ```

    2.  运行以下命令，进入软件包目录。

        ```
        cd e2fsprogs-1.42.8
        ```

    3.  运行以下命令，生成Makefile文件。

        ```
        ./configure
        ```

    4.  运行以下命令，编译e2fsprogs。

        ```
        make
        ```

    5.  运行以下命令，安装e2fsprogs。

        ```
        make install
        ```

4.  运行以下命令检查是否成功更新版本。

    ```
    rpm -qa | grep e2fsprogs
    ```


## 附录二：Linux实例关闭lazy init功能

ext4文件系统默认开启lazy init功能。该功能开启时，实例会发起一个线程持续地初始化ext4文件系统的metadata，从而延迟metadata初始化。所以在格式化数据盘后的近期时间内，云盘的IOPS性能会受到影响，IOPS性能测试的数据会明显偏低。

如果您需要在格式化以后马上测试数据盘性能，请运行以下命令在格式化文件系统时关闭lazy\_init功能。

```
mke2fs -O 64bit,has_journal,extents,huge_file,flex_bg,uninit_bg,dir_nlink,extra_isize -E lazy_itable_init=0,lazy_journal_init=0   /dev/vdb1
```

**说明：** 关闭lazy init功能后，格式化的时间会大幅度地延长，格式化32 TiB的数据盘可能需要10分钟~30分钟。请您根据自身的需要选择是否使用lazy init功能。

