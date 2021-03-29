---
keyword: [MySQL, install MySQL, configure MySQL, remotely access MySQL, DMS]
---

# Manually deploy a MySQL database on an instance running CentOS 7

MySQL is a relational database management system and is often used to build LAMP or LNMP environment. This topic describes how to install, configure, and remotely access a MySQL database on a Linux ECS instance.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   To use ECS instances that are located in mainland China regions, make sure that you have completed real-name verification for your account.
-   An ECS instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

In this topic, the following instance type and software versions are used. The operations may vary based on the versions of your software.

-   Instance type: ecs.c6.large \(2 vCPUs and 4 GiB memory\)
-   Operating system: public image CentOS 7.2 64-bit
-   MySQL: 5.7.33

    In this example, the following MySQL installation paths are used:

    -   Configuration file: /etc/my.cnf
    -   Data storage: /var/lib/mysql
    -   Command files: /usr/bin and /usr/sbin
-   Port: 3306

    **Note:** You must add inbound rules to a security group of the ECS instance and allow traffic on port 3306. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).


## Step 1. Prepare the environment

Connect to your ECS instance. For more information, see [Connect to a Linux instance by using an SSH key pair](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using an SSH key pair.md) or [Connect to a Linux instance by using a username and password](/intl.en-US/Instance/Connect to instances/Connect to an instance by using third-party client tools/Connect to a Linux instance by using a username and password.md).

## Step 2. Install MySQL

1.  Run the following command to update the YUM repository:

    ```
    rpm -Uvh  http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
    ```

2.  Run the following command to install MySQL:

    ```
    yum -y install mysql-community-server
    ```

3.  Run the following command to view the MySQL version:

    ```
    mysql -V
    ```

    MySQL is installed if the following result is returned:

    ```
    mysql  Ver 14.14 Distrib 5.7.33, for Linux (x86_64) using  EditLine wrapper
    ```


## Step 3. Configure MySQL

1.  Run the following command to start the MySQL service:

    ```
    systemctl start mysqld
    ```

2.  Run the following command to enable the MySQL service to run on system startup:

    ```
    systemctl enable mysqld
    ```

3.  Run the following command to check the /var/log/mysqld.log file, and obtain and record the initial password of the root user:

    ```
    grep 'temporary password' /var/log/mysqld.log
    ```

    A command output similar to the following one is displayed:

    ```
    2020-04-08T08:12:07.893939Z 1 [Note] A temporary password is generated for root@localhost: xvlo1lZs7>uI
    ```

    **Note:** The initial password in the example is `xvlo1lZs7>uI`. This initial password is used when you configure the security settings of MySQL.

4.  Run the following command to configure the security settings of MySQL:

    ```
    mysql_secure_installation
    ```

    1.  Reset the password of the root user.

        ```
        Enter password for user root: # Enter the initial password for the root user that you previously obtained.
        The 'validate_password' plugin is installed on the server.
        The subsequent steps will run with the existing configuration of the plugin.
        Using existing password for root.
        Estimated strength of the password: 100 
        Change the password for root ? (Press y|Y for Yes, any other key for No) : Y # Specify whether to change the password of the root user. Press the Y key.
        New password: # Enter a new password that is 8 to 30 characters in length. The password must contain uppercase letters, lowercase letters, digits, and special characters. Special characters include ( ) ` ~ !@ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ?/
        Re-enter new password: # Enter the new password again for confirmation.
        Estimated strength of the password: 100 
        Do you wish to continue with the password provided?((Press y|Y for Yes, any other key for No) : Y # Enter Y to continue.
        ```

    2.  Delete anonymous users.

        ```
        By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
        Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  # Enter Y to delete the anonymous user.
        Success.
        ```

    3.  Deny remote access from the root user.

        ```
        Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y # Enter Y to deny remote access from the root user.
        Success.
        ```

    4.  Delete the test database and access permissions on this database.

        ```
        Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y # Enter Y to delete the test database and permissions to access the database.
        - Dropping test database...
        Success.
        ```

    5.  Reload privilege tables.

        ```
        Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y # Enter Y to reload privilege tables.
        Success.
        All done!
        ```

    For more information about security settings of MySQL, visit [MySQL documentation](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html).


## Step 4. Remotely access the MySQL database

You can use a database client or Data Management Service \(DMS\) provided by Alibaba Cloud to remotely access the MySQL database. In this topic, DMS is used to show how to remotely access the MySQL database.

1.  On the ECS instance, create an account for remote logon to the MySQL database.

    1.  Run the following command and enter the password for the root user to log on to MySQL:

        ```
         mysql -uroot -p
        ```

    2.  Run the following commands in the sequence to create an account for remote logon to MySQL.

        We recommend that you use a non-root account to remotely log on to the MySQL database. The `dms` account and the `123456` password are used in this example.

        **Note:** When you create an account, replace the `123456` password with a more suitable one and keep it securely. The password must be 8 to 30 characters in length, and must contain uppercase letters, lowercase letters, digits, and special characters. Special characters include

        `()` ~!@ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ?/`

        ```
        mysql> grant all on *.* to 'dms'@'%'IDENTIFIED BY '123456'; # Replace dms with root to enable remote logon by using the root account.
        mysql> flush privileges;
        ```

2.  Log on to the [DMS console](https://dms.console.aliyun.com/).

3.  In the left-side navigation pane, click **User-Created Database \(ECS, Internet\)**.

4.  Click **Add Database**.

5.  Add the database that you have created. For more information, see [Manage user-created databases on ECS instances](/intl.en-US/Tutorials/Build an application/Deploy databases based on ECS/Manage user-created databases on ECS instances.md).

6.  Click **Log On**.

    After you are logged on, you can use the menu bar of DMS to create objects such as databases, tables, and functions.


