---
keyword: [Windows Server, 半年渠道, 实例管理, ecs, 阿里云]
---

# Windows Server半年渠道镜像与实例管理

云服务器ECS提供Windows Server半年渠道镜像，本文介绍如何管理由该类镜像创建的Windows Server半年渠道实例。

Windows Server半年渠道镜像是一款纯Server Core模式运行的操作系统，不提供图形化用户界面。Windows Server半年渠道镜像对硬件要求宽松许多，降低了更新频率并且支持远程管理。Windows Server半年渠道实例不再包含资源管理器、控制面板、Windows Explorer，不支持\*.msc功能（如devmgmt.msc等）。Windows Server半年渠道实例支持使用Sconfig、Server Manager、PowerShell和Windows Admin Center等工具管理服务器。

创建实例时，您可以在公共镜像列表中看到Windows Server半年渠道镜像，包括：

-   Windows Server Version 1809 数据中心版
-   Windows Server Version 1709 数据中心版
-   Windows Server Version 1903 数据中心版
-   Windows Server Version 1909 数据中心版
-   Windows Server Version 2004 数据中心版

由于Windows Server半年渠道实例使用Server Core模式，本文推荐您使用功能更为完善的PowerShell和Windows Admin Center。更多详情，请参见微软文档[如何管理 Server Core 模式服务器](https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-manage)。

## 远程管理PowerShell

PowerShell依赖于.NET Framework实现了强大的面向对象的脚本，可以做到SSH功能一样远程管理Windows实例。我们假设您的实例公网IP为172.16.1XX.183，您可以按以下步骤实现PowerShell远程管理。

1.  远程连接Windows实例。具体操作，请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。

2.  在命令行里输入PowerShell打开PowerShell。

3.  在实例PowerShell中运行以下命令。

    ```
    Enable-PSRemoting -Force
    Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
    ```

4.  在实例所在安全组中添加规则放行HTTP 5985端口和HTTPS 5986端口。添加安全组规则的具体操作，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

5.  在客户端计算机命令行里输入PowerShell打开PowerShell。

6.  在客户端PowerShell中运行以下命令。

    ```
    Set-Item WSMan:localhost\client\trustedhosts -value 172.16.1XX.183 -Force
    ```

    **说明：** `172.16.1XX.183`代表只授信您的实例，您也可以使用`*`表示授信所有计算机。

7.  在客户端PowerShell中运行`Enter-PSSession '172.16.1XX.183' -Credential:'administrator'`并按提示输入实例密码。


现在您可以在客户端计算机管理您的Windows实例了。

## 安装Windows Admin Center

Windows Admin Center是一个基于浏览器的图形管理工具，可以在Server Core运行环境中取代服务器管理和MMC。我们假设您的实例公网IP为172.16.1XX.183，您可以按以下任一方法安装Windows Admin Center。

-   通过命令行安装Windows Admin Center
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。
    2.  在实例所在安全组中添加规则放行HTTP 5985端口和HTTPS 5986端口。详情请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。
    3.  在命令行里输入PowerShell打开PowerShell。
    4.  在实例PowerShell中运行以下命令。

        ```
        Enable-PSRemoting -Force
        Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
        ```

    5.  运行以下命令下载Windows Admin Center。

        ```
        wget -Uri http://download.microsoft.com/download/E/8/A/E8A26016-25A4-49EE-8200-E4BCBF292C4A/HonoluluTechnicalPreview1802.msi -UseBasicParsing -OutFile c:\HonoluluTechnicalPreview1802.msi
        msiexec /i c:\HonoluluTechnicalPreview1802.msi /qn /L*v log.txt SME_PORT=443 SSL_CERTIFICATE_OPTION=generate
        ```

    6.  运行cat log.txt命令查看下载进度。

        当日志文件出现下列信息，说明Windows Admin Center已经成功安装。

        ```
        MSI (s) (14:44) [09:48:37:885]: Product: Project 'Honolulu'(技术预览版) -- Installation completed successfully. 
        MSI (s) (14:44) [09:48:37:885]: Windows Installer 已安装产品。产品名称: Project 'Honolulu'(技术预览版)。产品版本: 1.1.10326.0。产品语言: 1033。制造商: Microsoft Corporation。安装成功或错误状态: 0。
        ```

