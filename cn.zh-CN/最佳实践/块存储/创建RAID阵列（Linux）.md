# 创建RAID阵列（Linux）

本文以Ubuntu系统ECS实例为例，介绍了如何使用Linux系统内置的mdadm命令为多块数据盘创建一个200 GiB的RAID阵列。

您已经创建并挂载了多块云盘。建议您创建具有相同容量和相同类型的云盘。创建并挂载云盘的具体操作，请参见[创建云盘](/cn.zh-CN/块存储/云盘基础操作/创建云盘/创建云盘.md)和[挂载数据盘](/cn.zh-CN/块存储/云盘基础操作/挂载数据盘.md)。

独立冗余磁盘阵列（Redundant Array of Independent Disks，简称RAID）是将多块云盘按一定的方式组成一个磁盘阵列组。相比单块云盘，RAID能够有效的提高磁盘的容量、读写带宽、可靠性和可用性。

建议您使用RAID0或者RAID1模式，每块云盘采用相同大小的分区，从而减少云盘空间浪费。由于RAID5或者RAID6模式的奇偶校验数据会占用云盘IOPS，带来性能阻碍，因此不推荐使用RAID5或者RAID6模式。

下表对比了RAID0和RAID1模式的优缺点以及适用场景。

|模式|优势|劣势|适用场景|
|--|--|--|----|
|RAID0|I/O在存储卷内以条带化的方式分布在各云盘上。增加云盘空间会直接增加吞吐量，阵列中的容量和带宽等于各个云盘容量和带宽之和。|单块云盘的损坏有可能造成整个虚拟盘数据丢失，缺乏数据冗余能力。|对I/O性能要求很高，并且已通过其他方式对备份数据，或者不需要备份数据的应用。|
|RAID1|数据以镜像的方式存储在各云盘上，可以获取更高的数据冗余性。阵列中的容量和带宽等于阵列中容量和带宽最小的云盘。|因为要同时向多块云盘写入数据，写性能较差。|容错能力比 I/O 性能更重要，例如在关键应用程序中。|

## 操作步骤

1.  以root权限远程连接ECS实例。连接方式请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  运行以下命令查看ECS实例上所有云盘信息。

    ```
    lsblk
    ```

    结果如下所示。

    ![lsblk](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5221640261/p271747.png)

3.  使用mdadm命令创建RAID阵列/dev/md0。

    请根据您的实际情况，创建RAID0或RAID1模式。

    **说明：**

    -   以下示例中`/dev/vd[bcdef]`表示为/dev/vdb、/dev/vdc、/dev/vdd、/dev/vde和/dev/vdf五块云盘组成RAID阵列。如果您使用其他云盘，需要修改成对应的云盘。
    -   如果提示未安装mdadm，请先运行`apt-get install mdadm`命令安装mdadm工具。
    -   创建RAID0模式，运行以下命令。

        ```
        mdadm --create /dev/md0 --level=0 --raid-devices=5 /dev/vd[bcdef]
        ```

        -   `--level=0`：表示用于将阵列条带化的RAID0模式。
        -   `--raid-devices=5`：表示RAID阵列由五块云盘组成。
        -   `/dev/vd[bcdef]`：表示使用/dev/vdb、/dev/vdc、/dev/vdd、/dev/vde和/dev/vdf五块云盘组成一个RAID阵列。
        结果如下所示。

        ![mdadm_raid0](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5221640261/p271752.png)

    -   创建RAID1模式，运行以下命令。

        ```
        mdadm --create /dev/md0 --level=1 --raid-devices=5 /dev/vd[bcdef]
        ```

        -   `--level=1`表示用于将阵列镜像化的RAID1模式。
        -   `--raid-devices=5`：表示RAID阵列由五块云盘组成。
        -   `/dev/vd[bcdef]`：表示使用/dev/vdb、/dev/vdc、/dev/vdd、/dev/vde和/dev/vdf五块云盘组成一个RAID阵列。
4.  运行以下命令查看创建的RAID阵列/dev/md0信息。

    ```
    mdadm --detail /dev/md0
    ```

    结果如下所示。

    ![raid0](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1886640261/p271751.png)

5.  运行以下命令在RAID阵列上创建一个文件系统，例如，ext4文件系统。

    您也可以创建其他类型的文件系统。

    ```
    mkfs.ext4 /dev/md0
    ```

    结果如下所示。

    ![mkfs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1886640261/p271801.png)

6.  运行以下命令，创建一份包含RAID信息的配置文件，设置RAID阵列在启动ECS实例时自动重组。

    ```
    sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
    ```

7.  挂载RAID阵列的文件系统。

    1.  运行以下命令，创建挂载点，例如/media/raid0。

        ```
        mkdir /media/raid0
        ```

        **说明：** 您也可以将云盘挂载到已有目录下，例如/mnt。

    2.  运行以下命令挂载文件系统，例如将/dev/md0挂载至/media/rad0。

        ```
        mount /dev/md0 /media/raid0
        ```

8.  运行以下命令查看RAID阵列的挂载信息。

    ```
    df -h
    ```

    结果如下所示，返回信息中，文件系统已经挂载到指定的挂载点。

    ![挂载信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1886640261/p271901.png)


如果您需要在每次启动ECS实例时设置自动加载RAID阵列，可以在/etc/fstab配置文件中添加如下信息。

1.  运行以下命令，向/etc/fstab配置文件写入自启动设置。

    ```
    echo `blkid /dev/md0 | awk '{print $2}' | sed 's/\"//g'` /media/raid0 ext4 defaults 0 0 >> /etc/fstab
    ```

    -   `/dev/md0`：磁盘阵列名称。
    -   `/media/raid0`：挂载点信息，如果需要挂载到其他路径，您需要修改成对应路径。
    **说明：** 如果您需要在未挂载RAID阵列的情况下启动ECS实例，可以添加nofail配置。即使在安装云盘时出现错误，nofail配置也允许启动ECS实例。如果您使用的是Ubuntu系统，还需要额外添加nobootwait配置。

2.  运行以下命令挂载/etc/fstab配置文件中的所有文件系统。

    ```
    mount -a
    ```


