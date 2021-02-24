# Manually build a WordPress website on an ECS instance that runs CentOS 8

WordPress is a blog-publishing system written in PHP. You can use WordPress as a content management system \(CMS\) or use WordPress to build your own websites on servers that support PHP and MySQL databases. This topic describes how to build a WordPress website on an ECS instance that runs a Linux operating system.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   A VPC-type security group is created. Inbound rules are added to the security group to allow traffic on port 80. If you want to connect to the Linux instance by using SSH, you must also allow traffic on port 22 in the inbound rules. For more information about how to add security group rules, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).
-   A Linux ECS instance is created and deployed with the LNMP environment. For more information, see [Manually build an LNMP environment in CentOS 8](/intl.en-US/Tutorials/Build a software development environment/Deploy LNMP/Manually build an LNMP environment in CentOS 8.md). Resources of the following versions are used in this topic:
    -   Instance type: ecs.c6.large
    -   Operating system: the CentOS 8.1 64-bit public image
    -   NGINX: 1.16.1
    -   MySQL: 8.0.17
    -   PHP:7.3.5
    -   WordPress: 5.4.2

**Note:** If you use resources that are of versions different from the preceding ones, you may need to adjust commands and parameter settings.

The tutorial is intended for enterprises or individuals who are familiar with Linux, but new to building WordPress websites on Alibaba Cloud ECS instances. You can also use the WordPress image provided in Alibaba Cloud Marketplace to build a WordPress website.

## Build a WordPress website