-   通过浏览器安装Windows Admin Center

    -   前提条件

        通过浏览器安装Windows Admin Center需要在客户端计算机中完成，请确保您已经通过配置PowerShell管理实例。更多详情，请参见[PowerShell 远程管理](#section_et5_g14_hhb)。

    -   操作步骤
        1.  [下载](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)并安装Windows Admin Center。
        2.  完成安装后，打开[https://localhost/](https://localhost/?spm=a2c4g.11186623.2.32.3da666b5wlBkBq)。
        3.  单击**添加**，在弹窗中添加实例的IP地址。
    现在，您可以通过Microsoft Edge或者Chrome使用Windows Admin Center管理实例。


## 常见问题

问题一：如何复制文件到Windows Server半年渠道实例？

假设需要复制的文件在您的客户端计算机上，并且您已经配置了PowerShell远程管理或者已安装Windows Admin Center。

-   通过RDP应用
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。
    2.  在客户端计算机上，复制目标文件。
    3.  在实例CMD环境中输入notepad。
    4.  单击**文件** \> **打开**，在打开对话框里，选择文件要复制的目标目录，右键单击选择**粘贴**。
-   通过PowerShell远程
    1.  启动目标Windows实例。
    2.  在客户端计算机上打开CMD，输入PowerShell进入PowerShell。
    3.  通过PowerShell远程管理目标实例。详情请参见[远程管理PowerShell](#section_et5_g14_hhb)。
    4.  在客户端计算机上运行以下命令。

        ```
        $session = New-PSSession -ComputerName 172.16.1XX.183
        Copy-Item -ToSession $session -Path C:\1.txt -Destination c:\2.txt
        ```

        **说明：** C:\\1.txt是客户端计算机的文件位置，C:\\2.txt是要拷贝到的Windows实例目录。

-   通过Windows Admin Center
    1.  启动目标Windows 实例。
    2.  配置Windows Admin Center工具。详情请参见[安装Windows Admin Center](#section_y2t_3d4_hhb)。
    3.  打开Windows Admin Center，选择被管理的实例，单击**文件**，选中文件后单击**上传**。

问题二：如何从内部关闭或者重启Windows Server半年渠道实例？

-   通过RDP应用
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。
    2.  在CMD中输入sconfig，根据需要选择`13`重启实例或者`14`停止实例并回车。
-   通过PowerShell
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。
    2.  在CMD中输入PowerShell进入PowerShell。
    3.  选择并输入以下命令行重启或者停止实例。

        ```
        shutdown -r -t 00 ::命令行 在0秒后重启
        shutdown -s -t 00 ::命令行 在0秒后关机
        Stop-Computer -Force # Powershell 立即关机
        Restart-Computer -Force # Powershell 立即重启
        ```

-   通过PowerShell远程管理
    1.  启动目标 Windows 实例。
    2.  在客户端计算机上打开CMD，输入PowerShell进入PowerShell。
    3.  通过PowerShell远程管理目标实例。详情请参见[远程管理PowerShell](#section_et5_g14_hhb)。
    4.  在客户端计算机上选择性运行以下PowerShell命令。

        ```
        Enter-PsSession –ComputerName 172.16.1XX.183
        Restart-Computer -Force #重启
        Stop-Computer -Force #关机
        ```

-   通过Windows Admin Center
    1.  启动目标Windows实例。
    2.  配置Windows Admin Center工具。详情请参见[安装Windows Admin Center](#section_y2t_3d4_hhb)。
    3.  打开Windows Admin Center，选择被管理的实例，单击**概述**，选择性单击**重启**或者**关机**。

问题三：如何安装IIS服务？

-   通过RDP应用
    1.  远程连接Windows实例。详情请参见[在本地客户端上连接Windows实例](/intl.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md)。
    2.  在CMD中输入PowerShell进入PowerShell。
    3.  运行以下命令安装IIS。

        ```
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   通过PowerShell远程管理
    1.  启动目标 Windows 实例。
    2.  在客户端计算机上打开CMD，输入PowerShell进入 PowerShell。
    3.  通过PowerShell远程管理目标实例，详情请参见[远程管理PowerShell](#section_et5_g14_hhb)。
    4.  在客户端计算机上运行以下PowerShell命令。

        ```
        Enter-PsSession –ComputerName 172.16.1XX.183
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   通过Windows Admin Center
    1.  启动目标Windows实例。
    2.  配置Windows Admin Center工具，详情请参见[安装Windows Admin Center](#section_y2t_3d4_hhb)。
    3.  打开Windows Admin Center，选中被管理的实例，单击**角色和功能**，单击**Web 服务器**，选择您需要的功能后单击**是**。

问题四：如何重新建立不小心在RDP会话中关闭了的命令行窗口？

如果在远程会话中不小心关闭了命令行窗口，远程应用将变成纯黑界面，无法操作。这时您可以：

1.  通过mstsc连接的情况下按Ctrl + Alt + End组合键，其他情况按Ctrl + Alt + Del组合键。
2.  在出现的界面选择**任务管理器**并回车。
3.  在任务管理器中，依次单击**文件** \> **新建任务**文件，输入cmd后单击**确定**。

**相关文档**  


[Windows Server 半年渠道概述](https://docs.microsoft.com/zh-cn/windows-server/get-started/semi-annual-channel-overview)

[Introducing Windows Server, version 1709](https://docs.microsoft.com/en-us/windows-server/get-started/get-started-with-1709?spm=a2c4g.11186623.2.54.3da666b5wlBkBq)

[Windows Admin Center](https://docs.microsoft.com/en-us/windows-server/manage/honolulu/honolulu?spm=a2c4g.11186623.2.55.3da666b5wlBkBq)

[About Remote Troubleshooting](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_troubleshooting?spm=a2c4g.11186623.2.56.3da666b5wlBkBq&view=powershell-6)

