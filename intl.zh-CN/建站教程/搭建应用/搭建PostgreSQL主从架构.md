---
keyword: PostgreSQL本地Slave搭建
---

# 搭建PostgreSQL主从架构

PostgreSQL被业界誉为最先进的开源数据库，支持NoSQL数据类型（JSON/XML/hstore）。本文档介绍在CentOS 7操作系统的ECS实例上搭建PostgreSQL主从架构的操作步骤。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   已在安全组入方向中添加规则放行5432端口。具体步骤，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

本教程适用于熟悉阿里云服务器ECS、Linux系统、PostgreSQL的阿里云用户。

本教程在示例步骤中使用了以下实例配置和软件版本。操作时，请您以实际软件版本为准。

-   实例规格：ecs.g6.large
-   操作系统：CentOS 7.2
-   PostgreSQL：9.5

本教程基于yum方式手动安装并搭建PostgreSQL主从复制架构。

## 步骤一：选购ECS实例

搭建PostgreSQL主从复制架构，需要选购2台专有网络类型的ECS实例，一台ECS实例作为主节点，另一台ECS实例作为从节点。 具体操作，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。

**说明：** 建议您不为ECS实例分配公网IP，按需购买弹性公网IP绑定至ECS实例，后续您可以根据实际情况考虑升级配置或调优架构。详情请参见[申请弹性公网IP](/intl.zh-CN/用户指南/申请EIP/申请新EIP.md)。

## 步骤二：配置PostgreSQL主节点

1.  依次运行以下命令安装PostgreSQL。

    ```
    yum update -y
    ```

    ```
    wget https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    ```

    ```
    rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
    ```

    ```
    yum install postgresql95-server postgresql95-contrib -y
    ```

    ```
    /usr/pgsql-9.5/bin/postgresql95-setup initdb
    ```

    **说明：** 本教程以PostgreSQL 9.5版本为例。实际安装时，请您使用最新版本。

2.  依次运行以下命令启动服务并设置服务开机自启动。

    ```
    systemctl start postgresql-9.5.service    #启动服务
    ```

    ```
    systemctl enable postgresql-9.5.service   #设置服务开机自启动
    ```

3.  在主节点上创建数据库账号replica（用于主从复制），并设置密码及登录权限和备份权限。

    1.  运行以下命令登录postgres用户。

        ```
        su - postgres
        ```

    2.  当显示`-bash-4.2$`时表示成功登录，然后输入以下命令进入PostgreSQL交互终端。

        ```
        psql
        ```

    3.  当显示`postgres=#`时表示成功进入交互终端，然后为用户`postgres`设置密码，增强安全性。

        ```
        ALTER USER postgres WITH PASSWORD 'YourPassWord';
        ```

    4.  输入以下SQL语句创建数据库账号replica，并设置密码及登录权限和备份权限。

        本示例中将密码设置为`replica`。

        ```
        CREATE ROLE replica login replication encrypted password 'replica';
        ```

    5.  查询账号是否创建成功。

        ```
        SELECT usename from pg_user;
        ```

        返回结果如下，表示已创建成功。

        ```
        usename  
        ----------
        postgres
        replica
        (2 rows)
        ```

    6.  查询权限是否创建成功。

        ```
        SELECT rolname from pg_roles;
        ```

        返回结果如下，表示已创建成功。

        ```
        rolname  
        ----------
        postgres
        replica
        (2 rows)
        ```

    7.  输入以下命令并按`Enter`键退出SQL终端。

        ```
        \q
        ```

    8.  输入一下命令并按`Enter`键退出PostgreSQL。

        ```
        exit
        ```

4.  运行以下命令打开pg\_hba.conf文件，设置replica用户白名单。

    ```
    vim /var/lib/pgsql/9.5/data/pg_hba.conf
    ```

    在`IPv4 local connections`段添加下面两行内容。

    ```
    host    all             all             <从节点的VPC IPv4网段>          md5     #允许VPC网段中md5密码认证连接
    host    replication     replica         <从节点的VPC IPv4网段>          md5     #允许用户从replication数据库进行数据同步
    ```

    添加完成后，按esc键，输入`:wq`并按下enter键，保存并退出。

