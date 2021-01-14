---
keyword: [secure logon, SSH logon, ssh logon, Linux logon, ECS]
---

# Bind an SSH key pair to an instance

You can specify an SSH key pair when you create an ECS instance, or bind an SSH key pair to the instance after the instance is created. This topic describes how to bind an SSH key pair to an instance after the instance is created. If your ECS instance originally uses password-based authentication, the password-based authentication is automatically disabled after the key pair is bound.

Each ECS instance can be bound with only one SSH key pair in the console. If an ECS instance has already been bound with an SSH key pair, the new SSH key pair replaces the original one after the new SSH key pair is bound.

**Note:** After an SSH key pair is bound to a Linux instance, the public key of the key pair is stored in the ~/.ssh/authorized\_keys file. You can modify this file to add multiple key pairs or replace existing key pairs. For more information, see [Add or replace an SSH key pair](/intl.en-US/Security/Key pairs/Use an SSH key pair/Add or replace an SSH key pair.md).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).

2.  In the left-side navigation pane, choose **Network & Security** \> **SSH Key Pairs**.

3.  In the top navigation bar, select a region.

4.  Find the key pair to be bound and click **Bind** in the **Actions** column.

5.  Select the ECS instance to which to bind the SSH key pair in the **Select Instance** section, and then click the **\>** icon to move the target instance to the **Selected** section.

    If instance names in the **Select Instance** section are dimmed, the instances are Windows instances and cannot be bound with SSH key pairs.

6.  Click **OK**.

7.  If the selected ECS instance is in the **Running** \(Running\) state, perform the following operations to restart the instance to make the binding operation take effect:

    1.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.

    2.  Find the instance to be restarted and choose **More** \> **Instance Status** \> **Restart** in the **Actions** column.

    3.  In the **Restart Instance** dialog box, click **OK**.


-   After an SSH key pair is bound to an ECS instance, you can log on to the ECS instance by using the SSH key pair. For more information, see [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using an SSH key pair.md).
-   If you want to log on to an instance by using the password after you bind a key pair to the instance, you can reset the instance password. Then, you can log on to the instance by using the key pair or the new password. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).

**Related topics**  


[AttachKeyPair](/intl.en-US/API Reference/SSH key pairs/AttachKeyPair.md)

