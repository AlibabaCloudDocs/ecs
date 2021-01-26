---
keyword: [zombie, connection through remote connection software failed, VNC, remote connection password]
---

# Connect to a Linux instance by using VNC

If you cannot use remote connection software such as PuTTY, Xshell, and SecureCRT to connect to a Linux instance, you can use the **VNC Connection** feature in the ECS console to connect to the Linux instance and view the real-time status of the instance operation interface.

-   An ECS instance is created.
-   A logon password is set for the instance. If you have not set a password or if you have forgotten the password, you must reset the password for the instance. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).

The VNC password must be six characters in length and is used to connect to the VNC management terminal in the ECS console, while the instance password is used to log on to the instance.

By default, a remote VNC connection session lasts for about 300 seconds. If you do not perform operations within these 300 seconds, the connection to the instance is closed. You must connect to the instance again.

If you cannot use remote connection software to connect to your instance, you can use the **VNC Connection** feature in the ECS console to connect to the instance and view the status of the instance, as described in the following table.

|Scenario|Operation|
|--------|---------|
|The instance started slowly due to startup self-check.|Check the progress of the self-check.|
|The firewall of the operating system is enabled by mistake.|Disable the firewall.|
|The ECS instance is hacked into, which causes a high CPU utilization and high bandwidth usage.|Troubleshoot and terminate abnormal processes.|

## Procedure

The following figure shows the workflow.

![Workflow](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6803909951/p5162.png)

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

5.  Connect to the VNC management terminal.

    **Note:** The VNC password is used in this step.

    -   If you use an Alibaba Cloud account to connect to the VNC management terminal for the first time, perform the following operations:
        1.  In the **VNC Password** dialog box, copy the password.

            **Note:** The VNC password is displayed only once when you connect to the VNC management terminal for the first time. Keep the password confidential.

        2.  Click **Close**.
        3.  In the **Enter VNC Password** dialog box, paste the password and click **OK**.
    -   If you forget your password or connect to the VNC management terminal for the first time as a RAM user, perform the following operations:
        1.  [Modify the VNC password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using VNC.md).
        2.  In the upper-left corner of the interface, choose **Send Remote Call** \> **Connect VNC**.
        3.  In the **Enter VNC Password** dialog box, enter the new password.
        4.  Click **OK**.
    -   If you connect to the VNC management terminal again by using your Alibaba Cloud account or as a RAM user, perform the following operations:

        In the **Enter VNC Password** dialog box, enter the password and click **OK**.

6.  Log on to the instance.

    **Note:** The instance password is used in this step.

    1.  Enter the username root and press the Enter key.

    2.  Enter the instance password and press the Enter key.

        In the upper-left corner of the interface, choose **Send Remote Call** \> **CTRL+ALT+Fx** \(valid values of x: 1 to 10\) to switch between different VNC management terminals for connecting to the Linux instance. A persistent black screen indicates that the instance is in the sleep mode. Press any key to wake up the system.

        **Note:** The password characters are not displayed when you enter the password. After you enter the password, press the Enter key.


## Modify the VNC password

When you connect to the VNC management terminal as a RAM user for the first time, you must modify the VNC password. You can also change the password when you forget or want to update the VNC password.

**Note:** After you modify the VNC password for a non-I/O optimized instance, you must restart the instance in the ECS console for the new password to take effect. Before you restart the instance, you must stop it. This will lead to service interruption. Proceed with caution.

1.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

2.  Close the **VNC Password** or **Enter VPC Password** dialog box.

3.  In the upper-right corner of the interface, click **Modify VNC Password**.

4.  In the **Modify VNC Password** dialog box, enter and confirm the new password, and then click **OK**.

5.  If the instance is a non-I/O optimized instance, restart the instance.

    For more information, see [Reboot the instance](/intl.en-US/Instance/Manage instances/Restart an instance.md).


## Copy long commands

If you want to copy a long text item such as a download URL from the local device to the instance, you can use the copy command input feature.

1.  On the **Instances** page, find the instance to be connected and click **Connect** in the **Actions** column.

2.  Connect to the VNC management terminal.

3.  In the upper-right corner of the interface, click **Enter Copy Commands**.

4.  In the **Copy and Paste Commands** dialog box, enter the content to be copied and then click **OK**.


