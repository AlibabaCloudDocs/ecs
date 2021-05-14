# Deploy RabbitMQ

RabbitMQ is an open source message broker that implements the Advanced Message Queuing Protocol \(AMQP\) to store and forward messages in a distributed system. RabbitMQ is easy to use, scalable, and highly available. This topic describes how to deploy RabbitMQ on an Elastic Compute Service \(ECS\) instance.

A security group of the virtual private cloud \(VPC\) type is created. An inbound rule that allows traffic on ports 80, 5672, and 15672 is added to the security group. If you want to connect to a Linux instance in the security group by using Secure Shell \(SSH\), you must configure the rule to allow traffic on port 22. For more information, see [Add security group rules](/intl.en-US/Security/Security groups/Add security group rules.md).

The RabbitMQ server is written in the Erlang programming language. RabbitMQ supports multiple types of clients such as Python, Ruby, .NET, Java, Java Message Service \(JMS\), C, Professional Hypertext Preprocessor \(PHP\), ActionScript, Extensible Messaging and Presence Protocol \(XMPP\), Simple Text Oriented Messaging Protocol \(STOMP\), and Asynchronous JavaScript and XML \(AJAX\).

Manually deploy RabbitMQ. This method is suitable for users who have a basic knowledge of Linux commands and can perform personalized deployment. Use the following operating system and software versions to manually deploy RabbitMQ:

-   Operating system: CentOS 7.8 64-bit public image
-   RabbitMQ: RabbitMQ 3.7.8
-   Erlang: Erlang 21.1
-   JDK: JDK 1.8.0\_282

## Manually deploy RabbitMQ

1.  Create and connect to a Linux instance.

    1.  Create a Linux instance.

        For more information, see [Create an instance by using the wizard](/intl.en-US/Instance/Create an instance/Create an instance by using the wizard.md). When you configure parameters to create the instance, take note of the following items:

        -   Select Assign Public IPv4 Address in the Public IP Address section in the Networking step.
        -   Select the security group configured in the "Prerequisites" section.
        -   Complete other settings.
    2.  Connect to the instance.

        For more information, see [Connect to a Linux instance by using password authentication](/intl.en-US/Instance/Connect to instances/Connect to an instance by using VNC/Connect to a Linux instance by using password authentication.md).

2.  Install Erlang.

    1.  Run the following command to install the dependency for Erlang:

        ```
        yum install -y make gcc gcc-c++ m4 openssl openssl-devel ncurses-devel unixODBC unixODBC-devel java java-devel
        ```

    2.  Run the following command to download the Erlang installation package:

        ```
        wget http://erlang.org/download/otp_src_21.1.tar.gz
        ```

    3.  Run the following command to decompress the Erlang installation package:

        ```
        tar -zxvf otp_src_21.1.tar.gz
        ```

    4.  Run the following commands to go to the path to which the Erlang installation package is decompressed and create a directory for Erlang:

        ```
        cd otp_src_21.1
        mkdir -p /usr/local/erlang
        ```

    5.  Run the following commands in sequence to compile and install Erlang:

        ```
        ./configure --prefix=/usr/local/erlang
        ```

        ```
        make && make install
        ```

    6.  After Erlang is installed, run the following command to configure the environment variable for Erlang:

        ```
        echo 'export PATH=$PATH:/usr/local/erlang/bin' >> /etc/profile
        ```

    7.  Run the following command to apply the configured environment variable:

        ```
        source /etc/profile
        ```

    8.  Run the following commands to go back to the /root directory. View the Erlang version to check whether Erlang is installed.

        ```
        cd
        erl -version
        ```

        A command output similar to the following one indicates that Erlang is installed.

        ![erl version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3161690261/p263785.png)

