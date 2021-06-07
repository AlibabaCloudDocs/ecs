# Start or stop the Cloud Assistant client

The Cloud Assistant client is an agent that runs Cloud Assistant commands on ECS instances. This topic describes how to start or stop the Cloud Assistant client.

## Stop or start the client on a Windows instance

To start or stop the Cloud Assistant client on a Windows instance, perform the following steps:

**Warning:** **Aliyun Assist Service** is the process of the Cloud Assistant client. If you stop **Aliyun Assist Service**, the Cloud Assistant client also stops. This may cause an exception on the ECS instance and the failure to stop the instance in the ECS console. Proceed with caution when you stop Aliyun Assist Service.

1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance from a local client](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Windows instance from a local client.md).

2.  Click Start and choose **Windows Administrative Tools** \> **Computer Management**.

3.  Choose **Computer Management \(Local\)** \> **Services and Applications** \> **Services**.

4.  Find **Aliyun Assist Service** and click **Stop** or **Restart**.

    ![Restart the service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0597919951/p5250.png)


## Uninstall the Cloud Assistant daemon process from a Linux instance

The Cloud Assistant daemon process is used to monitor the resource consumption of the Cloud Assistant client, report the running status of the client, and restart the client when the client fails. Before you stop the Cloud Assistant client, you must uninstall the Cloud Assistant daemon process first.

**Note:** The Cloud Assistant daemon process is available only for Linux instances.

1.  Connect to the Linux instance. For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Stop the Cloud Assistant daemon process.

    ```
    /usr/local/share/assist-daemon/assist_daemon --stop
    ```

    **Note:** /usr/local/share/assist-daemon/assist\_daemon is the default path of the Cloud Assistant daemon process.

3.  Uninstall the Cloud Assistant daemon process.

    ```
    /usr/local/share/assist-daemon/assist_daemon --delete
    ```

4.  Delete the directory of the Cloud Assistant daemon process.

    ```
    rm -rf /usr/local/share/assist-daemon
    ```


## Stop or start the client on a Linux instance

**Note:** Before you stop the Cloud Assistant client, you must uninstall the Cloud Assistant daemon process first. For more information, see the [Uninstall the Cloud Assistant daemon process from a Linux instance](#section_5mk_rz9_g50) section.

To start or stop the Cloud Assistant client on a Linux instance, perform the following steps:

1.  Connect to the Linux instance. For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

2.  Run the following commands based on the init system of the Linux instance:

    -   For Linux operating systems based on new versions of the Linux kernel, which typically use the systemd initialization process, perform the following steps:
        -   Check whether your instance uses the systemd initialization process. If a message is returned, systemd is used.

            ```
            strings /sbin/init | grep "/lib/system"
            ```

        -   Stop the Cloud Assistant client.

            ```
            systemctl stop aliyun.service
            ```

        -   Start the Cloud Assistant client.

            ```
            systemctl start aliyun.service
            ```

    -   For Ubuntu 14 or earlier operating systems, which typically use the UpStart initialization process, perform the following steps:
        -   Check whether your instance uses the UpStart initialization process. If a message is returned, UpStart is used.

            ```
            strings /sbin/init | grep "upstart"
            ```

        -   Stop the Cloud Assistant client.

            ```
            /sbin/initctl stop aliyun-service
            ```

        -   Start the Cloud Assistant client.

            ```
            /sbin/initctl start aliyun-service
            ```

    -   For Linux operating systems based on earlier versions of the Linux kernel, which typically use the sysvinit initialization process, perform the following steps:
        -   Check whether your instance uses the sysvinit initialization process. If a message is returned, sysvinit is used.

            ```
            strings /sbin/init | grep "sysvinit"
            ```

        -   Stop the Cloud Assistant client.

            ```
            /etc/init.d/aliyun-service stop
            ```

        -   Start the Cloud Assistant client.

            ```
            /etc/init.d/aliyun-service start
            ```


