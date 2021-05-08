---
keyword: [ecs, 磁盘扩容, 扩展分区]
---

# 在线扩容云盘（Linux系统）

云盘（系统盘或数据盘）使用空间不足时，您可以扩容云盘的存储容量。本文介绍如何在不需要停止实例运行的情况下为Linux系统进行扩容云盘。

在Linux实例使用在线扩容云盘前，需要满足以下条件。

|资源|限制条件|
|--|----|
|实例|-   实例为I/O优化实例。
-   实例使用的公共镜像需要支持在线扩容功能，具体支持镜像请参见[支持在线扩容的操作系统](#section_cqo_5zn_ine)。
-   不支持以下实例规格：ecs.ebmc4.8xlarge、ecs.ebmhfg5.2xlarge、ecs.ebmg5.24xlarge。
-   实例状态为**运行中**（Running）。
-   实例的Linux内核不低于3.6.0版本。您可以使用`uname -a`命令查看内核版本。

如果Linux内核低于3.6.0版本，扩容分区操作请参见[扩展低内核版本实例的系统盘分区和文件系统](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux系统盘.md)和[扩展分区和文件系统\_Linux数据盘](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.md)。


**说明：** 如果您的ECS实例不符合在线扩容条件，您可以使用离线扩容云盘功能，具体请参见[离线扩容云盘（Linux系统）](/cn.zh-CN/块存储/扩容云盘/离线扩容云盘（Linux系统）.md)。 |
|云盘|-   云盘状态为**使用中**（In Use）。
-   云盘类型为ESSD云盘、SSD云盘或高效云盘。
-   包年包月ECS实例续费降配后，当前计费周期的剩余时间内，不支持扩容实例的包年包月云盘。
-   云盘扩容后的容量不能超过云盘最高容量，具体请参见[块存储使用限制](/cn.zh-CN/产品简介/使用限制.md)。

**说明：** 一个已有分区采用了MBR分区格式，则不支持扩容到2 TiB及以上。如果您的MBR分区容量需要扩容到2 TiB以上，建议您先创建一块大于2 TiB的云盘并格式化为GPT分区，再将MBR分区中的数据拷贝到GPT分区中。格式化GPT分区操作，请参见[分区格式化大于2 TiB数据盘](/cn.zh-CN/块存储/云盘基础操作/分区格式化数据盘/分区格式化大于2 TiB数据盘.md)。 |

本文示例中使用的配置如下所示。

|资源|描述|
|--|--|
|ECS实例的镜像|公共镜像Alibaba Cloud Linux 2.1903 LTS 64位|
|系统盘|/dev/vda：使用MBR分区和ext4文件系统，由40 GiB扩容到60 GiB。|
|数据盘|-   /dev/vdb：使用MBR分区和ext4文件系统，由40 GiB扩容到60 GiB。
-   /dev/vdc：使用GPT分区和xfs文件系统，由40 GiB扩容到60 GiB。 |

## 操作视频

以下视频介绍Linux系统如何在线扩容云盘。

## 步骤一：创建快照

在扩容云盘前，为云盘创建快照，做好数据备份。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  找到需要扩容云盘的实例，单击实例ID。

5.  在**实例详情**页，单击**云盘**页签。

6.  找到需要扩容的云盘，在**操作**列单击**创建快照**。

7.  在弹出的对话框中，输入快照名称，并按需绑定标签后，单击**确定**。

8.  单击**快照**页签，查看已创建的快照。

    当快照的**进度**为**100%**时，表示快照创建完成，您可以执行后续操作。


## 步骤二：在控制台扩容云盘容量

1.  在**实例详情**页，单击**云盘**页签。

2.  选择需要扩容的云盘，在**操作**列单击**更多** \> **云盘扩容**。

    如果需要批量扩容多个云盘，请使用阿里云主账号在**存储与快照** \> **云盘**页面选择多个云盘后，单击底部的**云盘扩容**。挂载在同一ECS实例下的云盘不支持批量扩容功能。

3.  在**磁盘扩容**页面，选中**在线扩容**，并设置**扩容后容量**。

    设置的**扩容后容量**不允许小于当前容量。

4.  确认费用，阅读并选中*云服务器ECS服务条款*后，单击**确认扩容**。

5.  阅读磁盘扩容须知后，单击**已阅读，继续扩容**，完成支付。


**说明：**

-   控制台上扩容云盘容量后，您还不能直接使用已扩容的容量，需要在ECS实例内部扩容分区和文件系统。
-   如果您使用LVM管理磁盘分区，在控制台完成扩容操作后，需要通过LVM扩容分区和文件系统。具体操作，请参见[扩容LVM逻辑卷](/cn.zh-CN/最佳实践/块存储/使用逻辑卷（Linux）/扩容LVM逻辑卷.md)。

## 步骤三：查看云盘分区情况

进入ECS实例内部，查看系统盘和数据盘的分区类型（MBR和GPT）和文件系统类型（ext4、xfs等）。不同的分区和文件系统，后续扩容分区和文件系统操作中存在差异。

1.  远程登录ECS实例。具体操作，请参见[通过密码或密钥认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用Workbench连接实例/通过密码或密钥认证登录Linux实例.md)。

2.  运行以下命令查看实例的云盘情况。

    ```
    fdisk -lu
    ```

    示例以系统盘（/dev/vda1）和数据盘（/dev/vdb1、/dev/vdc1）的三个分区为例，执行结果如下所示。

    ![查看云盘分区情况](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9339169951/p135832.png)

    |序号|分区|说明|
    |--|--|--|
    |①|`/dev/vda1`|系统盘，**System**取值**Linux**表示为MBR分区。|
    |②|`/dev/vdb1`|数据盘，**System**取值**Linux**表示为MBR分区。|
    |③|`/dev/vdc1`|数据盘，**System**取值**GPT**表示为GPT分区。|

    **说明：** 如果您的查询结果中云盘容量还是40 GiB（`Disk /dev/vda: 42.9 GB`），表示扩容不成功，建议您在控制台重启下本实例。

3.  运行以下命令确认已有分区的文件系统类型。

    ```
    df -Th
    ```

    执行结果如下所示。

    ![查看文件系统](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6620659951/p135833.png)


## 步骤四：扩容分区

通过查看云盘分区情况，在ECS实例内分区和文件系统并未扩容。此步骤介绍如何在ECS实例内部扩容云盘分区。

1.  在ECS实例内部，安装gdisk工具。

    如果您的分区为GPT格式，必须执行此步骤；如果您的分区为MBR格式，请跳过此步骤。

    ```
    yum install gdisk -y
    ```

2.  安装growpart工具。

    -   CentOS 7及以上版本运行以下命令。

        ```
        yum install -y cloud-utils-growpart
        ```

    -   Debian 9及以上版本、Ubuntu14及以上版本运行以下命令。

        更新软件源。

        ```
        apt-get update
        ```

        安装cloud-guest-utils。

        ```
        apt-get install -y cloud-guest-utils
        ```

3.  运行以下命令扩容分区。

    ```
    growpart /dev/vda 1
    ```

    此示例以扩容系统盘为例，`/dev/vda`和`1`之间需要空格分隔。如果需要扩容其他分区，请根据实际情况修改命令。执行结果如下所示。

    ![growpart](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6620659951/p135834.png)

    **说明：** 您在执行此步骤时，可能出现报错信息`unexpected output in sfdisk --version [sfdisk，来自 util-linux 2.23.2]`。关于如何排查此问题，请参见本文的常见问题部分。


## 步骤五：扩容文件系统

此步骤介绍如何ECS实例内部扩容分区的文件系统。

1.  在ECS实例内部，根据查询的文件系统类型，扩容文件系统。

    -   扩容ext\*（例如ext4）文件系统：运行以下命令扩容文件系统。

        扩容系统盘/dev/vda1的文件系统。

        ```
        resize2fs /dev/vda1    
        ```

        扩容数据盘/dev/vdb1的文件系统。

        ```
        resize2fs /dev/vdb1          
        ```

        **说明：** `/dev/vda1`和`/dev/vdb1`都是分区名称，您需要根据实际情况修改。

    -   扩容xfs文件系统：运行以下命令扩容文件系统。

        ```
        xfs_growfs /media/vdc
        ```

        **说明：** `/media/vdc`为`/dev/vdc1`的挂载点，您需要根据实际情况修改。

2.  运行以下命令检查扩容后结果。

    ```
    df -Th
    ```

    执行结果如下所示。

    ![查看扩容结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6620659951/p135835.png)

    扩容完成后，您需要根据实际情况检查数据是否正常。

    -   如果扩容成功，ECS实例中的业务程序能够正常运行，则完成操作。
    -   如果扩容失败，则通过备份的快照回滚数据。

## 支持在线扩容的操作系统

支持在线扩容的Linux公共镜像（或基于公共镜像制作的自定义镜像）包括：

-   Alibaba Cloud Linux：Alibaba Cloud Linux 2.1903 LTS 64位
-   CentOS：
    -   CentOS 6：CentOS 6.8及以上版本
    -   CentOS 7：CentOS 7.2及以上版本
    -   CentOS 8及以上版本
-   Red Hat Enterprise Linux：
    -   RHEL 6：RHEL 6.9及以上版本
    -   RHEL 7：RHEL 7.4及以上版本
    -   RHEL 8及以上版本
-   Ubuntu：Ubuntu 16及以上版本
-   Debian：Debian 8及以上版本
-   SUSE：SUSE 12 SP2及以上版本
-   OpenSUSE：OpenSUSE 42.3及以上版本

## 常见问题

-   **问题**：运行`growpart /dev/vda 1`时，提示`unexpected output in sfdisk --version [sfdisk，来自 util-linux 2.23.2]`。

    **解决方案**：

    1.  运行`locale`命令查看ECS实例的字符编码类型，将非en\_US.UTF-8的字符编码类型切换成en\_US.UTF-8。
        1.  运行以下命令，切换字符编码类型。

            ```
            LANG=en_US.UTF-8
            ```

        2.  如果问题仍未解决，运行以下命令，切换字符编码类型。

            ```
            export LC_ALL=en_US.UTF-8
            ```

        3.  如果问题仍未解决，运行以下命令，切换字符编码类型。

            ```
            localectl set-locale LANG=en_US.UTF-8
            ```

        4.  如果采用以上方案无法解决问题时，运行以下命令，切换字符编码类型。

            ```
            export LANGUAGE=en_US.UTF-8
            ```

    2.  如果问题仍未解决，请您尝试运行`reboot`命令重启ECS实例。
    **说明：**

    当您通过切换字符编码，成功完成扩容分区后，建议您按需切回原有字符编码。

-   **问题**：运行`growpart /dev/vda 1`时，提示`-bash: growpart: command not found`。

    **解决方案**：

    1.  运行`uname -a`检查Linux内核的版本。本文操作适用于Linux内核版本3.6.0及以上的系统。

        如果Linux内核低于3.6.0版本，扩容分区操作请参见[扩展低内核版本实例的系统盘分区和文件系统](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux系统盘.md)和[扩展分区和文件系统\_Linux数据盘](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.md)。

    2.  安装growpart工具。
        -   CentOS 7及以上版本运行以下命令。

            ```
            yum install -y cloud-utils-growpart
            ```

        -   Debian 9及以上版本、Ubuntu14及以上版本运行以下命令。

            ```
            apt install -y cloud-guest-utils
            ```

-   **问题**：为什么在CentOS 6.5中不能安装growpart进行扩容分区？

    **解决方案**：CentOS 6操作系统的Linux内核低于3.6.0版本，如果您需要在CentOS 6中使用growpart，请参考以下步骤：

    1.  在CentOS 6中切换yum源。具体操作，请参见[CentOS 6 EOL如何切换源](/cn.zh-CN/镜像/常见问题/CentOS 6 EOL如何切换源.md)。

        **说明：** CentOS 6操作系统版本已结束生命周期（EOL），如果您需要使用yum安装软件包，需要先切换yum源。

    2.  在CentOS 6中安装dracut-modules-growroot并扩容云盘分区。具体操作，请参见[扩展低内核版本实例的系统盘分区和文件系统](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux系统盘.md)。

## 其他扩容场景

-   如果数据盘需要使用新扩容容量创建新的分区，请参见[选项二：新增并格式化MBR分区](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.mdsection_gg7_ilv_h3j)或[选项四：新增并格式化GPT分区](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.mdsection_4hl_5l7_87s)。
-   如果数据盘没有创建分区，并且在裸设备上创建了文件系统，请参见[选项五：扩容裸设备文件系统](/cn.zh-CN/最佳实践/块存储/扩展分区和文件系统_Linux数据盘.mdsection_f88_ax7_y8i)。

**相关文档**  


[扩容云盘常见问题]()

[RebootInstance](/cn.zh-CN/API参考/实例/RebootInstance.md)

[ResizeDisk](/cn.zh-CN/API参考/块存储/ResizeDisk.md)

[AttachDisk](/cn.zh-CN/API参考/块存储/AttachDisk.md)

