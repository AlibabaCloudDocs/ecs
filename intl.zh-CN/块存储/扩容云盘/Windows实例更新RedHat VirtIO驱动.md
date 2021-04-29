---
keyword: [阿里云, ecs, 磁盘扩容, 扩容, windows扩容]
---

# Windows实例更新RedHat VirtIO驱动

阿里云的Windows实例支持对云盘在线扩容（即无需重启ECS实例便可以完成扩容云盘）和从操作系统内部获取磁盘序列号。如果您的Windows实例有在线扩容（实例创建时间早于2019年3月30日）或者获取磁盘序列号（实例创建时间早于2020年5月1日）需求，请根据本文描述检查是否需要更新RedHat VirtIO驱动。

-   驱动仅支持Windows Server 2008及更高版本操作系统。
-   如果ECS实例的数据盘数量较多，可能需要1~2分钟完成驱动的更新。

## 操作步骤

Windows实例更新RedHat VirtIO驱动的操作步骤如下。

1.  [步骤一：检查驱动版本](#section_mhl_nhy_dhb)
2.  [步骤二：下载驱动程序](#section_93w_k6h_jgz)
3.  [步骤三：更新RedHat VirtIO驱动](#section_pvf_cr1_qgb)

## 步骤一：检查驱动版本

检查驱动版本有以下两种方式。

-   方式一：使用PowerShell检查驱动版本
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/在本地客户端上连接Windows实例.md)。
    2.  打开CMD命令行窗口。
    3.  输入powershell进入PowerShell交互界面。
    4.  输入以下命令检查驱动版本，根据返回信息判断ECS实例是否支持在线扩容。

        ```
        [System.Diagnostics.FileVersionInfo]::GetVersionInfo("C:\Windows\System32\drivers\viostor.sys")
        ```

        ![检查驱动版本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5563359951/p41813.png)

-   方式二：手动检查驱动版本
    1.  远程连接Windows实例。
    2.  进入系统目录C:\\Windows\\System32\\drivers。
    3.  右键单击viostor.sys文件，选择**属性**，在**详细信息**页签下查看文件版本号 。

        ![文件版本号](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5563359951/p41818.png)


根据查询结果，判断是否符合文件版本的要求，并执行不同操作。

|适用场景|Red Hat VirtIO SCSI driver版本|操作|
|----|----------------------------|--|
|在线扩容云盘|大于等于58011|您可以直接在线扩容云盘。具体操作，请参见[在线扩容云盘（Windows系统）](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Windows系统）.md)。|
|小于58011|请继续下一步。|
|查询序列号|大于等于58015|您可以直接查看磁盘序列号。具体操作，请参见[查看磁盘序列号](/intl.zh-CN/块存储/云盘/查看磁盘序列号.md)。|
|小于58015|请继续下一步。|

## 步骤二：下载驱动程序

下载并解压安装包（[virtio驱动包](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/169523/cn_zh/1590721781509/virtio_58015.zip)），本文后续步骤假设您解压后驱动包所在路径为C:\\Users\\Administrator\\Desktop\\virtioDriver。ECS实例的操作系统与解压后文件夹目录的对应关系如下表所示。

|驱动文件（夹）名称|文件（夹）描述|
|:--------|:------|
|win7|Windows Server 2008 R2和Windows 7|
|Wlh|Windows Server 2008|
|Win8|Windows Server 2012和Windows Server 2012 R2|
|win10|Windows 10、Windows Server 2016、Windows Server 2019及更新版本的Windows Server系统|
|amd64|64位|
|x86|32位|

## 步骤三：更新RedHat VirtIO驱动

更新RedHat VirtIO驱动有以下两种方式。

-   方式一：使用pnputil添加和安装驱动
    1.  打开CMD命令行窗口。
    2.  运行以下命令添加驱动包。

        ```
        pnputil -i -a <path to virtio driver inf\>
        ```

        请确保您已经将目标.inf文件解压到指定的目录（<path to virtio driver inf\>中，例如C:\\Users\\Administrator\\Desktop\\virtioDriver\\win7\\amd64\\viostor.inf）。

        -   只更新云盘驱动，则运行：

            ```
            pnputil -i -a C:\Users\Administrator\Desktop\virtioDriver\win7\amd64\viostor.inf
            ```

        -   更新所有RedHat VirtIO相关驱动，则运行：

            ```
            pnputil -i -a C:\Users\Administrator\Desktop\virtioDriver\win7\amd64\*.inf
            ```

    3.  重启ECS实例的操作系统，使驱动更新生效。
-   方式二：手动添加驱动
    1.  打开设备管理器。
    2.  右键单击**存储控制器**下的**Red Hat VirtIO SCSI controller**，并选择**更新驱动程序软件**。

        **说明：** 如果出现多个**Red Hat VirtIO SCSI controller**，只需更新其中一个即可。

        ![更新驱动](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5563359951/p41810.png)

    3.  选择**浏览计算机以查找驱动程序软件**。
    4.  选择**从计算机的设备驱动程序列表中选择**。
    5.  单击**从磁盘安装**。
    6.  选择对应文件夹下的驱动文件viostor，并按向导提示更新驱动。
    7.  重启ECS实例的操作系统，使得驱动更新生效。

-   如果需要在线扩容云盘，请参见[在线扩容云盘](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)。
-   如果需要查询磁盘序列号，请参见[查看磁盘序列号](/intl.zh-CN/块存储/云盘/查看磁盘序列号.md)。

