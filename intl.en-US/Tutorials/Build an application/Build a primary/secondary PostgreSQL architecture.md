---
keyword: build a secondary PostgreSQL system on a local server
---

# Build a primary/secondary PostgreSQL architecture

PostgreSQL is one of the most advanced open source databases and supports NoSQL data types such as JSON, XML, and hstore. This topic describes how to build a primary/secondary PostgreSQL architecture on an Elastic Compute Service \(ECS\) instance that runs CentOS 7.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   An inbound rule is added to the security group of the instance to allow traffic on port 5432. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

The procedure described in this topic is applicable to Alibaba Cloud users who are familiar with Alibaba Cloud ECS, Linux operating systems, and PostgreSQL databases.

The following instance type and software versions are used in this topic. The operations may vary with the versions of your software.

-   Instance type: ecs.g6.large
-   Operating system: CentOS 7.2
-   PostgreSQL: 9.5

To install PostgreSQL by using YUM and build a primary/secondary PostgreSQL architecture, perform the following operations:

## Step 1: Create two ECS instances

To build a primary/secondary PostgreSQL architecture, you must create two instances of the Virtual Private Cloud \(VPC\) type. One instance works as the primary node, and the other instance works as the secondary node. For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md).

**Note:** We recommend that you do not assign public IP addresses to the ECS instances. You can bind an elastic IP address \(EIP\) to each ECS instance. This allows you to upgrade the configurations or optimize the architecture based on your actual requirements. For more information, see [Apply for new EIPs](/intl.en-US/User Guide/Create an EIP/Apply for new EIPs.md).

## Step 2: Configure the primary node of PostgreSQL

1.  Run the following commands in sequence to install PostgreSQL:

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

    **Note:** PostgreSQL 9.5 is used in this topic. We recommend that you use the latest version of PostgreSQL in your actual installation process.

2.  Run the following commands in sequence to start PostgreSQL and enable PostgreSQL to run on system startup:

    ```
    systemctl start postgresql-9.5.service    #Start PostgreSQL.
    ```

    ```
    systemctl enable postgresql-9.5.service   #Enable PostgreSQL to run on system startup.
    ```

3.  Create a database account named replica. This database is used for replication between the primary and secondary nodes. Then, specify the password, logon permission, and backup permission.

    1.  Run the following command to log on to PostgreSQL by using the postgres account:

        ```
        su - postgres
        ```

    2.  When `-bash-4.2$` appears, you are logged on to PostgreSQL. Then, run the following command to go to the interactive terminal of PostgreSQL:

        ```
        psql
        ```

    3.  When `postgres=#` appears, you are accessing the PostgreSQL interactive terminal. Then, set a password for the `postgres` account to enhance security.

        ```
        ALTER USER postgres WITH PASSWORD 'YourPassWord';
        ```

    4.  Enter the following SQL statement to create a database account named replica, specify a password, and configure the logon and backup permissions of the database.

        In this example, the password is set to `replica`.

        ```
        CREATE ROLE replica login replication encrypted password 'replica';
        ```

    5.  Run the following command to check whether the database account is created:

        ```
        SELECT usename from pg_user;
        ```

        The following results indicate that the account named replica is created:

        ```
        usename  
        ----------
        postgres
        replica
        (2 rows)
        ```

    6.  Run the following command to check whether the permissions are configured:

        ```
        SELECT rolname from pg_roles;
        ```

        The following results indicate that the permissions are created:

        ```
        rolname  
        ----------
        postgres
        replica
        (2 rows)
        ```

    7.  Run the following command and press the `Enter` key to exit the PostgreSQL interactive terminal:

        ```
        \q
        ```

    8.  Run the following command and press the `Enter` key to exit PostgreSQL:

        ```
        exit
        ```

4.  Run the following command to open the pg\_hba.conf file, and configure a whitelist for replica:

    ```
    vim /var/lib/pgsql/9.5/data/pg_hba.conf
    ```

    Add the following lines of information to the `IPv4 local connections` field:

    ```
    host    all             all             <The IPv4 CIDR block of the secondary node>          md5     #Enable MD5 password encryption for connections in the CIDR block of the VPC.
    host    replication     replica         <The IPv4 CIDR block of the secondary node>          md5     #Enable data synchronization from the replication database.
    ```

    After the information is added, press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit.

