---
keyword: [Windows Server, Semi-Annual Channel, manage instances, ECS, Alibaba Cloud]
---

# Manage Windows Server Semi-Annual Channel images and instances

This topic describes how to manage an ECS instance that is created from a Windows Server Semi-Annual Channel image.

Windows Server Semi-Annual Channel runs in Server Core mode and is entirely command-line based. Windows Server Semi-Annual Channel offers some significant advantages, such as support for remote management, lower requirements for hardware, and a reduction in the need for updates. Windows Server Semi-Annual Channel instances exclude Resource Manager, Control Panel, and Windows Explorer. These instances do not support the \\\*.msc command line option such as devmgmt.msc. You can manage these instances by using tools such as Sconfig, Server Manager, PowerShell, and Windows Admin Center.

When you create an instance, you can view the following Windows Server Semi-Annual Channel images in the public images list:

-   Windows Server Version 1809 Datacenter Edition
-   Windows Server Version 1709 Datacenter Edition
-   Windows Server Version 1903 Datacenter Edition
-   Windows Server Version 1909 Datacenter Edition
-   Windows Server Version 2004 Datacenter Edition

Windows Server Semi-Annual Channel runs in Server Core mode. We recommend that you use advanced management tools such as PowerShell and Windows Admin Center. For more information, visit [Manage a Server Core server](https://docs.microsoft.com/en-us/windows-server/administration/server-core/server-core-manage) in Microsoft Docs.

## Manage an instance by using PowerShell

PowerShell runs on.NET Framework and uses object-oriented scripts. This allows you to manage Windows instances in the same manner as you would by using SSH. For example, if the public IP address of your instance is 172.16.1XX.183, you can perform the following steps to manage your instance by using PowerShell:

1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).

2.  Enter PowerShell on the command line to start PowerShell.

3.  Run the following commands in PowerShell of the instance:

    ```
    Enable-PSRemoting -Force
    Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
    ```

4.  Add rules to a security group to which the instance belongs to allow access over HTTP port 5985 and HTTPS port 5986. For more information about how to add rules to a security group, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

5.  Enter PowerShell on the command line of the on-premises computer to start PowerShell.

6.  Run the following command in PowerShell of the on-premises computer:

    ```
    Set-Item WSMan:localhost\client\trustedhosts -value 172.16.1XX.183 -Force
    ```

    **Note:** `172.16.1XX.183` indicates that only your instance is trusted. You can use `*` to indicate that all PCs are trusted.

7.  Run `Enter-PSSession '172.16.1XX.183' -Credential:'administrator'` in PowerShell and enter the password of the instance as prompted.


Now you can manage your Windows instances on the on-premises computer.

## Install Windows Admin Center

Windows Admin Center is a browser-based GUI management tool. It can replace server management tools or Microsoft Management Console \(MMC\) when the Server Core mode is used. For example, if the public IP address of your instance is 172.16.1XX.183, you can use one of the following methods to install Windows Admin Center:

-   Use commands
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).
    2.  Add rules to a security group to which the instance belongs to allow access over HTTP port 5985 and HTTPS port 5986. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
    3.  Enter PowerShell on the command line to start PowerShell.
    4.  Run the following commands in PowerShell of the instance:

        ```
        Enable-PSRemoting -Force
        Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-PUBLIC" -RemoteAddress Any
        ```

    5.  Run the following commands to download Windows Admin Center:

        ```
        wget -Uri http://download.microsoft.com/download/E/8/A/E8A26016-25A4-49EE-8200-E4BCBF292C4A/HonoluluTechnicalPreview1802.msi -UseBasicParsing -OutFile c:\HonoluluTechnicalPreview1802.msi
        msiexec /i c:\HonoluluTechnicalPreview1802.msi /qn /L*v log.txt SME_PORT=443 SSL_CERTIFICATE_OPTION=generate
        ```

    6.  Run the cat log.txt command to check the download progress.

        When information similar to the following content is displayed in the log file, Windows Admin Center is installed:

        ```
        MSI (s) (14:44) [09:48:37:885]: Product: Project 'Honolulu'(Technical Preview) -- Installation completed successfully. 
        MSI (s) (14:44) [09:48:37:885]: Product installed by Windows Installer. Product name: Project 'Honolulu' (Technical Preview). Product version: 1.1.10326.0. Product language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.
        ```

