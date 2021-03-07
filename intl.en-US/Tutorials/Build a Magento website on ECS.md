# Build a Magento website on ECS {#concept_jny_5rl_2fb .concept}

Magento is an open-source e-commerce platform written in PHP. Many customers use it to build their B2B or B2C e-commerce platforms. This tutorial explains how to build a Magento platform on a single ECS instance.

In this tutorial,we will install the following tools:

-   MySQL version: 5.7
-   PHP version: 7.0
-   Magento version: 2.2

## Prerequisites {#section_nln_zrl_2fb .section}

[Create an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). Make sure the instance meets the following requirements: Operating system: CentOS 7.2 64bit. Minimum specifications include 2 Core CPU, 4 GiB RAM, and a 40 GiB Ultra Cloud Disk as the system disk. VPC-connected. If you do not have a VPC network, one will be created when you create an ECS instance. A public IP address is assigned to the instance.

Inbound Internet traffic to the TCP Port 80 of the ECS instance is allowed. For more information, see [create an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) and [add a security group rule](../../../../reseller.en-US/Security/Security groups/Add security group rules.md#).

|Service|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
|:------|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
|HTTP|Inbound|Allow|User-defined TCP|80/80|Address Field Access|0.0.0.0/0|1|
|MySQL|Inbound|Allow|User-defined TCP|3306/3306|Address Field Access|0.0.0.0/0|1|

## Procedure {#section_t5l_gsl_2fb .section}

To build a Magento website using ECS, follow these steps:

Step 1: Install LAMP on ECS.

Step 2: Configure the database.

Step 3: Install and configure Composer.

Step 4: Install and configure Magento.

Step 5: Test the installation.

**Step 1: Install LAMP \(Linux, Apache, MySQL, and PHP\) on ECS** 

This section describes how to manually install the LAMP platform. You can also start the ECS instance directly from the [cloud market](https://partners-intl.aliyun.com/marketplace/vodafone/) by purchasing LAMP images so that you can quickly build a website.

1.  Connect to the ECS instance and install Apache and MySQL.

    ``` {#codeblock_rms_yvq_cch}
    # yum -y update
    # yum -y install httpd
    # rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    # yum -y install mysql-community-server
    ```

2.  Start Apache and MySQL service and enable them at startup.

    ``` {#codeblock_gsi_07c_qb7}
    # systemctl start httpd
    # systemctl enable httpd
    # systemctl start mysqld
    # systemctl enable mysqld
    ```

3.  Configure the Apache configuration file: /etc/httpd/conf/httpd.conf.
    1.  Run `vim /etc/httpd/conf/httpd.conf`.
    2.  Press the `i` key.
    3.  Add the `LoadModule rewrite_module modules/mod_rewrite.so` line below `Include conf.modules.d/*.conf`, and replace `AllowOverride None` with `AllowOverride all` in the following section.

        ``` {#codeblock_jjl_3km_i7a}
        Options Indexes FollowSymLinks
        #
        # AllowOverride controls what directives may be placed in .htaccess files.
        # It can be "All", "None", or any combination of the keywords:
        # Options FileInfo AuthConfig Limit
        #
        AllowOverride None
        ```

    4.  Press the `Esc` key and type `:wq` to save and exit the file.
4.  Obtain the temporary password of the root account at the installation of MySQL by running the following.

    ``` {#codeblock_sj2_47d_ybj}
    # grep 'temporary password' /var/log/mysqld.log.
    2016-12-13T14:57:47.535748Z 1 [Note] A temporary password is generated for root@localhost: p0/G28g>lsHD
    ```

5.  Finish the MySQL security configuration, including:

    -   Resetting the root account password
    -   Disabling remote root logon
    -   Removing anonymous users
    -   Removing test database and test database access

        For more information, see the [official documentation](http://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html).

    ``` {#codeblock_mz0_9zv_023}
    # mysql_secure_installation
    Securing the MySQL server deployment.
    Enter password for user root:  # Enter your temporary root password that is recorded in the previous step
    The 'validate_password' plugin is installed on the server.
    The subsequent steps will run with the existing configuration of the plugin.
    Using existing password for root.
    Estimated strength of the password: 100 
    Change the password for root? (Press y|Y for Yes, any other key for No): Y
    New password: # Enter a new strong password. The password can be [8, 30] characters in length. It must contain uppercase letters, lowercase letters, and numbers. The following special characters are allowed: ()`~! @#$%^&amp;*-+=|{}[]:;‘&lt;>,.? /
    Re-enter new password: # Repeat the new password to confirm it
    Estimated strength of the password: 100 
    Do you wish to continue with the password provided?( Press y|Y for Yes, any other key for No) : Y
    By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
    Remove anonymous users? (Press y|Y for Yes, any other key for No): Y
    Success.
    Normally, root should only be allowed to connect from 'localhost'. 
    This ensures that someone cannot guess at the root password from the network.
    Disallow root login remotely? (Press y|Y for Yes, any other key for No): Y
    Success.
    By default, MySQL comes with a database named 'test' that anyone can access. 
    This is also intended only for testing, and should be removed before moving into a production
    environment.
    Remove test database and access to it? (Press y|Y for Yes, any other key for No): Y
    - Dropping test database...
    Success.
    - Removing privileges on test database...
    Success.
    Reloading the privilege tables will ensure that all changes
    made so far will take effect immediately.
    Reload privilege tables now? (Press y|Y for Yes, any other key for No): Y
    Success.
    All done!
    ```

6.  Install PHP 7.

    ``` {#codeblock_vix_ski_uh3}
    # yum install -y http://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-14.ius.centos7.noarch.rpm
    # yum -y update
    # yum -y install php70u php70u-pdo php70u-mysqlnd php70u-opcache php70u-xml php70u-gd php70u-mcrypt php70u-devel php70u-intl php70u-mbstring php70u-bcmath php70u-json php70u-iconv
    ```

7.  Validate PHP installation.

    ``` {#codeblock_zpt_xny_zq2}
    # php -v
    PHP 7.0.13 (cli) (built: Nov 10 2016 08:44:18) ( NTS )
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
    with Zend OPcache v7.0.13, Copyright (c) 1999-2016, by Zend Technologies
    ```

8.  Edit the /etc/php.ini file to set your time zone:
    1.  Run `vim /etc/php.ini`.
    2.  Press the `i` key.
    3.  Find the line starting with date.timezone which is commented out by default, and add the correct time zone. If your site is in China, add `date.timezone = Asia/Shanghai`.
9.  Restart httpd by running the following.

    ``` {#codeblock_8mk_i4g_o5d}
    systemctl start httpd
    ```


**Step 2: Configure the database** 

Follow these steps to configure a database:

1.  Create a database and a user. Run the following commands, including those typed in the mysql\> prompt.

    ``` {#codeblock_rfj_pk3_27a}
    # mysql -u root -p
    Enter password: 
    mysql> CREATE DATABASE magento;
    Query OK, 1 row affected (0.00 sec)
    mysql> GRANT ALL ON magento. * TO YourUser@localhost IDENTIFIED BY 'YourPass';
    Query OK, 0 rows affected, 1 warning (0.00 sec)
    mysql> FLUSH PRIVILEGES;
    Query OK, 0 rows affected (0.00 sec)
    ```

2.  Run `exit` to exit MySQL.
3.  Test the new user.

    ``` {#codeblock_jsm_vmk_ast}
    # mysql -u YourUser -p
    mysql> show databases;
    +--------------------+
    | Database |
    +--------------------+
    | information_schema |
    | magento |
    +--------------------+
    2 rows in set (0.00 sec)
    mysql> exit
    ```


**Step 3: Install and configure Composer** 

1.  Install Composer.

    ``` {#codeblock_un1_op3_78s}
    # curl -sS https://getcomposer.org/installer | php
    All settings correct for using Composer
    Downloading 1.2.4...
    Composer successfully installed to: /root/composer.phar
    Use it: php composer.phar
    ```

2.  Configure Composer.

    ``` {#codeblock_z7m_xsw_i0p}
    # mv /root/composer.phar /usr/bin/composer
    ```

3.  Test Composer.

    ``` {#codeblock_7k9_6vc_4nm}
    # composer -v
    ______
    / ____/___ ____ ___ ____ ____ ________ _____
    / / / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
    / /___/ /_/ / / / / / / /_/ / /_/ (__ ) __/ /
    \____/\____/_/ /_/ /_/ . ___/\____/____/\___/_/
    /_/
    Composer version 1.2.4 2016-12-06 22:00:51
    ```


**Step 4: Install and configure Magento** 

1.  Download Magento from github using the following commands through `git clone`.

    ``` {#codeblock_39b_8te_c3m}
    # yum -y install git
    # cd /var/www/html/
    # git clone https://github.com/magento/magento2.git
    ```

2.  Switch the version of Magento to the stable production version.

    ``` {#codeblock_jhl_uib_mno}
    # cd magento2 && git checkout tags/2.1.0 -b 2.1.0
    Switched to a new branch '2.1.0'
    ```

3.  Move the installation files to the Apache root directory. If you skip this step, you will only be able to access your Magento service at `http://your-server-ip /magento2`.

    ``` {#codeblock_5zu_bth_ndh}
    # shopt -s dotglob nullglob && mv /var/www/html/magento2/* /var/www/html/ && cd ..
    ```

4.  Set Magento file permissions.

    ``` {#codeblock_y5z_c1w_c11}
    # chown -R :apache /var/www/html
    # find /var/www/html -type f -print0 | xargs -r0 chmod 640
    # find /var/www/html -type d -print0 | xargs -r0 chmod 750
    # chmod -R g+w /var/www/html/{pub,var}
    # chmod -R g+w /var/www/html/{app/etc,vendor}
    # chmod 750 /var/www/html/bin/magento
    ```

5.  Run `composer install` to install Magento.
6.  Use your browser to access your server at `http://public IP address of your ECS instance`. You will see a welcome screen like this one.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156761186812984_en-US.png)

7.  Click **Agree and Setup Magento** and fill in the database information, web configuration, and accounts as follows. When you get a page like this, the installation is successful.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156761186812990_en-US.png)


**Step 5: Configure the cron job** 

1.  Run `crontab -u apache -e`.
2.  Add the following in the /etc/crontab file.

    ``` {#codeblock_7lj_3yu_5bn}
    */10 * * * * php -c /etc /var/www/html/bin/magento cron:run
    */10 * * * * php -c /etc /var/www/html/update/cron.php
    */10 * * * * php -c /etc /var/www/html/bin/magento setup:cron:run
    ```


For more information, see the [official documentation](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cron.html).

## What to do next {#section_jh3_l5l_2fb .section}

Visit `http://public IP address of your ECS instance` to see the default home page.

Visit `http://public IP address of your ECS instance/admin`, and use the user name and password you set during the installation to log on to the Dashboard.

For more information about Magento configuration, see the [official documentation](http://devdocs.magento.com/guides/v2.1/).

