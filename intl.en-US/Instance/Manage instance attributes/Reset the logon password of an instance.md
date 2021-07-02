---
keyword: [the credential does not work when you connect to the instance, forget the password, change the password, retrieve the password, the username and password of the remote desktop]
---

# Reset the logon password of an instance

This topic describes how to reset the logon password of an ECS instance. This topic is applicable to scenarios such as when you forget the password or when you did not set a password during instance creation.

The instance is in a stable state, such as **Stopped** or **Running**. For more information about the status of an instance, see [ECS instance lifecycle](/intl.en-US/Instance/ECS instance lifecycle.md).

-   After you reset the logon password of an instance that is in the **Running** state, you must restart the instance to make the new password take effect. When you restart the instance, your services may be affected. We recommend that you reset the logon password during off-peak hours to avoid service disruption.
-   If the instance is a Linux instance, you can log on to the instance by using the password or the key pair. If you only use the password for authentication, this authentication method becomes invalid after you attach a key pair to your instance. If you want to use both methods to log on to the instance, you must reset its logon password.
-   You can also change the logon password of an instance by using Cloud Assistant or change the logon password of an instance by connecting to the instance. The change takes effect immediately and you do not need to restart the instance. For more information, see [Change the logon password of an instance](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Change the logon password of an instance.md) or [Change the logon password of an instance by connecting to the instance](/intl.en-US/Instance/Manage instance attributes/Change the logon password of an instance by connecting to the instance.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

3.  In the top navigation bar, select a region.

4.  Based on the number of instances whose passwords you want to change, you can perform different operations.

    -   To reset the password of a single instance, find the instance and choose **More** \> **Password/Key Pair** \> **Reset Password** in the **Actions** column.

        ![Reset the password of a single instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3101359951/p32543.png)

    -   To reset the password of multiple instances, select the instances and click **Reset Password** below the instance list.

        ![Reset the password of multiple instances](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3101359951/p5442.png)

5.  In the **Reset Password** dialog box, enter a valid new password and click **Submit**.

6.  Based on the instance status, you can perform one of the following operations to make the new password take effect:

    -   If the instance is in the **Running** state, click **Restart Now**.
    -   If the instance is in the **Stopped** state, click **Cancel** and manually restart the instance.

        If you click **Restart Now**, an error is displayed, indicating that this operation is not supported while the instance is in the current state. However, the password is already reset and will take effect the next time the instance starts.


**Related topics**  


[Change the logon password of an instance](/intl.en-US/Deployment & Maintenance/Cloud assistant/DevOps practice/Change the logon password of an instance.md)

[ModifyInstanceAttribute](/intl.en-US/API Reference/Instances/ModifyInstanceAttribute.md)