5.  Run the following command to open the postgresql.conf file:

    ```
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    Find and modify the following parameters:

    ```
    listen_addresses = '*'   #Specify the IP addresses on which the server is to listen for connections from client applications.
    wal_level = hot_standby  #Enable the hot standby mode.
    synchronous_commit = on  #Enable synchronization.
    max_wal_senders = 32     #Specify the maximum number of synchronization processes.
    wal_sender_timeout = 60s #Specify the timeout value for the streaming replication instance to synchronize data.
    max_connections = 100    #Specify the maximum number of connections. The value of max_connections for the secondary node must be greater than that for the primary node.
    ```

    After the parameters are modified, press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit.

6.  Run the following command to restart the PostgreSQL service:

    ```
    systemctl restart postgresql-9.5.service
    ```


## Step 3: Configure the secondary node of PostgreSQL

1.  Run the following commands in sequence to install PostgreSQL:

    ```
    yum update -y
    ```

    ```
    wget https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
    ```

    ```
    yum install postgresql95-server postgresql95-contrib -y
    ```

2.  Run the following command to create a backup directory by using the pg\_basebackup utility:

    ```
    # pg_basebackup -D /var/lib/pgsql/9.5/data -h <The IP address of the primary node> -p 5432 -U replica -X stream -P
    ```

    In this example, the `Password` parameter is set to `replica`.

    ```
    Password: 
    30075/30075 kB (100%), 1/1 tablespace
    ```

3.  Run the following commands in sequence to create and modify the recovery.conf file:

    ```
    cp /usr/pgsql-9.5/share/recovery.conf.sample /var/lib/pgsql/9.5/data/recovery.conf
    ```

    ```
    vim /var/lib/pgsql/9.5/data/recovery.conf
    ```

    Find and modify the following parameters:

    ```
    standby_mode = on     #Declare the secondary node.
    primary_conninfo = 'host=<The IP address of the primary node> port=5432 user=replica password=replica' #Specify the connection information of the primary node.
    recovery_target_timeline = 'latest' #Synchronize the latest data by using streaming replication.
    ```

    After the parameters are modified, press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit.

4.  Run the following command to open the postgresql.conf file:

    ```
    vim /var/lib/pgsql/9.5/data/postgresql.conf
    ```

    Find and modify the following parameters:

    ```
    max_connections = 1000             # Specify the maximum number of connections. The value for the secondary node must be greater than that for the primary node.
    hot_standby = on                   # Enable the hot standby mode.
    max_standby_streaming_delay = 30s  #Specify the maximum delay for streaming replication.
    wal_receiver_status_interval = 1s  #Specify the maximum interval for the secondary node to report the running status to the primary node.
    hot_standby_feedback = on          # Enable the secondary node to report errors to the primary node during replication.
    ```

    After the parameters are modified, press the Esc key, enter `:wq`, and then press the Enter key to save the file and exit.

5.  Run the following command to modify the group and owner of the data directory:

    ```
    chown -R postgres.postgres /var/lib/pgsql/9.5/data
    ```

6.  Run the following commands in sequence to start PostgreSQL and enable PostgreSQL to run on system startup:

    ```
    systemctl start postgresql-9.5.service    #Start PostgreSQL.
    ```

    ```
    systemctl enable postgresql-9.5.service   #Enable PostgreSQL to run on system startup.
    ```


## Step 4: Test the primary/secondary PostgreSQL architecture

To test the primary/secondary PostgreSQL architecture, make sure that the data interaction exists between the primary and secondary nodes. For example, the following content shows the expected result of testing when you create a backup directory for the secondary node:

```
# pg_basebackup -D /var/lib/pgsql/9.5/data -h <The IP address of the primary node> -p 5432 -U replica -X stream -P
```

1.  Run the following command to check the sender process on the primary node:

    ```
    ps aux |grep sender
    ```

    The following results indicate that the sender process is available:

    ```
    postgres  2916  0.0  0.3 340388  3220 ?        Ss   15:38   0:00 postgres: wal sender     process replica 192.168.**.**(49640) streaming 0/F01C1A8
    ```

2.  Run the following command to check the receiver process on the secondary node:

    ```
    ps aux |grep receiver
    ```

    The following results indicate that the receiver process is available:

    ```
    postgres 23284  0.0  0.3 387100  3444 ?        Ss   16:04   0:00 postgres: wal receiver process   streaming 0/F01C1A8
    ```

3.  On the primary node, go to the PostgreSQL interactive terminal and execute the following SQL statement to check the status of the secondary node:

    ```
    postgres=# select * from pg_stat_replication;
    ```

    The following results indicate that the status of the secondary node is available:

    ```
    pid | usesysid | usename | application_name | client_addr | client_hostname | client_port | backend_start | backend_xmin | state | sent_location | write_locati
    on | flush_location | replay_location | sync_priority | sync_state 
    ------+----------+---------+------------------+---------------+-----------------+------------- +-------------------------------+--------------+-----------+---------------+-------------
    ---+----------------+-----------------+---------------+------------
    2916 | 16393 | replica | walreceiver | 192.168.**.** | | 49640 | 2017-05-02 15:38:06.188988+08 | 1836 | streaming | 0/F01C0C8 | 0/F01C0C8 
    | 0/F01C0C8 | 0/F01C0C8 | 0 | async
    (1 rows)
    ```