-   Use a browser

    -   Prerequisites

        PowerShell is configured and can be used to manage instances. If you want to install Windows Admin Center by using a browser, you must complete the installation on the on-premises computer. For more information, see the [Manage an instance by using PowerShell](#section_et5_g14_hhb) section.

    -   Procedure
        1.  Click [here](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center) to download Windows Admin Center and install it.
        2.  Open [https://localhost/](https://localhost/?spm=a2c4g.11186623.2.32.3da666b5wlBkBq) after you install Windows Admin Center.
        3.  Click **Add**. In the dialog box that appears, add the IP address of the instance.
    Now you can use Windows Admin Center to manage instances in Microsoft Edge or Chrome.


## FAQ

Question 1: How do I copy files to a Windows Server Semi-Annual Channel instance?

If the files to be copied are stored on your on-premises computer, and Windows Admin Center is installed, or PowerShell is configured to manage instances, you can copy files to the instance by using one of the following methods:

-   Use a Remote Desktop \(RDP\) application
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).
    2.  Copy the files from the on-premises computer.
    3.  Enter notepad on the command line of the instance.
    4.  Choose **File** \> **Open**. In the dialog box that appears, right-click the destination directory and select **Paste**.
-   Use PowerShell
    1.  Start the Windows instance.
    2.  Enter PowerShell on the command line of the on-premises computer to start PowerShell.
    3.  Use PowerShell to manage the instance. For more information, see the [Manage an instance by using PowerShell](#section_et5_g14_hhb) section.
    4.  Run the following commands on the on-premises computer:

        ```
        $session = New-PSSession -ComputerName 172.16.1XX.183
        Copy-Item -ToSession $session -Path C:\1.txt -Destination c:\2.txt
        ```

        **Note:** C:\\1.txt is the source file directory on the on-premises computer. C:\\2.txt is the destination file directory on the Windows instance.

-   Use Windows Admin Center
    1.  Start the Windows instance.
    2.  Configure Windows Admin Center. For more information, see the [Install Windows Admin Center](#section_y2t_3d4_hhb) section.
    3.  Start Windows Admin Center and click the Windows instance. Click **File**, select the file, and then click **Upload**.

Question 2: How do I stop or restart a Windows Server Semi-Annual Channel instance from inside?

-   Use an RDP application
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).
    2.  Enter sconfig on the command line, select `13` to restart the instance or `14` to stop the instance, and then press the Enter key.
-   Use PowerShell
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).
    2.  Enter PowerShell on the command line to start PowerShell.
    3.  Run one of the following commands to restart or stop the instance:

        ```
        shutdown -r -t 00 :: Restart the instance in 0 seconds by using the command line.
        shutdown -s -t 00 :: Stop the instance in 0 seconds by using the command line.
        Stop-Computer -Force # Stop the instance instantly by using PowerShell.
        Restart-Computer -Force # Restart the instance instantly by using PowerShell.
        ```

-   Use PowerShell
    1.  Start the Windows instance.
    2.  Enter PowerShell on the command line of the on-premises computer to start PowerShell.
    3.  Use PowerShell to manage the instance. For more information, see the [Manage an instance by using PowerShell](#section_et5_g14_hhb) section.
    4.  Run the following commands to restart or stop the instance:

        ```
        Enter-PsSession -ComputerName 172.16.1XX.183
        Restart-Computer -Force # Restart the instance.
        Stop-Computer -Force # Stop the instance.
        ```

-   Use Windows Admin Center
    1.  Start the Windows instance.
    2.  Configure Windows Admin Center. For more information, see the [Install Windows Admin Center](#section_y2t_3d4_hhb) section.
    3.  Start Windows Admin Center and select the Windows instance. In the left-side navigation pane, click **Overview**. On the Overview page, click **Restart** or **Shutdown**.

Question 3: How do I install the IIS service?

-   Use an RDP application
    1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).
    2.  Enter PowerShell on the command line to start PowerShell.
    3.  Run the following commands to install IIS:

        ```
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   Use PowerShell
    1.  Start the Windows instance.
    2.  Enter PowerShell on the command line of the on-premises computer to start PowerShell.
    3.  Use PowerShell to manage the Windows instance. For more information, see the [Manage an instance by using PowerShell](#section_et5_g14_hhb) section.
    4.  Run the following PowerShell commands on the on-premises computer:

        ```
        Enter-PsSession -ComputerName 172.16.1XX.183
        Import-Module ServerManager
        Add-WindowsFeature Web-Server, Web-CGI, Web-Mgmt-Console
        ```

-   Use Windows Admin Center
    1.  Start the Windows instance.
    2.  Configure Windows Admin Center. For more information, see the [Install Windows Admin Center](#section_y2t_3d4_hhb) section.
    3.  Start Windows Admin Center and select the Windows instance. In the left-side navigation pane, click **Roles & Features**. On the Roles & Features page, click **Web Server**. Select the suitable features based on your needs and click **Yes**.

Question 4: How do I reopen a command line window that I accidentally closed during an RDP session?

If a command line window is accidentally closed during an RDP session, the remote application shows a black screen and operations cannot be performed. In this case, you can perform the following steps:

1.  Press Ctrl+Alt+End if an MSTSC connection is used. In other cases, press Ctrl+Alt+Del.
2.  Select **Task Manager** and press the Enter key.
3.  In Task Manager, choose **File** \> **Run new task**. Enter cmd and click **OK**.

**References**  


[Windows Server servicing channels: LTSC and SAC](https://docs.microsoft.com/zh-cn/windows-server/get-started/semi-annual-channel-overview)

[Introducing Windows Server, version 1709](https://docs.microsoft.com/en-us/windows-server/get-started/get-started-with-1709?spm=a2c4g.11186623.2.54.3da666b5wlBkBq)

[Windows Admin Center](https://docs.microsoft.com/en-us/windows-server/manage/honolulu/honolulu?spm=a2c4g.11186623.2.55.3da666b5wlBkBq)

[About Remote Troubleshooting](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_troubleshooting?spm=a2c4g.11186623.2.56.3da666b5wlBkBq&view=powershell-6)

