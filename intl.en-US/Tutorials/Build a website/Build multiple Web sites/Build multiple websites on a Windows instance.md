# Build multiple websites on a Windows instance

This topic describes how to use Internet Information Services \(IIS\) to build multiple websites on a Windows Elastic Compute Service \(ECS\) instance. In this topic, the instance runs Windows Server 2012 R2 64-bit.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An instance is created, and the web environment that consists of IIS, PHP, and MySQL is deployed on the instance. You can use a Windows image from [Alibaba Cloud Marketplace](https://marketplace.alibabacloud.com/) that is installed with the environment to deploy the environment.

This tutorial is intended for users who are familiar with Windows and want to optimize the O&M process by making efficient use of resources and managing sites in a centralized manner. For example, you can configure multiple blogging platforms of different categories or build multiple websites to handle complex business tasks on an instance.

In this tutorial, IIS is used to simultaneously build the `windows-testpage-1` and `windows-testpage-2` websites and configure different domain names on the same port to access the websites.

In this topic, the following instance configurations are used:

-   Instance type: ecs.c6.large
-   Operating system: Windows Server 2012 R2 64-bit

## Create test websites

1.  Connect to the instance on which the web environment is deployed.

    For more information, see [Connect to a Windows instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Windows instance by using password authentication.md).

2.  On the desktop, click **This PC** and go to the C:\\wwwroot path in the default root directory.

3.  Create the `windows-testpage-1` and `windows-testpage-2` folders.

    ![wwwroot](../images/p128806.png)

4.  Open the `windows-testpage-1` folder, create the test1.php file in the folder, and then enter the following content in the file:

    ```
    <?php
    echo "<title>Test-1</title>";
    echo "windows-test-1";
    ?>
    ```

5.  Open the `windows-testpage-2` folder, create the test2.php file in the folder, and then enter the following content in the file:

    ```
    <?php
    echo "<title>Test-2</title>";
    echo "windows-test-2";
    ?>
    ```


## Configure IIS

1.  In the taskbar, click the **Server Manager** icon![server](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5703243061/p128809.png).

2.  In the top navigation bar, choose **Tools** \> **Internet Information Services \(IIS\) Manager**.

3.  In the left-side navigation pane of IIS Manager, click the name of the server and click **Sites**.

4.  In the Actions section on the right, click **Add Website**. Add the `windows-testpage-1` website and click **OK**.

    The following figure shows how to configure the website.

    ![netsite1](../images/p128817.png)

    The following list describes how to configure the parameters:

    -   Site name: Enter `windows-testpage-1`.
    -   Application pool: Select DefaultAppPool.
    -   Physical path: Select a physical path for the `windows-testpage-1` website.
    -   Host name: Specify the `test1.com` domain name as the hostname.
5.  In the Actions section on the right, click **Add Website**. Add the `windows-testpage-2` website and click **OK**.

    The following figure shows how to configure the website.

    ![netsite2](../images/p128819.png)

    The following list describes how to configure the parameters:

    -   Site name: Enter `windows-testpage-2`.
    -   Application pool: Select DefaultAppPool.
    -   Physical path: Select a physical path for the `windows-testpage-2` website.
    -   Host name: Specify the `test2.com` domain name as the hostname.
    The following figure indicates that the websites are added.

    ![result](../images/p128823.png)


## \(Optional\) Configure the hosts file on the local host

In this tutorial, the domain names are used only for test purposes. You must configure IP mapping in the local hosts file. If you use the actual server domain names when you configure the websites, skip this step. In this tutorial, the local physical server uses the Windows operating system.

1.  Go to the C:\\Windows\\System32\\drivers\\etc directory.

2.  Copy the hosts file for backup.

    Retain the hosts - copy file, which can be used to restore the hosts file to the initial state after the test is complete.

3.  Modify the hosts file.

    Append the following content to the end of the file, save the file, and then exit the file:

    ```
    <Public IP address of the instance> test1.com
    <Public IP address of the instance> test2.com
    ```

4.  Go back to the Windows desktop and press Win+R.

5.  In the **Run** dialog box, enter cmd and click **OK**.

6.  Run the following command in the command line to make the configurations of the hosts file immediately take effect:

    ```
    ipconfig /flushdns
    ```


You can access the two test websites from a browser on the local host.

-   Enter `test1.com/test1.php` in the address bar of the browser and press the Enter key. The `windows-testpage-1` website is displayed, as shown in the following figure.

    ![test1.php](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897773061/p128826.png)

-   Enter `test2.com/test2.php` in the address bar of the browser and press the Enter key. The `windows-testpage-2` website is displayed, as shown in the following figure.

    ![test2.php](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8897773061/p128827.png)


Multiple websites are built. In your actual operations, you need only to make sure that the hostnames and project paths are correctly configured to access your websites. You can install SSL certificates in IIS. For more information, see [Install SSL certificates on IIS servers](/intl.en-US/Install Certificates/Install certificates to servers/Install SSL certificates on IIS servers.md).

