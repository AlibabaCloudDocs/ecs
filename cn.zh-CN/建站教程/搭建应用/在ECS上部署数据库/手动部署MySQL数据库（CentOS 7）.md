---
keyword: [MySQL, 安装MySQL, 配置MySQL, 远程访问MySQL, DMS]
---

# 手动部署MySQL数据库（CentOS 7）

MySQL是一个关系型数据库管理系统，常用于LAMP和LNMP等网站场景中。本教程介绍如何在Linux系统ECS实例上安装、配置以及远程访问MySQL数据库。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   如果在中国内地地域中使用云服务器ECS，请确保账号已完成实名认证。如还未认证，请先完成[实名认证](https://account.console.aliyun.com/v2/#/authc/types)。
-   已创建一台ECS实例。详细步骤请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。

本教程在示例步骤中使用了以下实例规格和版本软件。实际操作时，请以您的软件版本为准。

-   实例规格：ecs.c6.large（2 vCPU，4 GiB内存）
-   操作系统：公共镜像CentOS 7.2 64位
-   MySQL：5.7.33

    本示例中，MySQL相关安装路径说明如下：

    -   配置文件：/etc/my.cnf
    -   数据存储：/var/lib/mysql
    -   命令文件：/usr/bin和/usr/sbin
-   数据库端口：3306

    **说明：** 您需要在ECS实例所使用的安全组入方向添加规则并放行3306端口。具体步骤，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。


## 步骤一：准备环境

连接您的ECS实例。具体操作，请参见[使用SSH密钥对连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用SSH密钥对连接Linux实例.md)或[使用用户名密码验证连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

## 步骤二：安装MySQL

1.  运行以下命令更新YUM源。

    ```
    rpm -Uvh  https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
    ```

2.  运行以下命令安装MySQL。

    ```
    yum -y install mysql-community-server
    ```

3.  运行以下命令查看MySQL版本号。

    ```
    mysql -V
    ```

    返回结果如下，表示MySQL安装成功。

    ![mysql版本信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4942730261/p271404.png)


## 步骤三：配置MySQL

1.  运行以下命令启动MySQL服务。

    ```
    systemctl start mysqld
    ```

2.  运行以下命令设置MySQL服务开机自启动。

    ```
    systemctl enable mysqld
    ```

3.  运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码。

    ```
    grep 'temporary password' /var/log/mysqld.log
    ```

    执行​命令结果示例如下。

    ```
    2020-04-08T08:12:07.893939Z 1 [Note] A temporary password is generated for root@localhost: xvlo1lZs7>uI
    ```

    **说明：** 示例末尾的`xvlo1lZs7>uI`为初始密码，下一步对MySQL进行安全性配置时，会使用该初始密码。

4.  运行下列命令对MySQL进行安全性配置。

    ```
    mysql_secure_installation
    ```

    1.  重置root用户的密码。

        **说明：** 在输入密码时，系统为了最大限度的保证数据安全，命令行将不做任何回显。您只需要输入正确的密码信息，然后按Enter键即可。

        ```
        Enter password for user root: #输入上一步获取的root用户初始密码
        The 'validate_password' plugin is installed on the server.
        The subsequent steps will run with the existing configuration of the plugin.
        Using existing password for root.
        Estimated strength of the password: 100 
        Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
        New password: #输入新密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
        Re-enter new password: #再次输入新密码
        Estimated strength of the password: 100 
        Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y #是否继续操作，输入Y
        ```

    2.  删除匿名用户账号。

        ```
        By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
        Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  #是否删除匿名用户，输入Y
        Success.
        ```

    3.  禁止root账号远程登录。

        ```
        Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
        Success.
        ```

    4.  删除test库以及对test库的访问权限。

        ```
        Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
        - Dropping test database...
        Success.
        ```

    5.  重新加载授权表。

        ```
        Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
        Success.
        All done!
        ```

    安全性配置的更多信息，请参见[MySQL官方文档](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。


## 步骤四：远程访问MySQL数据库

您可以使用数据库客户端或阿里云提供的数据管理服务DMS（Data Management Service）来远程访问MySQL数据库。本节以DMS为例，介绍远程访问MySQL数据库的操作步骤。

1.  在ECS实例上，创建远程登录MySQL的账号。

    1.  运行以下命令后，输入root用户的密码登录MySQL。

        ```
         mysql -uroot -p
        ```

    2.  依次运行以下命令创建远程登录MySQL的账号。

        建议您使用非root账号远程登录MySQL数据库，本示例账号为`dms`、密码为`123456`。

        **说明：** 实际创建账号时，需将示例密码`123456`更换为符合要求的密码，并妥善保存。密码要求：长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。可以使用以下特殊符号：

        `()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/`

        ```
        mysql> grant all on *.* to 'dms'@'%' IDENTIFIED BY '123456'; #使用root替换dms，可设置为允许root账号远程登录。
        mysql> flush privileges;
        ```

2.  登录[数据管理控制台](https://dms.console.aliyun.com/)。

3.  在左侧导航栏中，选择**自建库（ECS、公网）**。

4.  单击**新增数据库**。

5.  配置自建数据库信息。 具体操作，请参见[管理ECS实例自建数据库](/cn.zh-CN/建站教程/搭建应用/在ECS上部署数据库/管理ECS实例自建数据库.md)。

6.  单击**登录**。

    成功登录后，您可以使用DMS提供的菜单栏功能，创建数据库、表、函数等。