5.  运行以下命令打开postgresql.conf文件。

    ```
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    分别找到以下参数，并将参数修改为以下内容：

    ```
    listen_addresses = '*'   #监听的IP地址
    wal_level = hot_standby  #启用热备模式
    synchronous_commit = on  #开启同步复制
    max_wal_senders = 32     #同步最大的进程数量
    wal_sender_timeout = 60s #流复制主机发送数据的超时时间
    max_connections = 100    #最大连接数，从库的max_connections必须要大于主库的
    ```

    修改完成后，按esc键，输入`:wq`并按下enter键，保存并退出。

6.  运行以下命令重启服务。

    ```
    systemctl restart postgresql-9.5.service
    ```


## 步骤三：配置PostgreSQL从节点

1.  依次运行以下命令安装PostgreSQL。

    ```
    yum update -y
    ```

    ```
    wget https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    ```

    ```
    yum install postgresql95-server postgresql95-contrib -y
    ```

2.  运行以下命令使用pg\_basebackup基础备份工具指定备份目录。

    ```
    pg_basebackup -D /var/lib/pgsql/9.5/data -h <主节点IP> -p 5432 -U replica -X stream -P
    ```

    本示例中`Password`为`replica`。

    ```
    Password: 
    30075/30075 kB (100%), 1/1 tablespace
    ```

3.  依次运行以下命令新建并修改recovery.conf配置文件。

    ```
    cp /usr/pgsql-9.5/share/recovery.conf.sample /var/lib/pgsql/9.5/data/recovery.conf
    ```

    ```
    vim /var/lib/pgsql/9.5/data/recovery.conf
    ```

    分别找到以下参数，并将参数修改为以下内容：

    ```
    standby_mode = on     #声明此节点为从库
    primary_conninfo = ‘host=<主节点IP> port=5432 user=replica password=replica’ #对应主库的连接信息
    recovery_target_timeline = ‘latest’ #流复制同步到最新的数据
    ```

    修改完成后，按esc键，输入`:wq`并按下enter键，保存并退出。

4.  运行以下命令打开postgresql.conf文件。

    ```
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    分别找到以下参数，并将参数修改为以下内容：

    ```
    max_connections = 1000             # 最大连接数，从节点需设置比主节点大
    hot_standby = on                   # 开启热备
    max_standby_streaming_delay = 30s  # 数据流备份的最大延迟时间
    wal_receiver_status_interval = 1s  # 从节点向主节点报告自身状态的最长间隔时间
    hot_standby_feedback = on          # 如果有错误的数据复制向主进行反馈
    ```

    修改完成后，按esc键，输入`:wq`并按下enter键，保存并退出。

5.  运行以下命令修改数据目录的属组和属主。

    ```
    chown -R postgres.postgres /var/lib/pgsql/9.5/data
    ```

6.  依次运行以下命令启动服务并设置服务开机自启动。

    ```
    systemctl start postgresql-9.5.service    #启动服务
    ```

    ```
    systemctl enable postgresql-9.5.service   #设置服务开机自启动
    ```


## 步骤四：检测验证

检测验证需要主从节点之间存在数据交互，例如，从节点备份目录时，进行检测能够得到预期的结果。

```
pg_basebackup -D /var/lib/pgsql/9.5/data -h <主节点IP> -p 5432 -U replica -X stream -P
```

1.  在主节点中运行以下命令查看sender进程。

    ```
    ps aux |grep sender
    ```

    返回结果如下，表示可成功查看到sender进程。

    ```
    postgres  2916  0.0  0.3 340388  3220 ?        Ss   15:38   0:00 postgres: wal sender     process replica 192.168.**.**(49640) streaming 0/F01C1A8
    ```

2.  在从节点中运行以下命令查看receiver进程。

    ```
    ps aux |grep receiver
    ```

    返回结果如下，表示可成功查看到receiver进程。

    ```
    postgres 23284  0.0  0.3 387100  3444 ?        Ss   16:04   0:00 postgres: wal receiver process   streaming 0/F01C1A8
    ```

3.  在主节点中进入PostgreSQL交互终端，输入以下SQL语句，在主库中查看从库状态。

    ```
    postgres=# select * from pg_stat_replication;
    ```

    返回结果如下，表示可成功查看到从库状态。

    ```
    pid | usesysid | usename | application_name | client_addr | client_hostname | client_port | backend_start | backend_xmin | state | sent_location | write_locati
    on | flush_location | replay_location | sync_priority | sync_state 
    ------+----------+---------+------------------+---------------+-----------------+------------- +-------------------------------+--------------+-----------+---------------+-------------
    ---+----------------+-----------------+---------------+------------
    2916 | 16393 | replica | walreceiver | 192.168.**.** | | 49640 | 2017-05-02 15:38:06.188988+08 | 1836 | streaming | 0/F01C0C8 | 0/F01C0C8 
    | 0/F01C0C8 | 0/F01C0C8 | 0 | async
    (1 rows)
    ```


