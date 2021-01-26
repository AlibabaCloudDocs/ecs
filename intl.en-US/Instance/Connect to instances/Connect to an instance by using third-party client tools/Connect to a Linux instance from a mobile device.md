---
keyword: [Alibaba Cloud, ECS, server, elastic computing]
---

# Connect to a Linux instance from a mobile device

This topic describes how to use a username and password to connect to a Linux instance from an iOS or Android mobile device.

-   An ECS instance is created.
-   A logon password is set for the instance.
-   A public IP address or an elastic IP address \(EIP\) is associated with the instance.
-   The instance is in the Running state.
-   A security group rule is added to the security group to which the instance belongs to allow traffic on the corresponding port. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Network type|Rule direction|Action|Port range|Priority|Authorization object|
    |------------|--------------|------|----------|--------|--------------------|
    |VPC|Inbound|Allow|SSH \(22\)|1|0.0.0.0/0|
    |Classic network|Internet ingress|

    |Network type|NIC type|Rule direction|Action|Protocol type|Port range|Priority|Authorization type|Authorization object|
    |------------|--------|--------------|------|-------------|----------|--------|------------------|--------------------|
    |VPC|N/A|Inbound|Allow|SSH \(22\)|22/22|1|IPv4 CIDR Block|0.0.0.0/0|
    |Classic network|Public|


You can use one of the following methods to connect to a Linux instance based on the operating system of your mobile device:

-   [Use SSH Control Lite to connect to a Linux instance from an iOS device](#section_1k4_15a_pb8)
-   [Use JuiceSSH to connect to a Linux instance from an Android device](#section_euu_1ti_i0n)

## Use SSH Control Lite to connect to a Linux instance from an iOS device

In this example, a username and password is used for authentication.

1.  Download SSH Control Lite.

2.  Start SSH Control Lite.

3.  In the lower part of the page, tap **Hosts**.

4.  In the upper-left corner of the page, tap the **+** icon.

    ![Connect to a Linux instance from an iOS device - 001](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77178.png)

5.  Tap **Connection**.

    ![Connect to a Linux instance from an iOS device - 002](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77179.png)

6.  Configure the connection parameters and tap **Save**.

    -   **Name**: Specify the host name. In this example, **DocTest** is used.
    -   **Protocol**: Use the default value **SSH**.
    -   **Host**: Specify the public IP address or EIP of the Linux instance to which you want to connect.
    -   **Port**: Enter the port number **22**.
    -   **Username**: Enter the username **root**.
    -   **Password**: Enter the password to log on to the instance.
    ![Connect to a Linux instance from an iOS device - 003](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77180.png)

7.  In the lower part of the page, tap **Remote Controls**.

    ![Connect to a Linux instance from an iOS device - 004](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77181.png)

8.  In the upper-left corner of the page, tap the **+** icon.

    Create a remote connection session. In this example, the session name is specified as **New remote**.

    ![Connect to a Linux instance from an iOS device - 005](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77187.png)

9.  Tap **Host1**.

    ![Connect to a Linux instance from an iOS device - 006](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9557887851/p77190.png)

10. Tap **Bind**.

    ![Connect to a Linux instance from an iOS device - 007](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77193.png)

11. Select the newly added Linux instance.

    In this example, **DocTest** is used.

    ![Connect to a Linux instance from an iOS device - 008](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77196.png)

12. In the upper-right corner of the page, tap **Done**. When **Edit** is displayed in the upper-right corner of the page, tap **DocTest**.

    ![Connect to a Linux instance from an iOS device - 009](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77198.png)

13. Tap **Connect**.

    ![Connect to a Linux instance from an iOS device - 010](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77199.png)

14. Select **Yes, Once** or **Yes, Permanently**.

    If the connection is successful, the indicator icon next to **DocTest** becomes green.

    ![Connect to a Linux instance from an iOS device - 011](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77204.png)

15. Tap **DocTest**.

    ![Connect to a Linux instance from an iOS device - 012](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77205.png)

16. Tap **Console** to go to the Linux instance management page.

    ![Connect to a Linux instance from an iOS device - 013](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0657887851/p77206.png)


You have connected to the Linux instance.

![Connect to a Linux instance from an iOS device - 014](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p77214.png)

## Use JuiceSSH to connect to a Linux instance from an Android device

In this example, a username and password is used for authentication.

1.  Install JuiceSSH.

2.  Start JuiceSSH.

3.  Tap **Connections**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p5320.png)

4.  Tap the **+** icon.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p5321.png)

5.  Configure the connection parameters and tap the ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png) icon.

    -   **Nickname**: Specify the session name. In this example, **DocTest** is used.
    -   **Type**: Use the default value **SSH**.
    -   **Address**: Specify the public IP address or EIP of the Linux instance to which you want to connect.
    -   Set **Identity**.
        1.  Tap **Identity** and select **New** from the drop-down list.
        2.  Specify the following parameters and tap the ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png) icon.
            -   **NickName**: optional. You can specify an identity name based on your management needs. In this example, **DocTest** is used.
            -   **Username**: Enter the username **root**.
            -   **Password**: Tap **SET\(OPTIONAL\)** and enter the password to log on to the instance.

                ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p5322.png)

    -   **Port**: Enter the port number **22**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p5323.png)

6.  Read the prompt and tap **ACCEPT**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1657887851/p5324.png)

7.  When you connect to the instance for the first time, a message appears to remind you to set information such as font. Read the information and tap **OK - I'VE GOT IT!**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2657887851/p5325.png)


You have connected to the Linux instance.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2657887851/p5326.png)

**Related topics**  


[OverviewGuidelines on instance connection](/intl.en-US/Instance/Connect to instances/Overview.md)

