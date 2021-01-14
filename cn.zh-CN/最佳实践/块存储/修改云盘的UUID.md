---
keyword: [uuid冲突, 修改uuid, 云盘挂载报错]
---

# 修改云盘的UUID

如果您使用快照创建云盘后挂载到原Linux实例，新创建云盘的UUID会和原云盘冲突。本文介绍如何修改新云盘的UUID。

使用快照创建云盘后，新创建的云盘的UUID和原云盘是一样的。如果您将新创建的云盘挂载到原来的Linux实例，此时会导致UUID冲突，存在以下问题：

-   如果您使用系统盘快照创建一个新云盘，挂载到原Linux实例。Linux可能不是从系统盘启动，而是从新挂载的数据盘启动。
-   如果您的云盘使用xfs文件系统，会因为UUID冲突禁止挂载（mount），提示`“mount: wrong fs type, bad option, bad superblock on /dev/vdd1,”`。

因此，您在使用快照创建新云盘并在控制台挂载到原Linux实例后，需要登录实例修改新云盘的UUID，再执行挂载（mount）操作。关于如何修改云盘的UUID，您可以通过`blkid`命令查询文件系统类型，并根据查询结果选择合适的操作：

-   如果查询结果为`TYPE="ext4"`、`TYPE="ext3"`或`TYPE="ext2"`，具体操作，请参见[修改ext2、ext3或ext4文件系统分区的UUID](#section_gqh_rma_fsw)。
-   如果查询结果为`TYPE="xfs"`，具体操作，请参见[修改xfs文件系统分区的UUID](#section_qw6_51s_l6y)。

## 修改ext2、ext3或ext4文件系统分区的UUID

**说明：** 本示例以/dev/vdb1为例，您需要根据自己的设备名修改相关命令。

1.  远程连接ECS实例。连接方式请参见[通过VNC远程连接登录Linux实例](/cn.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令查询云盘的UUID。

    ```
    blkid
    ```

    查询结果如下所示，此时通过快照新创建云盘的UUID和原云盘一样。

    ![uuid信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8520299061/p210223.png)

3.  运行以下命令检查文件系统。

    ```
    e2fsck -f /dev/vdb1
    ```

4.  运行以下命令为云盘生成新的UUID。

    ```
    uuidgen | xargs tune2fs /dev/vdb1 -U
    ```

5.  运行以下命令查看是否已经修改UUID。

    ```
    blkid
    ```

    查询结果如下，表示已经修改/dev/vdb1的UUID。

    ![uuid已变动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8520299061/p210347.png)

6.  运行以下命令挂载（mount）云盘。

    ```
    mount /dev/vdb1 /mnt
    ```

7.  配置/etc/fstab文件，开机自动挂载新云盘。

    关于如何配置/etc/fstab文件，请参见[在fstab文件中配置UUID方式自动挂载数据盘](/cn.zh-CN/最佳实践/块存储/在fstab文件中配置UUID方式自动挂载数据盘.md)。


## 修改xfs文件系统分区的UUID

**说明：** 本示例以/dev/vdd1为例，您需要根据自己的设备名修改相关命令。

1.  远程连接ECS实例。连接方式请参见[通过VNC远程连接登录Linux实例](/cn.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令查询云盘的UUID。

    ```
    blkid
    ```

    查询结果如下所示，此时通过快照新创建云盘的UUID和原云盘一样。

    ![xfs-uuid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6255299061/p210365.png)

3.  运行以下命令为云盘生成新的UUID。

    ```
    xfs_admin -U generate /dev/vdd1
    ```

4.  运行以下命令查看是否已经修改UUID。

    ```
    blkid
    ```

    查询结果如下，表示已经修改/dev/vdd1的UUID。

    ![uuid结果-xfs](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6255299061/p210558.png)

5.  运行以下命令挂载（mount）云盘。

    ```
    mount /dev/vdd1 /mnt
    ```

6.  配置/etc/fstab文件，开机自动挂载新云盘。

    关于如何配置/etc/fstab文件，请参见[在fstab文件中配置UUID方式自动挂载数据盘](/cn.zh-CN/最佳实践/块存储/在fstab文件中配置UUID方式自动挂载数据盘.md)。


## 相关文档

-   [使用快照创建云盘](/cn.zh-CN/块存储/云盘基础操作/创建云盘/使用快照创建云盘.md)
-   [在fstab文件中配置UUID方式自动挂载数据盘](/cn.zh-CN/最佳实践/块存储/在fstab文件中配置UUID方式自动挂载数据盘.md)
-   [Linux系统中xfs类型分区在挂在时提示“mount: wrong fs type, bad option, bad superblock on /dev/vdd1,”](https://help.aliyun.com/knowledge_detail/151196.html)

