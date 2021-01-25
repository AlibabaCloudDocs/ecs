# Manually build a WordPress website on a Windows ECS instance

This topic describes how to build a WordPress website on an ECS instance that is running a Windows operating system.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   A security group of the VPC type is created. Inbound rules are added for the security group to allow traffic on ports 80 and 3389. For more information about how to add security group rules, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   A Windows ECS instance is created and deployed with the web environment. The following software versions are used in this tutorial:
    -   Operating system: Windows Server 2012 R2 64-bit
    -   Internet Information Services \(IIS\): 7.5
    -   PHP: 7.0.28
    -   MySQL: 5.7
    -   WordPress: 5.3.2

**Note:** If you use software versions different from the preceding versions, you may need to adjust parameter settings.

## Build a WordPress website

1.  Use the ECS console to connect to the ECS instance that is deployed with the web environment and download the WordPress installation package.

    1.  Connect to the ECS instance.

    2.  Download the [WordPress installation package](https://wordpress.org/download/) from the official WordPress website.

        Version 5.3.2 is used in this tutorial.

        **Note:** If you download WordPress on an ECS instance that is located in a mainland China region and the `429 Too Many Requests` error is reported, we recommend that you try multiple times or download the WordPress installation package from a third-party website.

    3.  Decompress the WordPress installation package.

        In this tutorial, the WordPress installation package is decompressed to `C:\wordpress`.

2.  Create a MySQL database for the WordPress website that you want to build.

    1.  Go to the bin folder in the MySQL installation directory, right-click a blank area in this folder when you press and hold the `Shift` key, and then select **Open command window here**.

    2.  Log on to the MySQL database.

        ```
        mysql -u root -p
        ```

    3.  Create a database for the WordPress website.

        In this tutorial, the database that is created for the WordPress website is named wordpress.

        ```
        create database wordpress;
        ```

3.  Configure the WordPress website.

    1.  In the `C:\wordpress` directory, find the `wp-config-sample.php` file, copy it, and name the file copy `wp-config.php`.

    2.  Use the text editor to open the `wp-config.php` file and modify information related to the wordpress database.

        The following figure shows an example.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9329919951/p81914.png)

    3.  Save the `wp-config.php` file.

4.  Add the WordPress website to Server Manager.

    1.  Find the Server Manager icon in the Windows taskbar and open Server Manager.

        ![Server Manager](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9329919951/p110645.png)

    2.  In the top menu bar of the Server Manager window, choose **Tools** \> **Internet Information Services \(IIS\) Manager**.

    3.  In the **Connections** pane, choose **<ECS instance name\>** \> **Sites**.

    4.  Delete the website that is bound to port 80, or change the port number from 80 to an unused port, such as port 8080.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9329919951/p81925.png)

    5.  In the right-side **Actions** pane, click **Add Website** to add the WordPress website.

        The following figure shows an example.

        ![1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9329919951/p81927.png)

        The following content describes the parameters to be configured:

        -   Site name: the name of a custom website. In this tutorial, enter wordpress.
        -   Application pool: Select DefaultAppPool.
        -   Physical path: the directory where the WordPress installation package is decompressed. In this tutorial, select `C:\wordpress`.
        -   Port: Set it to 80.
5.  Install WordPress and log on to the WordPress website.

    1.  Visit `http://localhost/` from the ECS instance. The WordPress installation page is displayed.

    2.  Enter basic information of the website and click **Run the installation**.

        The following content describes the parameters to be specified:

        -   Site Title: The name of the WordPress website. Example: demowp.
        -   Username: The username used to log on to WordPress. Keep your username secure. Example: testwp.
        -   Password: We recommend that you choose a secure password. Example: Wp.123456.
        -   Your Email: The email used to receive notifications. Example: 1234567890@aliyun.com.
    3.  Click **Install WordPress**.

    4.  Enter the username and password that are used to install WordPress and click **LOGIN**.

        You are logged on to your WordPress website.


## Resolve the domain name of the WordPress website

If you allow users to access your WordPress website by using the public IP address of the ECS instance, this compromises the security of the ECS instance. If you have a domain name or need to register a domain name for your WordPress website, perform the following steps. The domain name to register in this tutorial is `www.WordPress.EcsQuickStart.com`.

1.  Register the domain name.

    For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

2.  Apply for an ICP filing.

    If the website of your domain name is hosted on an ECS instance located in a mainland China region, you must apply for an ICP filing.

3.  Resolve the domain name and bind it to the public IP address of the ECS instance.

    You must perform domain name resolution before you access your website by using a domain name. For more information, see [Domain name resolution](https://www.alibabacloud.com/help/doc-detail/58131.htm).

4.  Return to the ECS instance on which the WordPress website is deployed. Go to the bin folder in the MySQL installation directory, right-click a blank area in this folder when you press and hold the `Shift` key, and then select **Open command window here**.

5.  Log on to the MySQL database.

    ```
    mysql -u root -p
    ```

6.  Use the wordpress database.

    ```
    use wordpress;
    ```

7.  Replace `http://localhost/` with the new domain name.

    ```
    update wp_options set option_value = replace(option_value, 'http://localhost', 'http://www.WordPress.EcsQuickStart.com') where option_name = 'home' OR option_name = 'siteurl';
    ```

    The new domain name is configured for your WordPress website.


