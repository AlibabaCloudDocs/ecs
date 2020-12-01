---
keyword: [MySQL, 安装MySQL, 配置MySQL, CentOS 8, DMS]
---

# 手动部署MySQL（CentOS 8）

MySQL是一个关系型数据库管理系统，常用于LAMP和LNMP等建站场景中。本教程介绍如何在CentOS 8系统ECS实例上安装、配置以及远程访问MySQL数据库。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   如果在中国内地地域中使用云服务器ECS，请确保账号已完成实名认证。
-   已创建一台ECS实例。详细步骤请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。

本教程在示例步骤中使用了以下实例规格和版本软件。实际操作时，请以您的软件版本为准。

-   实例规格：ecs.c6.large（2 vCPU，4 GiB内存）
-   操作系统：公共镜像CentOS 8.2 64位
-   MySQL：8.0.21

    本示例中，MySQL相关安装路径说明如下：

    -   配置文件：/etc/my.cnf
    -   数据存储：/var/lib/mysql
    -   命令文件：/usr/bin和/usr/sbin
-   数据库端口：3306

    **说明：** 您需要在ECS实例所使用的安全组入方向添加规则并放行3306端口。具体步骤，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。


## 步骤一：安装MySQL

1.  远程连接CentOS 8系统的ECS实例。具体操作，请参见[通过VNC远程连接登录Linux实例](/intl.zh-CN/实例/连接实例/连接Linux实例/通过VNC远程连接登录Linux实例.md)。

2.  运行以下命令安装MySQL。

    ```
    dnf -y install @mysql
    ```

3.  安装完成后，运行以下命令查看MySQL版本信息。

    ```
    mysql -V
    ```

    查看版本结果如下图所示。

    ![mysql 8.0.21](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/4826554061/p179478.png)


## 步骤二：配置MySQL

1.  运行以下命令启动MySQL，并设置为开机自启动。

    ```
    systemctl enable --now mysqld
    ```

2.  运行以下命令查看MySQL是否已启动。

    ```
    systemctl status mysqld
    ```

    查看返回结果中`Active: active (running)`表示已启动。

3.  运行以下命令执行MySQL安全性操作并设置密码。

    ```
    mysql_secure_installation
    ```

    命令运行后，根据命令行提示执行如下操作。

    1.  输入Y并回车开始相关配置。
    2.  选择密码验证策略强度，输入2并回车。

        策略0表示低，1表示中，2表示高。建议您选择高强度的密码验证策略。

    3.  设置MySQL的新密码并确认。

        本示例设置密码`PASSword123！`。

    4.  输入Y并回车继续使用提供的密码。
    5.  输入Y并回车移除匿名用户。
    6.  输入N并回车禁止root用户远程连接MySQL。
    7.  输入Y并回车删除`test`库以及对`test`库的访问权限。
    8.  输入Y并回车重新加载授权表。

## 步骤三：远程访问MySQL数据库

建议您使用非root账号远程登录MySQL数据库。本示例中，将创建新的MySQL用户账户，用于远程访问MySQL。

1.  在ECS实例上，创建并配置远程访问MySQL的账号。

    1.  运行以下命令后，输入root用户的密码登录MySQL。

        ```
         mysql -uroot -p
        ```

    2.  在MySQL客户端中，依次运行以下命令，创建用于远程访问MySQL的账号，并允许远程主机使用该账号访问MySQL。

        本示例中，账号为`dms`、密码为`PASSword123!`。

        ```
        create user 'dms'@'%' identified by 'PASSword123!';
        grant all privileges on *.* to 'dms'@'%'with grant option;
        flush privileges;
        ```

        **说明：** 实际创建账号时，密码需符合要求。长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。可以使用以下特殊符号：

        `()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/`

2.  使用`dms`账号远程登录MySQL。

    -   （推荐）您可以通过阿里云提供的数据管理服务DMS（Data Management Service）来远程访问MySQL数据库。详细信息，请参见[云数据库录入]()。
    -   您可以通过本地主机的远程连接工具进行测试。例如：MySQL Workbench、Navicat。