1.  Use the ECS console to connect to the Linux instance and configure a database for the WordPress website.

    1.  Connect to the ECS instance.

        For more information, see [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

    2.  Log on to MySQL.

        Log on to MySQL by using the `root` username and entering the password that you set for the root user when you build the LNMP environment.

        ```
        mysql -uroot -p
        ```

    3.  Create a database for the WordPress website that you want to build.

        In this tutorial, the database created for the WordPress website is wordpress.

        ```
        create database wordpress;
        ```

    4.  Create a new user to manage the wordpress database to improve security.

        In MySQL 5.7 and later, the password strength validation plug-in validate\_password is installed by default. You can log on to MySQL to view the password strength rules.

        ```
        show variables like "%password%";
        ```

        In this tutorial, the created user is named `user` and its password is `PASSword123.`

        ```
        create user 'user'@'localhost' identified by 'PASSword123.' ;
        ```

    5.  Grant the user all permissions on the wordpress database.

        ```
        grant all privileges on wordpress.* to 'user'@'localhost';
        ```

    6.  Run the following command to validate the preceding configurations:

        ```
        flush privileges;
        ```

    7.  Run the following command to exit MySQL:

        ```
        exit;
        ```

2.  Download and depress WordPress and move it to the root directory of the WordPress website.

    1.  Go to the root directory of the NGINX website and download the WordPress package.

        ```
        cd /usr/share/nginx/html
        wget https://wordpress.org/wordpress-5.4.2.zip
        ```

    2.  Decompress the WordPress package.

        ```
        unzip wordpress-5.4.2.zip
        ```

    3.  Copy the content of the `wp-config-sample.php` file in the WordPress installation directory to `wp-config.php`, and save `wp-config-sample.php` as a copy.

        ```
        cd /usr/share/nginx/html/wordpress
        cp wp-config-sample.php wp-config.php
        ```

    4.  Edit the `wp-config.php` file.

        ```
        vim wp-config.php
        ```

    5.  Press the I key to switch to the edit mode and modify MySQL-related configurations based on the wordpress database. The following content is an example of the modified code:

        The data of the WordPress website will be saved in the wordpress database by the user named `user`.

        ```
        // ** MySQL settings - The information is based on the host in use. ** //
        /** The name of the WordPress database */
        define('DB_NAME', 'wordpress');
        
        /** The username of the MySQL database */
        define('DB_USER', 'user');
        
        /** The password of the MySQL database */
        define('DB_PASSWORD', 'PASSword123.') ;
        
        /** The host of the MySQL database */
        define('DB_HOST', 'localhost');
        ```

    6.  Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and exit the configuration file.

3.  Modify the configuration file of NGINX.

    1.  Run the following command to open the configuration file of NGINX:

        ```
        vi /etc/nginx/conf.d/default.conf
        ```

    2.  Press the I key to enter the edit mode.

        Within the `location /` braces, replace the content that follows `root` with the wordpress root directory. The root directory is /usr/share/nginx/html/wordpress in this example.

        ![nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4481101061/p167509.png)

        Within the `location ~ .php$` braces, replace the content that follows `root` with the root directory of the WordPress website.

        ![nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4481101061/p167510.png)

        Press the Esc key to exit the edit mode and enter `:wq` to save and close the configuration file.

    3.  Run the following command to restart the NGINX service:

        ```
        systemctl restart nginx
        ```

4.  Install WordPress and log on to the WordPress website.

    1.  On your local physical machine, use a browser to access `<The public IP address of the ECS instance>` to go to the WordPress installation page.

    2.  Enter basic information of the website and click **Run the installation**.

        The following content describes the parameters to the specified:

        -   Site Title: The name of the WordPress website. Example: demowp.
        -   Username: The username used to log on to WordPress. Keep your username secure. Example: testwp.
        -   Password: We recommend that you choose a secure password. Example: Wp.123456.
        -   Your Email: The email used to receive notifications. Example: 1234567890@aliyun.com.
    3.  Click **Install Wordpress**.

    4.  Enter the username `testwp` and password `Wp.123456` that are used to install WordPress, and then click **LOGIN**.

        You are logged on to your WordPress website.


## Resolve the domain name of the WordPress website

If you allow users to access your WordPress website by using the public IP address of the ECS instance, this compromises the security of the ECS instance. If you have a domain name or need to register a domain name for your WordPress website, perform the following steps. The domain name to register in this tutorial is `www.WordPress.EcsQuickStart.com`.

1.  Register the domain name.

    For more information, see [Register a generic domain name](/intl.en-US/Quick Start/Register a generic domain name.md).

2.  Apply for an ICP filing.

    If the website of your domain name is hosted on an ECS instance located in a mainland China region, you must apply for an ICP filing.

3.  Resolve the domain name and bind it to the public IP address of the ECS instance.

    You must perform domain name resolution before you access your website by using a domain name. For more information, see [Domain name resolution](https://www.alibabacloud.com/help/doc-detail/58131.htm).

4.  Return to the ECS console, connect to the ECS instance on which the WordPress website is deployed, and log on to the MySQL database.

    ```
    mysql -uroot -p
    ```

5.  Use the wordpress database.

    ```
    use wordpress;
    ```

6.  Replace the public IP address of the ECS instance with the new domain name.

    ```
    update wp_options set option_value = replace(option_value, 'http://<The public IP address of the instance>', 'http://www.WordPress.EcsQuickStart.com') where option_name = 'home' OR option_name = 'siteurl';
    ```

7.  Run the following command to exit MySQL:

    ```
    exit;
    ```

    The new domain name is configured for your WordPress website.


## FAQ

-   Problem description: After a static link is set for the WordPress website, the web page to which the static link points cannot be accessed.

    Solution: If you set a website to be pseudo-static, search engines can include the website more easily. Before you set a static link for a WordPress website, you must specify pseudo-static rules in the NGINX server. To do this, perform the following operations:

    1.  Log on to the ECS instance on which the WordPress website is built.
    2.  Run the following command to open the configuration file of NGINX:

        ```
        vi /etc/nginx/conf.d/default.conf
        ```

    3.  Press the I key to enter the edit mode. Within the `location /` braces, add the following code:

        ```
        if (-f $request_filename/index.html){
        rewrite (.*) $1/index.html break;
        }
        if (-f $request_filename/index.php){
        rewrite (.*) $1/index.php;
        }
        if (! -f $request_filename){
        rewrite (.*) /index.php;
        }
        ```

        Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and exit the configuration file.

    4.  Run the following command to restart the NGINX service:

        ```
        systemctl restart nginx
        ```

-   Problem description: When I update the version of WordPress or upload a topic or plug-in in WordPress, a message is displayed. The message indicates that an FTP logon credential is required or that the directory cannot be created.

    Solution:

    1.  Log on to the ECS instance on which the WordPress website is built.
    2.  Run the following command to open the configuration file of WordPress:

        ```
        vim /usr/share/nginx/html/wordpress/wp-config.php
        ```

    3.  Press the I key to enter the edit mode. Add the following code to the end of the file:

        ```
        define("FS_METHOD","direct");
        define("FS_CHMOD_DIR", 0777);
        define("FS_CHMOD_FILE", 0777);
        ```

        Press the Esc key to exit the edit mode. Enter `:wq` and press the Enter key to save and exit the configuration file.

    4.  Return to the WordPress dashboard and refresh the page. Check whether the problem that an FTP logon credential is required is solved.

        If the problem that the directory cannot be created persists, return to the ECS instance and run the following command to change the owner of the root directory of the WordPress website to a NGINX user. In this example, the NGINX user is the `nginx` user.

        ```
        chown -R nginx /usr/share/nginx/html/wordpress
        ```


