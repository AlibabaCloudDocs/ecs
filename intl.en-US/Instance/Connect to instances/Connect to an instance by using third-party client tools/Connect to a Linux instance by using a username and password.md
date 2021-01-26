---
keyword: [remote connection, SSH, Linux, logon, ECS, shell]
---

# Connect to a Linux instance by using a username and password

This topic describes how to use a username and password to connect to a Linux instance from a Windows, Linux, Mac OS X, Android, or iOS device.

-   An ECS instance is created.
-   A logon password is set for the instance.
-   A public IP address or an elastic IP address \(EIP\) is associated with the instance.
-   The instance is in the Running state.
-   A security group rule is added to the security group to which the instance belongs to allow traffic on the corresponding port. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

    |Network type|NIC type|Rule direction|Action|Protocol type|Port range|Priority|Authorization type|Authorization object|
    |------------|--------|--------------|------|-------------|----------|--------|------------------|--------------------|
    |VPC|N/A|Inbound|Allow|SSH \(22\)|22/22|1|IPv4 CIDR Block|0.0.0.0/0|
    |Classic network|Public|


You can use one of the following methods based on the operating system of your device to connect to a Linux instance by using a username and password:

-   [Use a username and password for authentication on a Windows device](#section_k1p_o74_bwm)
-   [Use a username and password for authentication on a Linux or Mac OS X device](#section_zo7_ddd_8yk)
-   [Use a username and password for authentication on an Android or iOS device](#section_x5j_164_ejd)

## Use a username and password for authentication on a Windows device

The following section describes how to use a username and password to connect to a Linux instance. PuTTY is used in this example.

1.  Download and install PuTTY.

    Click [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/) to download PuTTY.

2.  Start PuTTY.

3.  Configure required parameters to connect to the Linux instance.

    -   **Host Name \(or IP address\)**: Specify the public IP address or EIP of the instance.
    -   **Port**: Enter the port number **22**.
    -   **Connection type**: Select **SSH**.
    -   **Saved Sessions**: optional. Enter an identifiable name and click **Save** to save the session. Saved sessions store session information so you do not need to enter session information such as the public IP address the next time you log on to the instance.

        ![Saved Session](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0257887851/p5249.gif)

4.  Click **Open**.

    When you connect to the instance for the first time, the **PuTTY Security Alert** message appears, which indicates that PuTTY cannot confirm the authenticity of the remote server and can provide only the public key fingerprint of the server. Click **Yes** to confirm that you trust this server. PuTTY then adds the public key fingerprint to the registry of the on-premises device.

    **Note:** If the **PuTTY Security Alert** message appears the next time you log on to the instance, the instance may suffer from [man-in-the-middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack). For more information, visit [PuTTY User Manual](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter2.html#gs-hostkey).

    ![PuTTY cannot confirm the authenticity of the remote server (instance)](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0257887851/p5251.png)

5.  Specify the username \(as root by default\) and press the Enter key.

6.  Specify the logon password of the instance and press the Enter key.

    The characters of the password are hidden as you enter the password. After you enter the password, press the Enter key.

    If the `Welcome to Alibaba Cloud Elastic Compute Service !` message appears, the connection to the instance is successful.


## Use a username and password for authentication on a Linux or Mac OS X device

1.  Run the following SSH command:

    ```
    ssh root@<Public IP address or EIP of the instance>
    ```

    Example:

    ```
    ssh root@47.99.XX.XX
    ```

2.  Enter the logon password of the instance.

    If the `Welcome to Alibaba Cloud Elastic Compute Service !` message appears, the connection to the instance is successful.


## Use a username and password for authentication on an Android or iOS device

For more information, see [Connect to a Linux instance from a mobile device](/intl.en-US/Instance/Connect to instances/Connect to an instance by using Workbench/Connect to a Linux instance from a mobile device.md).

