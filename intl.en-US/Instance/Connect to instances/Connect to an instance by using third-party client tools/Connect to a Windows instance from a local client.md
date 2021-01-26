# Connect to a Windows instance from a local client

This topic describes how to connect to a Windows instance from a local client.

Before you connect to a Windows instance, make sure that the following requirements are met:

-   The instance is in the **Running** state. If not, you must start it. For more information, see [Start or stop an instance](/intl.en-US/Instance/Manage instances/Start ECS instances.md).
-   A logon password is set for the instance. If you have not set a password or if you have forgotten the password, you must reset the password for the instance. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).
-   The instance can access the Internet:
    -   In a VPC, a public IP address is assigned to the instance or an elastic IP address \(EIP\) is associated with the instance. For more information, see [Create an IPv4 VPC network](/intl.en-US/Quick Start/Create an IPv4 VPC network.md).
    -   In the classic network, a public IP address is assigned to the instance by using one of the following methods:
        -   If you select Assign Public IP Address when you create a subscription or pay-as-you-go instance, a public IP address is assigned to the instance.
        -   If you do not select Assign Public IP Address when you create a subscription instance, you can upgrade the bandwidth to obtain a public IP address for the instance. For more information, see [Overview of instance upgrade and downgrade](/intl.en-US/Instance/Change configurations/Overview of instance upgrade and downgrade.md).
-   The following security group rules are added to the security group to which the instance belongs. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Network type|NIC type|Rule direction|Action|Protocol|Port range|Authorization type|Authorization object|Priority|
    |------------|--------|--------------|------|--------|----------|------------------|--------------------|--------|
    |VPC|N/A|Inbound|Allow|RDP\(3389\)|3389/3389|CIDR block|0.0.0.0/0|1|
    |Classic network|Internet|


## Procedure

You can connect to a Windows instance by using different remote connection software based on the operating system of your local client:

-   [Connect from a local client that runs a Windows operating system](#windows)
-   [Connect from a local client that runs a Linux operating system](#linux)
-   [Connect from a local client that runs a Mac operating system](#macOS1)
-   [Connect from a local client that runs an Android or iOS operating system](#mobile)

## Connect from a local client that runs a Windows operating system

If the local client runs a Windows operating system, you can connect to a Windows instance from the local client by using the Microsoft Terminal Services Client \(MSTSC\), which is a component of Microsoft Windows.

1.  Use one of the following methods to start **MSTSC**:

    -   Choose **Start** \> **Windows Accessories** \> **Remote Desktop Connection**.
    -   Click the **Start** icon, enter mstsc in the search box, and then press the Enter key.
    -   Press **Win**+**R** to open the Run dialog box, enter mstsc, and then press the Enter key.
2.  In the Remote Desktop Connection dialog box, perform the following operations in sequence:

    1.  Click **Show Options**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/9622/15510233415258_en-US.png)

    2.  Set Computer to the public IP address or EIP of the instance.

    3.  Set Username. The default username is Administrator.

        If you do not want to manually enter your username and password again when you connect to the instance next time, you can select **Allow me to save credentials**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/9622/15510233415259_en-US.png)

    4.  If you want to copy files from your local client to the instance, you can click the **Local Resources** tab to view options for sharing local computer resources.

        -   If you want to copy text only, select **Clipboard**.
        -   If you want to copy files, click **More**, select Drive, and then select the letters of the drives from which you want to copy files.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/9622/15510233415260_en-US.png)

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/9622/15510233415261_en-US.png)

    5.  If you have specific requirements on the size of the remote desktop window, you can click the **Display** tab to resize the remote desktop window. We recommend that you use Full Screen.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/9622/15510233415262_en-US.png)

    6.  Click **Connect**.


## Connect from a local client that runs a Linux operating system

If the local client runs a Linux operating system, you can connect to a Windows instance from the local client by using a remote connection tool. rdesktop is used in this example.

1.  Download and start rdesktop.

2.  Run the following command to connect to the Windows instance. Change the parameter values based on your own configurations.

    ```
    rdesktop -u administrator -p password -f -g 1024*720 192.168.1.1 -r clipboard:PRIMARYCLIPBOARD -r disk:sunray=/home/yz16184
    ```

    The following table describes the parameters.

    |Parameter|Description|
    |:--------|:----------|
    |-u|The username used to log on to the Windows instance. The default username is Administrator.|
    |-p|The password used to log on to the Windows instance.|
    |-f|The full-screen mode. You can press **Ctrl**+**Alt**+**Enter** to switch the mode.|
    |-g|The screen resolution. An asterisk \(\*\) is used in between the two pixel values. This parameter can be left empty. If this parameter is not specified, the full-screen mode is used.|
    |192.168.1.1|The IP address of the server to connect to. Replace it with the public IP address or EIP of your Windows instance.|
    |-d|The domain name. For example, if the domain name is INC, set the parameter to `-d inc`.|
    |-r|Multimedia redirection. Examples:     -   Turn on the sound: `-r sound`.
    -   Use a local sound card: `-r sound : local`.
    -   Enable USB flash drive: `-r disk:usb=/mnt/usbdevice`. |
    |-r clipboard:PRIMARYCLIPBOARD|Allows text including Chinese to be copied between the local client that runs a Linux operating system and the Windows instance.|
    |-r disk:sunray=/home/yz16184|Maps a directory in the Linux operating system on the local client to a disk in the Windows instance. This way, Samba and FTP are not required for file transfer.|


## Connect from a local client that runs a Mac operating system

For information about how to connect to a Windows instance from a local client that runs a Mac operating system, visit [Get started with the macOS client](https://docs.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/clients/remote-desktop-mac).

## Connect from a local client that runs an Android or iOS operating system

You can use applications to connect to a Windows instance from your mobile device.

For more information, see [Connect to a Windows instance from a mobile device](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Windows instance from a mobile device.md).