3.  Download and install RabbitMQ.

    Different RabbitMQ versions are compatible with different Erlang versions. For more information, see [RabbitMQ Erlang Version Requirements](https://www.rabbitmq.com/which-erlang.html). In this example, Erlang 21.1 is used, and you must download RabbitMQ 3.7.8.

    1.  Run the following command to download the RabbitMQ installation package:

        ```
        wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.8/rabbitmq-server-generic-unix-3.7.8.tar.xz
        ```

    2.  Run the following command to decompress the RabbitMQ installation package:

        ```
        tar -xvf rabbitmq-server-generic-unix-3.7.8.tar.xz
        ```

    3.  After the package is decompressed, run the following command to configure the environment variable for RabbitMQ:

        ```
        echo 'export PATH=$PATH:/root/rabbitmq_server-3.7.8/sbin' >> /etc/profile
        ```

    4.  Run the following command to apply the configured environment variable:

        ```
        source /etc/profile
        ```

4.  Configure RabbitMQ.

    1.  Run the following command to start RabbitMQ and run RabbitMQ in the background:

        ```
        rabbitmq-server -detached
        ```

        **Note:** This command starts RabbitMQ only in the current runtime environment. If the instance restarts, RabbitMQ does not automatically start. We recommend that you use Cloud Assistant to configure RabbitMQ to automatically start on instance startup. For more information, see [Use Cloud Assistant to Configure RabbitMQ to automatically start on instance startup](#section_9ke_67a_pwt).

    2.  Run the following command to enable the RabbitMQ monitoring plug-in:

        ```
        rabbitmq-plugins enable rabbitmq_management
        ```

        To disable the RabbitMQ monitoring plug-in, you can run the `rabbitmq-plugins disable rabbitmq_management` command.

    3.  To ensure data security, we recommend that you run the following command to delete the default user of RabbitMQ.

        The default username and password of RabbitMQ are both `guest`.

        ```
        rabbitmqctl delete_user guest
        ```

    4.  Create a RabbitMQ administrator user.

        1.  Run the following command to create a user:

            ```
            rabbitmqctl add_user <Username\> <Password\>
            ```

            Specify the <Username\> and <Password\> parameters.

        2.  Run the following command to set the new user as an administrator:

            ```
            rabbitmqctl set_user_tags <Username\> administrator
            ```

        3.  Run the following command to grant all permissions to the new user:

            ```
            rabbitmqctl set_permissions -p / <Username\> ".*" ".*" ".*"
            ```

5.  Access `<Public IP address of the Linux instance>:15672` in a browser on your computer.

    The following page indicates that RabbitMQ is installed.

    ![RabbitMQ logon page](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0701779161/p39377.png)

6.  Enter the username and password of the RabbitMQ administrator user that you created and click **Login** to access the RabbitMQ management interface.

    The RabbitMQ management interface appears, as shown in the following figure.

    ![RabbitMQ homepage](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/0701779161/p39379.png)


## Use Cloud Assistant to Configure RabbitMQ to automatically start on instance startup

1.  Configure the rabbitmq-server file for RabbitMQ.

    1.  Run the following command to edit the rabbitmq-server file:

        ```
        vim /root/rabbitmq_server-3.7.8/sbin/rabbitmq-server
        ```

    2.  Press shift+: and enter `set nu` to view line numbers of the file.

    3.  Press shift+: and enter `189` to go to Line 189.

    4.  Press the I key to enter the edit mode.

        Add the following content to Line 189:

        ```
        export PATH=$PATH:/usr/local/erlang/bin
        export HOME=/root/rabbitmq_server-3.7.8/
        ```

        The following figure shows the lines after the content is added.

        ![rabbitmq-server](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3161690261/p263925.png)

    5.  Press the Esc key, enter `:wq`, and then press the Enter key to save and close the file.

2.  Call the ECS API [RunCommand](/intl.en-US/API Reference/Cloud assistant/RunCommand.md) operation to configure RabbitMQ to automatically start on instance startup.

    For more information, see [Quick start](/intl.en-US/API Reference/Quick start.md). To configure RabbitMQ to automatically start on instance startup, you must configure the parameters listed in the following table.

    |Parameter|Description|Valid or example value|
    |---------|-----------|----------------------|
    |RegionId|The region ID of the instance.|Example: `cn-hangzhou`.|
    |Name|The name of the Cloud Assistant command.|Example: `start-rabbitmq`.|
    |Type|The language type of the command.|Set the value to `RunShellScript`.|
    |CommandContent|The plaintext content of the command.|Set the value to `/root/rabbitmq_server-3.7.8/sbin/rabbitmq-server -detached`.**Note:** The command is used to start RabbitMQ. |
    |RepeatMode|Specifies how to run the command.|Set the value to `EveryReboot`.|
    |InstanceId.N|The ID of the instance where RabbitMQ is deployed.|Example: `i-bp12f1b0i3r7adm3****`.|

    The following code shows a sample success response in the JSON format. Subsequently, the command used to start RabbitMQ is triggered every time you restart the instance.

    ```
    {
      "RequestId": "8B4BFE47-F1E3-48D1-B405-CA783B697046",
      "CommandId": "c-hz01gvo1ri9****",
      "InvokeId": "t-hz01gvo1rig****"
    }
    ```


