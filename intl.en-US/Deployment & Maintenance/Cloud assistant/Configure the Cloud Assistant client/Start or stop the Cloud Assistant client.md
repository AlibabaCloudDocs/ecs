# Start or stop the Cloud Assistant client

The Cloud Assistant client is an agent that runs Cloud Assistant commands on ECS instances. This topic describes how to start or stop the Cloud Assistant client.

The Cloud Assistant client is installed. For more information, see [Install the Cloud Assistant client](/intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the Cloud Assistant client/Install the Cloud Assistant client.md).

## Stop or start the client on a Windows instance

To start or stop the Cloud Assistant client on a Windows instance, perform the following operations.

1.  Connect to the Windows instance. For more information, see [Connect to a Windows instance](/intl.en-US/Instance/Connect to instances/Connect to Windows instances/Connect to a Windows instance from a local client.md).

2.  Choose **Computer Management** \> **Services and Applications** \> **Services** and find **AliyunService**.

    **Warning:** **AliyunService** is the process of the Cloud Assistant client. If you stop **AliyunService**, the Cloud Assistant client also stops. This may only result in an exception on the ECS instance but cannot cause the instance to be stopped in the ECS console. Use caution when you stop AliyunService.

3.  Click **Stop** or **Restart** below AliyunService.

    ![Restart the service](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0597919951/p5250.png)


## Stop or start the client on a Linux instance

To start or stop the Cloud Assistant client on a Linux instance, perform the following operations.

1.  Connect to the Linux instance. For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a username and password.md).

2.  Run the following commands based on the init system of ECS instances:

    -   For the Linux operating systems based on new versions of the Linux kernel, which typically use the systemd initialization process, perform the following operations:

        ```
        # Check whether your ECS instance uses the systemd initialization process. If a message is returned, systemd is used.
        strings /sbin/init | grep "/lib/system"
        # Stop the Cloud Assistant client.
        systemctl stop aliyun.service
        # Start the Cloud Assistant client.
        systemctl start aliyun.service
        ```

    -   For Ubuntu 14 or earlier operating systems, which typically use the UpStart initialization process, perform the following operations:

        ```
        # Check whether your ECS instance uses the UpStart initialization process. If a message is returned, UpStart is used.
        strings /sbin/init | grep "upstart"
        # Stop the Cloud Assistant client.
        /sbin/initctl stop aliyun-service
        # Start the Cloud Assistant client.
        /sbin/initctl start aliyun-service
        ```

    -   For the Linux operating systems based on earlier versions of the Linux kernel, which typically use the sysvinit initialization process, perform the following operations:

        ```
        # Check whether your ECS instance uses the sysvinit initialization process. If a message is returned, sysvinit is used.
        strings /sbin/init | grep "sysvinit"
        # Stop the Cloud Assistant client.
        /etc/init.d/aliyun-service stop
        # Start the Cloud Assistant client.
        /etc/init.d/aliyun-service start
        ```


