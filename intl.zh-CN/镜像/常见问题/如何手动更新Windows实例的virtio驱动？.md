# 如何手动更新Windows实例的virtio驱动？

如果您需要手动更新Windows实例的virtio驱动，可以参考本文介绍的方式完成驱动更新。

您在手动更新virtio驱动前，建议您先为Windows实例创建快照备份数据。具体操作，请参见[创建一个云盘快照](/intl.zh-CN/快照/使用快照/创建一个云盘快照.md)。

您可以根据实际情况，选择以下任一方式手动更新virtio驱动：

-   如果您的Windows实例能够访问公网，建议您使用脚本快速更新。具体操作，请参见[方式一：使用脚本更新驱动](#section_dxx_gk9_ro8)。
-   如果您的Windows实例不具备公网访问能力，建议您上传virtio驱动的压缩包，手动更新驱动。具体操作，请参见[方式二：通过安装包更新驱动](#section_1kb_hov_812)。
-   如果您存在多台ECS实例需要更新virtio驱动，且Windows实例能够访问公网或者专有网络VPC的内网，可以通过阿里云的云助手功能批量更新。具体操作，请参见[方式三：使用云助手批量更新驱动](#section_u8c_blo_x3v)。

**说明：** 更新virtio驱动时，ECS实例的网络会中断10秒左右。您需要注意网络中断所造成的业务影响。

## 方式一：使用脚本更新驱动

如果您的Windows实例能够访问公网，可以通过该方式快速更新virtio驱动。

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


## 方式二：通过安装包更新驱动

如果您的Windows实例不具备公网访问能力，可以通过该方式更新virtio驱动。

1.  在本地主机上，下载阿里云提供的virtio驱动压缩包。

    下载地址：[virtio驱动压缩包](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/210408.1454.1459_bin.zip)

    成功下载后，您可以查看到名为210408.1454.1459\_bin.zip的压缩包。

2.  将210408.1454.1459\_bin.zip上传至Windows实例。

    您可以使用以下任一方式上传文件：

    -   本地操作系统为Windows时，可以使用Windows远程桌面连接工具连接Windows实例，并完成文件的上传。
    -   为Windows实例搭建FTP服务，然后通过FTP客户端将文件上传至Windows实例。更多信息，请参见[手动搭建FTP站点（Windows）](/intl.zh-CN/建站教程/搭建应用/搭建FTP站点/手动搭建FTP站点（Windows）.md)。
3.  在Windows实例中，解压210408.1454.1459\_bin.zip，然后打开210408.1454.1459\_bin文件夹。

    打开文件夹后，您可以查看到不同Windows操作系统版本对应的文件夹。

    ![windows版本](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6902421261/p274528.png)

    各个文件夹中保存不同操作系统适用的驱动。您只需关注以下文件夹：

    -   win10目录中保存的驱动适用于：Windows Server 2016、Windows Server 2019以及Windows 10。
    -   Win8目录中保存的驱动适用于：Windows Server 2012 R2、Windows 8.1。
    -   win7目录中保存的驱动适用于：Windows Server 2008 R2、Windows 7。
    每个文件夹中的驱动按照amd64架构和x86架构区分，amd64架构对应64位操作系统，x86架构对应32位操作系统。

4.  根据Windows实例当前的操作系统版本，选择打开对应的文件夹。

    例如，本示例中Windows实例的操作系统版本为Windows Server 2012 R2 64位，则打开的文件夹路径为C:\\test\\210408.1454.1459\_bin\\Win8\\amd64。

5.  在amd64文件夹内的空白区域，按下Shift键的同时，单击鼠标右键，然后单击**在此处打开 Powershell 窗口\(S\)**。

    ![powershell](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6902421261/p274577.png)

6.  在Windows Powershell中，运行以下命令，安装新版virtio驱动。

    **说明：** 如果您当前Windows实例的登录用户为普通用户，需要以管理员权限运行该命令。如果是系统用户，则可以直接运行该命令。

    ```
    pnputil -i -a *.inf
    ```

    如下图所示，表示virtio驱动安装成功。

    ![执行命令](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6902421261/p274580.png)

7.  重启Windows实例。

    具体操作，请参见[重启实例](/intl.zh-CN/实例/管理实例状态/重启实例.md)。重启实例后，virtio驱动更新才会生效。


## 方式三：使用云助手批量更新驱动

如果您存在多台ECS实例需要更新virtio驱动，且Windows实例能够访问公网或者专有网络VPC的内网，可以通过阿里云的云助手功能批量更新。

**说明：** 通过云助手更新virtio驱动时，需要下载驱动相关的安装包，系统会优先访问VPC内网进行下载，如果VPC内网访问受限导致下载失败，系统再访问公网进行下载。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，选择**运维与监控** \> **发送命令/文件（云助手）**。

3.  在顶部菜单栏，选择地域。

    选择的地域需要与您ECS实例所属的地域保持一致。

4.  在**ECS云助手**页面，单击**创建/执行命令**。

5.  在**创建命令**面板，完成以下配置。

    -   在**命令信息**区域，必填参数说明如下表所示，其它参数保持默认值即可。

        |参数|说明|
        |--|--|
        |**命令来源**|单击**输入命令内容**。|
        |**命令名称**|自定义名称或保持默认名称。|
        |**执行计划**|单击**立即执行**。|
        |**命令类型**|单击**PowerShell**。|
        |**命令内容**|以下任一方式均可完成virtio驱动的更新：        -   通过InstallVirtIo.ps1脚本更新virtio驱动。

您需要在本地主机下载[InstallVirtIo.ps1](https://windows-driver-cn-beijing.oss-cn-beijing.aliyuncs.com/virtio/InstallVirtIo.ps1)脚本，然后将脚本的内容完整复制到云助手的命令内容中。

        -   通过云助手插件更新virtio驱动。

将以下命令复制到云助手的命令内容中。

            ```
acs-plugin-manager.exe --exec --plugin=UpdateVirtIo
            ``` |

    -   在**选择实例**区域，选中需要更新驱动的实例ID。
6.  单击**执行**。

    您可以在**命令执行结果**页签查看命令的执行结果。具体操作，请参见[控制台查看执行结果](/intl.zh-CN/运维与监控/云助手/使用云助手/查看执行结果及修复常见问题.md)。如下图所示，表示多台ECS实例的其中一台实例成功更新virtio驱动。

    ![执行结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6902421261/p274637.png)

7.  批量重启多台Windows实例。

    具体操作，请参见[重启实例](/intl.zh-CN/实例/管理实例状态/重启实例.md)。重启实例后，virtio驱动更新才会生效。


