---
keyword: [Alibaba Cloud, ECS, time calibration, time zone]
---

# Configure the NTP service for Windows instances

This topic describes how to enable and configure the NTP service for a Windows instance to ensure that the local system time is precisely synchronized.

By default, ECS instances in all Alibaba Cloud regions use UTC+8. You can configure or change time zones for your instances.

Windows Server 2012 R2 Datacenter Edition 64-bit is used in this topic to demonstrate how to use the NTP service to synchronize the local system time for Windows instances.

## Enable the NTP service

By default, the Windows Time service is enabled on Windows Server operating systems. The NTP service must be enabled for Windows instances to synchronize the local system time. Perform the following operations to check and enable the NTP service:

1.  Connect to the Windows ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Click the ![Start](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4529276061/p179485.png) icon and open the **Run** dialog box. Run the `services.msc` command in the Run dialog box.

3.  In the Services dialog box, find and double-click **Windows Time**.

4.  In the Windows Time Properties \(Local Computer\) dialog box, perform the following operations:

    1.  Set **Startup type** to **Automatic**.

    2.  Make sure that the value of **Service status** is **Running**. Otherwise, click **Start**.

    3.  Click **Apply** and then click **OK**.


## Modify the default NTP server address

By default, Windows Server operating systems use the Microsoft NTP server \(time.windows.com\), but errors may occur while the operating systems are synchronizing with the Microsoft NTP server. When you use a Windows instance, you can replace the default NTP server with an internal NTP server provided by Alibaba Cloud. Perform the following operations to modify the default NTP server address:

1.  Connect to the Windows ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  In the notification area of the taskbar, click the date and time, and then click **Change date and time settings**.

3.  In the Date and Time dialog box, click the **Internet Time** tab and then click **Change settings**.

4.  In the Internet Time Settings dialog box, select **Synchronize with an Internet time server**, enter the address of an Alibaba Cloud internal NTP server, and then click **Update now**. For more information, see [Alibaba Cloud NTP server](/intl.en-US/Instance/Manage instances/Configure time/Alibaba Cloud NTP server.md).


## Modify the NTP synchronization interval

The default NTP synchronization interval is five minutes. You can modify the interval. Perform the following operations to modify the NTP synchronization interval:

1.  Connect to the Windows ECS instance. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Click the ![Start](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4529276061/p179485.png) icon and open the **Run** dialog box. Run the `regedit` command in the Run dialog box.

3.  In the left-side navigation pane of Registry Editor, choose **HKEY\_LOCAL\_MACHINE** \> **SYSTEM** \> **CurrentControlSet** \> **Services** \> **W32Time** \> **TimeProviders** \> **NtpClient** and double-click **SpecialPollInterval**.

4.  In the Edit DWORD \(32-bit\) Value dialog box, select **Decimal** in the **Base** section and enter a value in the **Value data** field. The entered value is the new synchronization interval. Unit: seconds.

5.  Click **OK**.

6.  Restart the instance for the changes to take effect.

    You can restart the instance for the changes to take effect. If you cannot restart the instance due to business requirements, you can restart the NTP service for the changes to take effect. Perform the following operations:

    1.  Click the ![Start](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4529276061/p179485.png) icon and open the **Run** dialog box. Run the `services.msc` command in the Run dialog box.

    2.  In the Services dialog box, find and double-click **Windows Time**.

    3.  In the Windows Time Properties \(Local Computer\) dialog box, click **Stop**.

    4.  Click **Start** after the service enters the **Stopped** state.

    5.  Click **OK**.


**Related topics**  


[Alibaba Cloud NTP server](/intl.en-US/Instance/Manage instances/Configure time/Alibaba Cloud NTP server.md)

[Time setting: Synchronize NTP servers and change time zone for Linux instances](/intl.en-US/Instance/Manage instances/Configure time/Time setting: Synchronize NTP servers and change time zone for Linux instances.md)

[Configure chrony for Linux instances \(CentOS 7\)](/intl.en-US/Instance/Manage instances/Configure time/Configure chrony for Linux instances (CentOS 7).md)

[Configure chrony for Linux instances \(Alibaba Cloud Linux 2\)](/intl.en-US/Instance/Manage instances/Configure time/Configure chrony for Linux instances (Alibaba Cloud Linux 2).md)

