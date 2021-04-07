# Deploy RabbitMQ

This topic describes how to deploy RabbitMQ on an ECS instance.

-   An Alibaba Cloud account is created. To create an Alibaba Cloud account, go to the [account registration page](https://account.alibabacloud.com/register/intl_register.htm).
-   A security group of the VPC type is created. An inbound rule that allows traffic on ports 80, 5672, and 15672 is added to the security group. If you want to connect to a Linux instance in the security group by using SSH, you must also allow traffic on port 22 in the rule. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

RabbitMQ is an open source message broker that implements the Advanced Message Queuing Protocol \(AMQP\) to store and forward messages in a distributed system. RabbitMQ is easy to use, scalable, and highly available. The RabbitMQ server is written in the Erlang programming language. RabbitMQ supports multiple types of clients, such as Python, Ruby, .NET, Java, JMS, C, PHP, ActionScript, XMPP, STOMP, and AJAX.

Manually deploy RabbitMQ. This method is suitable for users who have a basic knowledge of Linux commands and allows for personalized deployment. Use the following operating system and software versions to manually deploy RabbitMQ:

-   Operating system: public image CentOS 7.3 64-bit
-   RabbitMQ: RabbitMQ Server 3.6.9
-   Erlang: Erlang 19.3
-   JDK: JDK 1.8.0\_121

## Manually deploy RabbitMQ

1.  Install dependencies.

    ```
    yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
    ```

2.  Install Erlang.

    1.  Download the Erlang installation package.

        ```
        wget http://erlang.org/download/otp_src_19.3.tar.gz
        ```

    2.  Decompress the Erlang installation package.

        ```
        tar xzf otp_src_19.3.tar.gz
        ```

    3.  Create a folder.

        ```
        mkdir /usr/local/erlang
        ```

    4.  Compile and install Erlang.

        Run the following commands:

        ```
        cd otp_src_19.3
        ./configure --prefix=/usr/local/erlang --without-javac
        ```

        ```
        make && make install
        ```

3.  Modify the profile configuration file.

    1.  Run the following command to open the profile configuration file:

        ```
        vi /etc/profile
        ```

    2.  Press the I key and add the following content to the end of the file:

        ```
        export PATH=$PATH:/usr/local/erlang/bin
        ```

    3.  Press the Esc key, enter `:wq`, and then press the Enter key to save and close the file.

4.  Make environment variables take effect and check the installation result.

    1.  Run the following command to make environment variables take effect:

        ```
        source /etc/profile
        ```

    2.  Run the following command to check the installation results:

        ```
        erl -version
        ```

5.  Download and install RabbitMQ.

    1.  Download the RabbitMQ installation package.

        ```
        wget -P /root "https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.9/rabbitmq-server-3.6.9-1.el7.noarch.rpm"
        ```

    2.  Import the RabbitMQ signing key.

        ```
        sudo rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
        ```

    3.  Install the RabbitMQ server.

        ```
        cd /root
        sudo yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
        ```

6.  Configure RabbitMQ.

    1.  Set RabbitMQ to run at startup.

        ```
        sudo systemctl enable rabbitmq-server
        ```

    2.  Start RabbitMQ.

        ```
        sudo systemctl start rabbitmq-server
        ```

    3.  To ensure data security, we recommend that you delete the default RabbitMQ user.

        The default username and password of RabbitMQ are both guest.

        ```
        sudo rabbitmqctl delete_user guest
        ```

    4.  Create an administrator user.

        1.  Create a user.

            ```
            sudo rabbitmqctl add_user <Username> <Password>
            ```

        2.  Set the new user as an administrator.

            ```
            sudo rabbitmqctl set_user_tags <Username> administrator
            ```

        3.  Grant all permissions to the new user.

            ```
            sudo rabbitmqctl set_permissions -p / <Username> ". *" ". *" ". *"
            ```

7.  Run the following command to enable the RabbitMQ web management interface:

    ```
    sudo rabbitmq-plugins enable rabbitmq_management
    ```

8.  Enter `http://<Public IP address of the ECS instance>:15672` in the address bar of your browser and press the Enter key.

    The following page indicates that RabbitMQ is installed.

    ![RabbitMQ logon page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7729919951/p39377.png)

9.  Enter the username and password you created and click **Login** to access the RabbitMQ management interface.

    ![RabbitMQ homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7729919951/p39379.png)


