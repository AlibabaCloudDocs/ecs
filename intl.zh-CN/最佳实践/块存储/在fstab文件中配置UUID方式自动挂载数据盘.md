# 在fstab文件中配置UUID方式自动挂载数据盘

在Linux系统中，您可以通过配置fstab文件让ECS启动时会自动挂载数据盘。但是，如果fstab文件配置不当，那么您的云盘挂载顺序变动后，可能会导致ECS重启后不能正常运行。本文介绍如何在fstab文件中配置UUID方式自动挂载数据盘，可以解决此类重启异常问题。

挂载到实例的云盘已经进行分区格式化。具体操作，请参见[Linux格式化数据盘](/intl.zh-CN/块存储/云盘/分区格式化数据盘/Linux格式化数据盘.md)。

fstab支持使用云盘分区名（例如/dev/vdb1）或UUID标识文件系统，两者的差异如下所示：

-   在fstab中使用云盘分区名标识文件系统，如果云盘的挂载顺序变更，云盘分区可能不会被正确的挂载（mount）到原来的挂载点。这种情况下可能会影响您ECS上运行的应用。
-   在fstab中使用UUID标识文件系统，如果云盘的挂载顺序变更，云盘分区仍然可以正确的挂载（mount）到原来的挂载点。因此，本文建议使用UUID标识文件系统。

## 操作步骤

1.  远程连接ECS实例。

    关于如何远程连接ECS实例，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令查看实例的云盘信息。

    ```
     fdisk -lu
    ```

    运行结果如下所示。

    ![查询云盘](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0707186061/p187006.png)

3.  运行以下命令查询云盘的UUID信息。

    ```
    blkid
    ```

    运行结果如下所示。

    ![查询uuid](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0707186061/p187034.png)

4.  运行以下命令分别创建数据盘的挂载点。

    -   创建/dev/vdb1的挂载点/test01：

        ```
        mkdir /test01
        ```

    -   创建/dev/vdc1的挂载点/test02：

        ```
        mkdir /test02
        ```

5.  在fstab文件中添加挂载信息。

    1.  运行以下命令编辑fstab。

        ```
        vi /etc/fstab
        ```

    2.  按`i`键进入编辑模式。

    3.  新增以下挂载信息。

        ```
        UUID=59f23670-94c1-42d1-8bb0-209d7854****   /test01     ext4    defaults     0   0
        UUID=88619b1a-d971-41c2-91d0-3a440fc0****   /test02     xfs     defaults     0   0
        ```

        结果如下所示。

        ![fstab文件说明](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3616937061/p187115.png)

        |序号|字段|说明|
        |--|--|--|
        |①|<file system\>|要挂载的分区。此处建议使用UUID，可以使用`blkid`命令查询文件系统的UUID。 |
        |②|<dir\>|分区挂载位置。您可以自己创建新的挂载位置，例如本文中的/test01和/test02。 |
        |③|<type\>|要挂载分区的文件系统类型。您可以使用`blkid`命令查询分区的文件系统类型。 |
        |④|<options\>|挂载时使用的参数，一般情况下使用defaults参数。如果需要使用多个参数，通过英文逗号（,）分隔，例如`defaults,noatime`。对于<options\>参数的更多信息，请参见[fstab说明](https://wiki.debian.org/fstab)。 |
        |⑤|<dump\>|dump工具是否对这个文件系统进行备份。        -   0：表示忽略。
        -   1：表示进行备份。
一般情况下没有使用dump工具，可以设置为0。 |
        |⑥|<pass\>|fsck检查文件系统的优先级。        -   0：表示设备不进行检查。
        -   1：如果需要检查，根目录设置为1。
        -   2：如果需要检查，其它所有需要被检查的设备设置为2。
一般情况下，可以设置为0。 |

    4.  修改完成后，按`Esc`键退出编辑模式。

    5.  输入`:wq`后，按`Enter`键保存并退出。

6.  运行以下命令查看fstab文件。

    ```
    cat /etc/fstab
    ```

    执行结果如下所示。

    ![查询fstab](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4946937061/p187136.png)

7.  运行以下命令挂载数据盘。

    -   挂载/dev/vdb1：

        ```
        mount /dev/vdb1 /test01
        ```

    -   挂载/dev/vdc1：

        ```
        mount /dev/vdc1 /test02
        ```

8.  运行以下命令检查挂载结果。

    ```
    df -h
    ```

    执行结果如下所示。

    ![查询结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9937986061/p187224.png)


配置完成后，您后续如果重启ECS实例，系统将自动挂载数据盘。

