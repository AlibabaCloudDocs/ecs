---
keyword: [MySQL, install MySQL, configure MySQL, CentOS 8, DMS]
---

# Manually deploy a MySQL database on an ECS instance that runs CentOS 8

MySQL is a relational database management system and is often used to build the LAMP or LNMP environment. This topic describes how to install, configure, and remotely access a MySQL database on an ECS instance that runs CentOS 8.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   To use ECS instances that are located in mainland China regions, make sure that you have completed real-name verification for your account.
-   An ECS instance is created. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

In this topic, the following instance type and software versions are used. The operations may vary based on the versions of your software.

-   Instance type: ecs.c6.large \(two vCPUs and 4 GiB memory\)
-   Operating system: the CentOS 8.2 64-bit public image
-   MySQL: 8.0.21

    In this example, the following MySQL installation paths are used:

    -   Configuration file: /etc/my.cnf
    -   Data storage: /var/lib/mysql
    -   Command files: /usr/bin and /usr/sbin
-   Port: 3306

    **Note:** You must add inbound rules to the security group associated with the ECS instance and allow inbound traffic on port 3306. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).


## Step 1: Install MySQL

1.  Connect to the ECS instance that runs CentOS 8. For more information, see [Connect to a Linux instance by using VNC](/intl.en-US/Instance/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using VNC.md).

2.  Run the following command to install MySQL:

    ```
    dnf -y install @mysql
    ```

3.  Run the following command to view the MySQL version:

    ```
    mysql -V
    ```

    The following figure shows the query result.

    ![mysql 8.0.21](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0609276061/p179478.png)


## Step 2: Configure MySQL

1.  Run the following command to start MySQL and enable it to start upon system startup:

    ```
    systemctl enable --now mysqld
    ```

2.  Run the following command to check whether MySQL is started:

    ```
    systemctl status mysqld
    ```

    If the command output contains `Active: active (running)`, MySQL is started.

3.  Run the following command to make security configurations for MySQL and set the password:

    ```
    mysql_secure_installation
    ```

    After you run the command, perform the following operations based on the command prompts:

    1.  Enter Y and press the Enter key to make the configurations.
    2.  Enter 2 as the password strength and press the Enter key.

        0 indicates a low password strength, 1 indicates a medium password strength, and 2 indicates a high password strength. We recommend that you select a high password strength.

    3.  Enter a new password and confirm it.

        In this example, the password is `PASSword123！`.

    4.  Enter Y and press the Enter key to use the password.
    5.  Enter Y and press the Enter key to delete anonymous users.
    6.  Enter N and press the Enter key to disallow root users to remotely access MySQL.
    7.  Enter Y and press the Enter key to delete the `test` database and the access permissions on the `test` database.
    8.  Enter Y and press the Enter key to reload privilege tables.

## Step 3. Remotely access the MySQL database

We recommend that you use an account other than root user to remotely access the MySQL database. In this example, a MySQL account is created to remotely access MySQL.

1.  On the ECS instance, create and configure an account to remotely access MySQL.

    1.  Run the following command and enter the password of the root user to log on to the MySQL database:

        ```
         mysql -uroot -p
        ```

    2.  On the MySQL client, run the following commands in sequence to create an account for remote access to MySQL and allow remote hosts to access MySQL by using this account.

        In this example, the account is `dms` and the password is `PASSword123!`.

        ```
        create user 'dms'@'%' identified by 'PASSword123!' ;
        grant all privileges on *.* to 'dms'@'%'with grant option;
        flush privileges;
        ```

        **Note:** When you create an account, the password must meet the requirements. The password must be 8 to 30 characters in length, and must contain uppercase letters, lowercase letters, digits, and special characters. Special characters include

        `()` ~! @ # $ % ^ & * - + = | {} [] : ; ' < > , . ? /`

2.  Remotely access MySQL by using the `dms` account.

    -   We recommend that you use Data Management Service \(DMS\) provided by Alibaba Cloud to remotely access the MySQL database. For more information, see [Register an ApsaraDB instance]().
    -   You can use remote connection tools on your local computer to perform tests. Example: MySQL Workbench and Navicat.

