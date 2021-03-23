# Boot a Linux ECS instance into single user mode

This topic describes how to boot an ECS instance that is created from a CentOS, Debian, SUSE Linux Enterprise Server \(SLES\), or Ubuntu image into single user mode.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An ECS instance is created. For more information, see [Creation method overview](/intl.en-US/Instance/Create an instance/Creation method overview.md). In this example, an ECS instance of the ecs.g6.large instance type is created.

Single user mode is one of the modes in which Linux distributions are booted. GRUB can be used to boot a Linux distribution into single user mode. After the system enters single user mode, you will have system administrator permissions and can modify all system configurations. This mode is usually used in the following scenarios:

-   Change the system password
-   Troubleshoot boot failures
-   Fix system exceptions
-   Maintain partitions of hard disk drives \(HDD\)

**Note:** In single user mode, you can modify critical system configurations. We recommend that you set this mode only when necessary and proceed with caution.

## References

-   [Example 1: How a CentOS ECS instance enters single user mode](#section_1nk_30k_rpj)
-   [Example 2: How a Debian ECS instance enters single user mode](#section_mo5_s2t_m7i)
-   [Example 3: How a SLES instance enters single user mode](#section_im9_5nl_g9k)
-   [Example 4: How an Ubuntu ECS instance enters single user mode](#section_4aa_ic6_c8p)

## Example 1: How a CentOS ECS instance enters single user mode

In this example, an ECS instance running a CentOS 8.0 64-bit operating system is used.

1.  Connect to the ECS instance.

    For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    **Note:** If you connect an instance by using Workbench or SSH commands, you are not directed to the system boot page when you restart the instance by using a command. Therefore, we recommend that you do not connect to an instance by using Workbench or SSH commands.

2.  Run the `reboot` command to restart the ECS instance. When the interface for selecting a boot system appears, press the E key to go to the configuration interface for boot options.

    The following figure shows the configuration interface for boot options.

    ![os1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7214488951/p94739.png)

3.  Move the pointer to the line that starts with `linux` by using the arrow keys on the keyboard. Replace the content from `ro` to the end of the line with `rw init=/bin/sh creashkernel=auto`.

    The following figure shows the information after the change is made.

    ![os2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1982435161/p94742.png)

4.  Press the Ctrl+X composite key or the F10 key.

    The system enters single user mode. The following figure shows the interface for resetting the system password.

    ![os3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94745.png)


## Example 2: How a Debian ECS instance enters single user mode

In this example, an ECS instance running a Debian 10.2 64-bit operating system is used.

1.  Connect to the ECS instance.

    For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    **Note:** If you connect an instance by using Workbench or SSH commands, you are not directed to the system boot page when you restart the instance by using a command. Therefore, we recommend that you do not connect to an instance by using Workbench or SSH commands.

2.  Run the `reboot` command to restart the ECS instance. When the configuration interface for kernel options appears, press the E key to go to the GRUB interface.

    The following figure shows the GRUB interface.

    ![db1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94723.png)

3.  Move the pointer to the line that starts with `linux` by using the arrow keys on the keyboard. Append `single` to the end of the line.

    The following figure shows the information after the change is made.

    ![db3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94715.png)

4.  Press the Ctrl+X composite key or the F10 key to start the system. Enter the password of the root user.

    The system enters single user mode.

    ![db4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94716.png)


## Example 3: How a SLES instance enters single user mode

In this example, an ECS instance running a SLES 15 SP1 64-bit operating system is used.

1.  Connect to the ECS instance.

    For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    **Note:** If you connect an instance by using Workbench or SSH commands, you are not directed to the system boot page when you restart the instance by using a command. Therefore, we recommend that you do not connect to an instance by using Workbench or SSH commands.

2.  Run the `reboot` command to restart the ECS instance. When the configuration interface for kernel options appears, press the E key to go to the GRUB interface.

    The following figure shows the GRUB interface.

    ![sles1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94725.png)

3.  Move the pointer to the line that starts with `linux` by using the arrow keys on the keyboard. Append `single` to the end of the line.

    The following figure shows the information after the change is made.

    ![sles2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94731.png)

4.  Press the Ctrl+X composite key or the F10 key to start the system. Enter the password of the root user.

    The system enters single user mode.

    ![sles3](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94733.png)


## Example 4: How an Ubuntu ECS instance enters single user mode

In this example, an ECS instance running an Ubuntu 18.04 64-bit operating system is used.

1.  Connect to the ECS instance.

    For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

    **Note:** If you connect an instance by using Workbench or SSH commands, you are not directed to the system boot page when you restart the instance by using a command. Therefore, we recommend that you do not connect to an instance by using Workbench or SSH commands.

2.  Run the `reboot` command to restart the ECS instance. During the restarting process, press the Shift key to go to the GRUB interface.

    The following figure shows the GRUB interface.

    ![ubt1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8214488951/p94572.png)

3.  Select the Advanced options for Ubuntu in the second line of the GRUB interface and press the Enter key.

4.  Select the recovery mode in the second line on the interface that appears and press the E key to edit the boot options.

    ![ubt2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9214488951/p94573.png)

5.  On the editing page, move the pointer to the line that starts with `linux` by using the arrow keys on the keyboard. Replace the content from `ro` to the end of the line with `rw single inti=/bin/bash`.

    The following figure shows the information after the change is made.

    ![ubt4](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9214488951/p94683.png)

6.  Press the Ctrl+X composite key or the F10 key.

    The system enters single user mode. The following figure shows the interface for resetting the system password.

    ![ubt5](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9214488951/p94707.png)


