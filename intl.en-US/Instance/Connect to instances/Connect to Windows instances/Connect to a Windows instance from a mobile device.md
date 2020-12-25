---
keyword: [Alibaba Cloud, ecs, server, elastic computing]
---

# Connect to a Windows instance from a mobile device

This topic describes how to connect to a Windows ECS instance from an Android device. Microsoft Remote Desktop is used in this topic.

Before you connect to an ECS instance, take note of the following items:

-   The instance is in the **Running** state.
-   The instance has a public IP address and is accessible from the Internet.
-   The logon password for the instance is set. If you forget the password, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instances/Reset the logon password of an instance.md).
-   Microsoft Remote Desktop is installed. For more information about the software, visit the [Microsoft website](https://www.microsoft.com/en-us/p/microsoft-remote-desktop/9wzdncrfj3ps).
-   A security rule is added to the security group to which the instance belongs. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Network type|NIC type|Direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:-------|:--------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC|Not required|Inbound|Allow|RDP \(3389\)|3389/3389|CIDR block|0.0.0.0/0|1|
    |Classic network|Public|

-   If you log on to the Windows instance as a non-administrator user, the username must belong to the Remote Desktop Users group.

1.  Start RD Client.

2.  In the upper-right corner of the **Remote Desktop** page, tap the **+** icon.

    ![Remote Desktop](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1539889851/p5327.png)

3.  On the **Add New** page, select **Desktop**.

    ![Add New](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2539889851/p5329.png)

4.  On the **Edit Desktop** page, configure the connection information and tap **Save**.

    You must configure the following parameters to connect to the Windows instance:

    -   **PC Name**: the public IP address
    -   **User Account**: the username, such as **administrator**, and logon password of the instance

        ![Edit Desktop](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2539889851/p5330.png)

5.  On the **Remote Desktop** page, tap the icon of the Windows instance to which you want to connect.

    ![Remote Desktop](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2539889851/p5331.png)

6.  On the confirmation page, tap **Accept**.

    ![Confirmation page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2539889851/p5332.png)


You are connected to the Windows instance.

![Connected to the Windows instance](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2539889851/p5333.png)

**Related topics**  


[Overview](/intl.en-US/Instance/Connect to instances/Overview.md)

