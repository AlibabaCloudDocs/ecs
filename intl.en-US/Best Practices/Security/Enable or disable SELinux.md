# Enable or disable SELinux

Security-enhanced Linux \(SELinux\) is a Linux kernel feature that provides a security policy-based protection mechanism for access control. This topic describes how to enable or disable SELinux and avoid system boot failures.

An ECS instance is created from an Alibaba Cloud public image or a custom image.

**Note:** If the custom image that you use was created from imported local files or migrated from the source server in Server Migration Center \(SMC\), ensure that SELinux is disabled on the source server before migration.

Typically, enabled SELinux can enhance system security. However, it can damage files in the operating system and lead to system boot failures. If your enterprise or team has high requirements on security and SELinux must be enabled for your operating systems, you can perform operations in this topic to enable SELinux and avoid system boot failures. In this topic, the CentOS 7.2 64-bit operating system is used.

## Enable SELinux

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the following command on an instance to modify the `config` file of SELinux:

    ```
    vi /etc/selinux/config
    ```

3.  Find `SELINUX=disabled`, press the `I` key to enter the edit mode, and then enable SELinux by modifying this parameter.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3437846161/p76895.png)

    You can modify the parameter to one of the following modes:

    -   `SELINUX=enforcing`: indicates that all security policy violations will be prohibited.
    -   `SELINUX=permissive`: indicates that security policy violations will not be prohibited but will be recorded in the operation logs.
4.  Press the `Esc` key and run the `:wq` command to save and close the file.

    **Note:** After you modify the `config` file, you must restart the instance for the modification to take effect. However, if you restart the instance directly, the system may fail to start. You need to create an `autorelabel` file under the root directory before you restart the instance.

5.  Create the hidden `autorelabel` file under the root directory. After the instance is restarted, SELinux automatically relabels all system files.

    ```
    touch /.autorelabel
    ```

6.  Restart the ECS instance.

    ```
    shutdown -r now
    ```


## Check SELinux status

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the `getenforce` command to check the status of SELinux.

    The return value can be `enforcing` or `permissive`. The return value in this topic is `enforcing`.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3437846161/p77235.png)

3.  Run the `sestatus` command to query more information about SELinux.

    ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4437846161/p77236.png)

    If the return value of `SELinux status` is `enabled`, SELinux is enabled.


## Disable SELinux

1.  Remotely connect to an ECS instance as a root user. For more information, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

2.  Run the `getenforce` command to check the status of SELinux.

    If the return value is `enforcing`, SELinux is enabled.

3.  Disable SELinux temporarily or permanently.

    -   Run the `setenforce 0` command to disable SELinux temporarily.
    -   Disable SELinux permanently.
        1.  Run the following command to edit the `config` file of SELinux:

            ```
            vi /etc/selinux/config
            ```

        2.  Find `SELINUX=enforcing`, press the `I` key to enter the edit mode, and then modify the parameter to `SELINUX=disabled`.

            ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4437846161/p77234.png)

        3.  Press the `Esc` key and run the `:wq` command to save and close the file.
        4.  Restart the ECS instance.

            ```
            shutdown -r now
            ```

        5.  Run the `getenforce` command to check the status of SELinux. If the return value is `disabled`, SELinux is disabled.

You can create a custom image from an ECS instance that has SELinux enabled. Then, you can create more SELinux-enabled instances from this custom image.

