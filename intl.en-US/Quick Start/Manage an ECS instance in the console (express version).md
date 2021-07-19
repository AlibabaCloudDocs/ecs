---
keyword: [create an ECS instance, quick start, quick purchase]
---

# Manage an ECS instance in the console \(express version\)

This topic describes how to create a subscription instance in scenarios that require only one or two Elastic Compute Service \(ECS\) instances without complex network configurations.

## Purchase an instance

1.  Go to the [Custom Launch](https://ecs-buy.aliyun.com/wizard/#/) tab.

    **Note:**

    If you have not created an Alibaba Cloud account, create one first. For more information, see [Sign up with Alibaba Cloud](https://www.alibabacloud.com/help/doc-detail/50482.htm).

2.  In the **Basic Configurations** step, configure parameters and click **Next: Networking**.

    ![Basic Configurations](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2845525061/p101036.png)

    The following table describes the parameters of which you must take note. For other parameters that are not described in this table, you can use the default values.

    |Parameter|Description|
    |---------|-----------|
    |Region|Select a region that is close to the region of your customer. This way, you can provide your customer with a higher access speed and lower latency. In this example, the **China \(Hangzhou\)** region is used. |
    |Instance Type|Select an appropriate instance type.     -   For individual applications, we recommend that you select the **ecs.t6-c2m1.large** instance type that has 2 vCPUs and 1 GiB memory.
    -   For applications of small and medium-sized enterprises, we recommend that you select the **ecs.c5.large** instance type that has 2 vCPUs and 4 GiB memory. |
    |Quantity|Default value: 1.|
    |Image|Specify an image for the instance.     -   **Public Image**: Select a pure operating system such as Linux or Windows.
    -   **Custom Image**: Select an operating system deployed with an application environment.
In this example, the **Alibaba Cloud Linux 2.1903 64-bit \(Quick Start\)** **public image** is used. |
    |Storage|Select an ultra disk as the system disk, which is 40 GiB in size by default.|
    |Duration|Default value: 1 Month.|

3.  In the **Networking** step, configure the network type, public bandwidth settings, and security group, as shown in the following figure. Then, click **Next: System Configurations**.

    ![Security group](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2845525061/p101039.png)

    Set the Bandwidth parameter, and use the default settings of the Network Type and Security Group parameters.

    |Parameter|Description|
    |---------|-----------|
    |Network Type|A virtual private cloud \(VPC\) is created by default.|
    |Public IP Address|Set the public bandwidth. The default value is 1 Mbit/s.|
    |Security Group|A security group is created by default.|

4.  In the **System Configurations \(Optional\)** step, set the logon password of the instance and click **Preview**.

    ![Set a password](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2845525061/p100347.png)

5.  Read and select the ECS terms of service and click **Create Order**.

6.  Confirm and pay for the order.


**Note:** For more information about all the parameters, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

## Connect to an ECS instance

You can connect to an ECS instance by using the [ECS console](https://ecs.console.aliyun.com/#/server).

**Note:** The default username of a Linux instance is root and that of a Windows instance is Administrator. If you forget your password, reset the password before you connect to the instance. For more information, see [Reset the logon password of an instance](/intl.en-US/Instance/Manage instance attributes/Reset the logon password of an instance.md).

1.  Go to the Instances page.

2.  Click **Connect** in the **Actions** column corresponding to the instance.

3.  In the **Enter VNC Password** dialog box, click **Modify VNC Password**.

4.  Modify the password. In the **Enter VNC Password** dialog box, enter your new password and click **OK**.

5.  On the instance logon page, enter the username and password of the instance.


**Note:** If you want to use a different method to connect to the ECS instance, see [Overview](/intl.en-US/Instance/Connect to instances/Overview.md).

## Manage an ECS instance

For more information about how to manage ECS instances, see [Quick reference](/intl.en-US/Best Practices/Quick reference.md).

You may need to use an instance to deploy an environment or build a website. Common operations:

-   Build a Linux, Apache, MySQL, and PHP \(LAMP\) environment. For more information, see [Build a LAMP environment](/intl.en-US/Tutorials/Build a software development environment/Build a LAMP environment.md).
-   Build a Linux, NGINX, MySQL, and PHP \(LNMP\) environment. For more information, see [Manually build an LNMP environment on a CentOS 7 instance](/intl.en-US/Tutorials/Build a software development environment/Deploy LNMP/Manually build an LNMP environment on a CentOS 7 instance.md).

For more information about tutorials for building websites, see [Summary of website building methods](/intl.en-US/Tutorials/Summary of website building methods.md).

## Release an ECS instance

You can manually release a subscription instance after it expires. If you do not renew the instance after it expires, the instance is automatically released.

