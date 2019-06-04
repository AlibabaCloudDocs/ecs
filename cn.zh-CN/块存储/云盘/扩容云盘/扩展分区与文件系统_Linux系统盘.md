# 扩展分区与文件系统\_Linux系统盘 {#concept_ocb_htw_dhb .concept}

本文提供了如何使用growpart和resize2fs工具完成Linux系统盘分区扩容及文件系统扩展的操作指导。

## 适用范围 { .section}

本文的操作步骤适用于以下分区和文件系统格式的云盘：

-   分区格式支持：mbr、gpt
-   文件系统支持：ext、xfs、btrfs、ufs

## 准备工作 {#section_h25_n5w_dhb .section}

1.  通过ECS控制台或者API扩容云盘。
2.  [创建快照](cn.zh-CN/快照/使用快照/创建快照.md#)以备份数据。
3.  实例已处于**运行中**状态。连接方式请参见[连接方式导航](../../../../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
4.  根据操作系统安装growpart扩容格式化工具。
    -   CentOS 7、Aliyun Linux：

        ```
        yum install cloud-utils-growpart
        ```

    -   Ubuntu 14、Ubuntu 16、Ubuntu 18、Debian 9：

        ```
        apt install cloud-guest-utils
        ```

    -   Debian 8、OpenSUSE 42.3、OpenSUSE 13.1、SUSE Linux Enterprise Server 12 SP2：请使用上游版本（upstream）的growpart工具
5.  检查实例的内核版本，如通过`uname -a`查看内核版本。
    -   内核版本大于3.6.0，则无需重启reboot便能完成扩容分区和文件系统。该情况请参见[高内核版本的操作步骤](#section_gxq_3tw_dhb)。
    -   内核版本小于3.6.0，如CentOS 6、Debian 7和SUSE Linux Enterprise Server 11 SP4等发行版，需要经过一次重启reboot才能完成分区扩容。该情况请参见[低内核版本的操作步骤](#section_vxq_3tw_dhb)。

## 高内核版本的操作步骤 {#section_gxq_3tw_dhb .section}

此处以CentOS 7操作系统为例演示分区扩展的步骤。

1.  运行`fdisk -l`查看现有磁盘大小。示例返回磁盘（/dev/vda）容量是100 GiB。

    ```
    [root@localhost ~]# fdisk -l
    
    Disk /dev/vda: 107.4 GB, 107374182400 bytes, 209715200 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x0008d73a
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    41943039    20970496   83  Linux
    ```

2.  运行`df -h`查看磁盘分区大小。示例返回分区容量（/dev/vda1）是20 GiB。

    ```
    [root@localhost ~]# df -h
    
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.5G   18G   8% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  344K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```

3.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的磁盘和对应的第几个分区扩容。示例命令表示为系统盘的第一个分区扩容。

    ```
    [root@localhost ~]# growpart /dev/vda 1
    
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

4.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ```
    [root@localhost ~]# resize2fs /dev/vda1
    
    resize2fs 1.42.9 (28-Dec-2013)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old_desc_blocks = 2, new_desc_blocks = 7
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```



5.  运行`df -h`查看磁盘分区大小。返回分区（/dev/vda1）是100 GiB，表示已经成功扩容。

    ```
    [root@localhost ~]# df -h
    
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.6G   93G   2% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  500K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```
    ```


## 低内核版本的操作步骤 {#section_vxq_3tw_dhb .section}

此处以CentOS 6操作系统为例演示分区扩展的步骤。

1.  安装dracut-modules-growroot工具。

    ```
    [root@AliYunOS ~]# yum install -y dracut-modules-growroot
    ```

    如果您使用的是其他软件包管理器，请将yum修改为对应的命令。

2.  覆盖已有的initramfs文件。

    ```
    [root@AliYunOS ~]# dracut -f
    ```

3.  运行`fdisk -l`查看现有磁盘大小。示例返回磁盘（/dev/vda）容量是100 GiB。

    ```
    [root@AliYunOS ~]# fdisk -l
    
    Disk /dev/vda: 107.4 GB, 107374182400 bytes
    255 heads, 63 sectors/track, 13054 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x0003a7b4
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *           1        2611    20970496   83  Linux
    ```

4.  运行`df -h`查看磁盘分区大小。示例返回分区容量（/dev/vda1）是20 GiB。

    ```
    [root@AliYunOS ~]# df -h
    
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.1G   18G   6% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```

5.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的磁盘和对应的第几个分区扩容。示例命令表示为系统盘的第一个分区扩容。

    ```
    [root@AliYunOS ~]# growpart /dev/vda 1
    
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```
    ```
    #xfs 文件系统请通过xfs_growfs 完成文件系统扩容
    [root@AliYunOS ~]# xfs_growfs /dev/vda 1
    ```
6.  重启实例。

    ```
    [root@AliYunOS ~]# reboot
    ```

7.  再次远程连接实例。
8.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ```
    [root@AliYunOS ~]# resize2fs /dev/vda1
    
    resize2fs 1.41.12 (17-May-2010)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old desc_blocks = 2, new_desc_blocks = 7
    Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

9.  运行`df -h`查看磁盘分区大小。返回分区（/dev/vda1）是100 GiB，表示已经成功扩容。

    ```
    [root@AliYunOS ~]# df -h
    
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.1G   93G   2% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```


