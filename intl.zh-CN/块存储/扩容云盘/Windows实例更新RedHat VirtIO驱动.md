---
keyword: [VirtIO驱动, 扩容, windows扩容, 查询序列号]
---

# Windows实例更新RedHat VirtIO驱动

阿里云的Windows实例支持对云盘在线扩容（即无需重启ECS实例便可以完成扩容云盘）和从操作系统内部获取磁盘序列号。如果您的Windows实例有在线扩容（实例创建时间早于2019年3月30日）或者获取磁盘序列号（实例创建时间早于2020年5月1日）需求，请根据本文描述检查是否需要更新RedHat VirtIO驱动。

-   驱动仅支持Windows Server 2008及更高版本操作系统。
-   如果ECS实例的数据盘数量较多，可能需要1~2分钟完成驱动的更新。

## 操作步骤

Windows实例更新RedHat VirtIO驱动的操作步骤如下。

1.  [步骤一：检查驱动版本](#section_mhl_nhy_dhb)
2.  [步骤二：更新驱动程序](#section_93w_k6h_jgz)

## 步骤一：检查驱动版本

检查驱动版本有以下两种方式。

-   方式一：使用PowerShell检查驱动版本
    1.  远程连接Windows实例。详情请参见[通过密码认证登录Windows实例](/intl.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/在本地客户端上连接Windows实例.md)。
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

## 步骤二：更新驱动程序

如果您的Windows实例能够访问公网，建议您使用本小节中的步骤快速更新virtio驱动。如果实例不能访问公网，或需要批量更新virtio驱动，请参见[如何手动更新Windows实例的virtio驱动](/intl.zh-CN/镜像/常见问题/如何手动更新Windows实例的virtio驱动.md)中的步骤。

您在手动更新virtio驱动前，建议您先为Windows实例创建快照备份数据。具体操作，请参见[创建一个云盘快照](/intl.zh-CN/快照/使用快照/创建一个云盘快照.md)。

1.  远程连接待更新驱动的Windows实例。

    具体操作，请参见[连接方式介绍](/intl.zh-CN/实例/连接实例/连接方式概述.md)。

2.  在Windows实例中，下载用于更新virtio驱动的脚本。

    下载地址：[InstallVirtIo.ps1](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/InstallVirtIo.ps1)

3.  执行InstallVirtIo.ps1脚本更新virtio驱动。

    例如，您将脚本InstallVirtIo.ps1下载到了C:\\test目录下。

    1.  打开C:\\test文件夹。

        您需要打开InstallVirtIo.ps1实际的下载目录。

    2.  选中InstallVirtIo.ps1文件，单击鼠标右键，然后单击**使用 PowerShell 运行**。

        ![执行脚本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6902421261/p274473.png)

        您也可以在文件夹的空白区域，按下Shift键的同时，单击鼠标右键，然后单击**在此处打开 Powershell 窗口\(S\)**。在Windows PowerShell中手动执行InstallVirtIo.ps1脚本。

        **说明：** 如果您当前Windows实例的登录用户为普通用户，需要以管理员权限执行脚本。如果是系统用户，则可以直接执行脚本。

4.  脚本执行完成后，重启Windows实例。

    具体操作，请参见[重启实例](/intl.zh-CN/实例/管理实例状态/重启实例.md)。重启实例后，virtio驱动更新才会生效。


-   如果需要在线扩容云盘，请参见[在线扩容云盘](/intl.zh-CN/块存储/扩容云盘/在线扩容云盘（Linux系统）.md)。
-   如果需要查询磁盘序列号，请参见[查看磁盘序列号](/intl.zh-CN/块存储/云盘/查看磁盘序列号.md)。
-   更多更新RedHat VirtIO驱动方式，请参见[如何手动更新Windows实例的virtio驱动](/intl.zh-CN/镜像/常见问题/如何手动更新Windows实例的virtio驱动.md)。

