---
keyword: zombie
---

# Connect to a Windows instance by using password authentication

If you cannot use remote connection software such as RDP and rdesktop to connect to a Windows instance, you can use the **VNC Connection** feature in the console to log on to the instance and view the real-time status of the instance operating interface.

A logon password is set for the instance.

**Note:** If you have not set a password or forget the password, you can reset the password for the instance. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).

The following passwords are involved when you use VNC to connect to an instance:

-   VNC password: the password of management terminals used to connect to the ECS console.
-   Instance logon password: the password used to log on to the instance operating system.

By default, a remote VNC connection session lasts for about 300 seconds. If you do not perform operations within these 300 seconds, the connection to the instance is disconnected. You must connect to the instance again.

If you cannot use remote connection software to connect to your instance, you can use the **VNC Connection** feature in the ECS console to connect to the instance and view the status of the instance. The following table describes the related scenarios.

|Scenario|Solution|
|--------|--------|
|The instance starts slowly due to self-check on startup.|Check the self-check progress.|
|The firewall of the operating system is enabled by mistake.|Disable the firewall.|
|The ECS instance is hacked into, which causes a high CPU utilization and high bandwidth usage.|Troubleshoot and terminate abnormal processes.|

## Procedure

The following figure shows the workflow.

![Procedure](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7413606161/p5162.png)

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

5.  Connect to a VNC management terminal.

    **Note:** The VNC password is used in this step.

    -   For the first time:
        1.  Change the VNC password. For more information, see the [Change the VNC password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md) section.
        2.  In the **Modify VNC Password** dialog box, enter the new password.
        3.  Click **OK**.
    -   For the second or later time:
        1.  In the **Enter VNC Password** dialog box, enter the password.
        2.  Click **OK**.
6.  In the upper-left corner of the **VNC** page, choose **Send Remote Call** \> **CTRL+ALT+DELETE**.

    ![Windows shortcut combination](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9568432161/p171354.png)

7.  Select an account, enter the instance password, and then press the Enter key.

    By default, the Administrator account is available.


## Change the VNC password

When you connect to the VNC management terminal for the first time, you must change the VNC password. You can also change the VNC password when you forget the password or want to update the password.

**Note:** After you change the VNC password for a non-I/O optimized instance, you must restart the instance in the ECS console for the new password to take effect. Before you restart the instance, you must stop it. This can lead to service interruption. Proceed with caution.

1.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

2.  In the **Enter VNC Password** dialog box, click **Modify VNC Password**.

3.  In the **Modify VNC Password** dialog box, enter and confirm the new password, and then click **OK**.

4.  If the instance is a non-I/O optimized instance, restart the instance.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instances/Restart an instance.md).


## Copy long commands

If you want to copy a long-text item such as a download URL from your computer to the instance, you can use the command copy feature.

1.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

2.  Connect to a VNC management terminal.

3.  In the upper-left corner of the interface, click **Enter Copy Commands**.

4.  In the **Copy and Paste Commands** dialog box, enter the content to be copied and click **OK**.


## References

If you want to adjust the resolution of the Windows desktop, see [How do I adjust the desktop resolution of a Windows instance?](/intl.en-US/Instance/Instance FAQ.md).

