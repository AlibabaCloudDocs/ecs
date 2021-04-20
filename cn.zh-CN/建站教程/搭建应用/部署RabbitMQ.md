# 部署RabbitMQ

RabbitMQ是实现了高级消息队列协议（AMQP）的开源消息代理软件，用于在分布式系统中存储转发消息，有良好的易用性、扩展性和高可用性。本文介绍如何通过ECS实例部署RabbitMQ。

已创建网络类型为专有网络的安全组，并且在安全组的入方向添加规则并放行80、5672及15672端口，如果您使用SSH远程连接Linux实例，还需要放行22端口。 具体操作，请参见[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。

RabbitMQ使用Erlang语言编写服务器端，并支持多种客户端，如Python、Ruby、.NET、Java、JMS、C、PHP、ActionScript、XMPP和STOMP，同时也支持AJAX。

您可以通过以下两种方式部署RabbitMQ。

-   镜像部署：适合新手使用。具体操作，请参见[镜像部署RabbitMQ](#section_market_image)。
-   手动部署：适合对Linux命令有基本了解的用户，能够个性化部署。具体操作，请参见[手动部署RabbitMQ](#section_gr4_zy1_ffb)。

    手动部署使用以下操作系统和软件版本：

    -   操作系统：公共镜像CentOS 7.8 64位
    -   RabbitMQ版本：3.7.8
    -   erlang版本：21.1
    -   JDK版本：1.8.0\_282
    本文提供的手动部署方式中，RabbitMQ只在当前运行的系统环境下启动，如果您需要设置开机自启动RabbitMQ服务，可以通过云助手实现。具体操作，请参见[通过云助手设置RabbitMQ开机自启动](#section_9ke_67a_pwt)。


## 镜像部署RabbitMQ

完成以下操作，通过镜像部署RabbitMQ：

1.  单击[RabbitMQ环境 \( CentOS7.3 Erlang19.3 \)](https://market.aliyun.com/products/55530001/cmjj017527.html)进入镜像详情页。

    您可以通过镜像详情页获取镜像信息以及使用指南。

2.  单击**立即购买**。

3.  在自定义购买页，**镜像**区域已自动设置为您购买的镜像。根据页面提示，完成配置项并购买ECS实例。

    配置时需注意：

    -   为实例分配公网IPv4地址。
    -   选择前提条件中已配置的安全组。
    -   其他配置您可以按需选择。具体操作，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。
4.  获取ECS实例的公网IP地址。

    1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

    2.  在左侧导航栏，选择**实例与镜像** \> **实例**。

    3.  在顶部菜单栏处，选择目标ECS实例所在地域。

    4.  找到目标ECS实例，在**IP 地址**列获取该实例的公网IP地址。

5.  在浏览器地址栏中输入公网IP地址并回车，下载操作文档。

    ![镜像安装成功页面](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0912649951/p12515.png)

6.  远程连接Linux实例。

    具体操作，请参见[通过密码或密钥认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用Workbench连接实例/通过密码或密钥认证登录Linux实例.md)。

7.  初始化RabbitMQ。

    ```
    cd /root/oneinstack 
    ./init_rabbitmq.sh
    ```

    根据提示与操作文档内容，输入对应的信息：

    1.  输入操作系统主机名并回车。本示例中，使用默认值`rabbit`。
    2.  输入rabbitmq的用户名并回车。
    3.  输入rabbitmq的密码并回车。
    4.  输入y并回车，开始初始化RabbitMQ。
    ![信息输入](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0912649951/p12516.png)

8.  通过浏览器访问`http://ECS实例的公网IP:15672`，进入管理页面。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0912649951/p12517.png)


## 手动部署RabbitMQ

1.  创建并远程连接Linux实例。

    1.  创建实例。

        具体操作，请参见[使用向导创建实例](/cn.zh-CN/实例/创建实例/使用向导创建实例.md)。配置资源时您需要注意：

        -   为实例分配公网IPv4地址。
        -   选择前提条件中已配置的安全组。
        -   其他配置您可以按需选择。
    2.  远程连接实例。

        具体操作，请参见[通过密码或密钥认证登录Linux实例](/cn.zh-CN/实例/连接实例/使用Workbench连接实例/通过密码或密钥认证登录Linux实例.md)。

2.  安装erlang。

    1.  运行以下命令，安装erlang所需要的依赖包。

        ```
        yum install -y make gcc gcc-c++ m4 openssl openssl-devel ncurses-devel unixODBC unixODBC-devel java java-devel
        ```

    2.  运行以下命令，下载erlang安装包。

        ```
        wget http://erlang.org/download/otp_src_21.1.tar.gz
        ```

    3.  运行以下命令，解压erlang安装包。

        ```
        tar -zxvf otp_src_21.1.tar.gz
        ```

    4.  运行以下命令，进入erlang安装包的解压路径，并为erlang创建一个新的目录。

        ```
        cd otp_src_21.1
        mkdir -p /usr/local/erlang
        ```

    5.  依次运行以下命令，编译并安装erlang。

        ```
        ./configure --prefix=/usr/local/erlang
        ```

        ```
        make && make install
        ```

    6.  安装完成后，运行以下命令，为erlang配置环境变量。

        ```
        echo 'export PATH=$PATH:/usr/local/erlang/bin' >> /etc/profile
        ```

    7.  运行以下命令，使环境变量立即生效。

        ```
        source /etc/profile
        ```

    8.  运行以下命令，返回系统的/root目录，然后查看erlang版本，确认是否安装成功。

        ```
        cd
        erl -version
        ```

        返回如下信息表示erlang已成功安装。

        ![erl version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9845938161/p263785.png)

3.  下载并安装RabbitMQ。

    RabbitMQ对Erlang的版本具有一定限制，更多信息，请参见[RabbitMQ Erlang Version Requirements](https://www.rabbitmq.com/which-erlang.html)。本示例使用的Erlang为21.1版本，因此选择下载RabbitMQ 3.7.8版本。

    1.  运行以下命令，下载RabbitMQ安装包。

        ```
        wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.8/rabbitmq-server-generic-unix-3.7.8.tar.xz
        ```

    2.  运行以下命令，解压RabbitMQ安装包。

        ```
        tar -xvf rabbitmq-server-generic-unix-3.7.8.tar.xz
        ```

    3.  解压完成后，运行以下命令，为RabbitMQ配置环境变量。

        ```
        echo 'export PATH=$PATH:/root/rabbitmq_server-3.7.8/sbin' >> /etc/profile
        ```

    4.  运行以下命令，使环境变量立即生效。

        ```
        source /etc/profile
        ```

4.  配置RabbitMQ。

    1.  运行以下命令，启动RabbitMQ并后台运行。

        ```
        rabbitmq-server -detached
        ```

        **说明：** 该命令只在当前运行的系统环境下启动RabbitMQ，一旦服务器重启，RabbitMQ服务将不会自动启动。因此，建议您通过阿里云的云助手功能，设置RabbitMQ开机自启动。具体操作，请参见[通过云助手设置RabbitMQ开机自启动](#section_9ke_67a_pwt)。

    2.  运行以下命令，启动RabbitMQ监控插件。

        ```
        rabbitmq-plugins enable rabbitmq_management
        ```

        如果您需要关闭RabbitMQ监控插件，可以运行`rabbitmq-plugins disable rabbitmq_management`命令。

    3.  为保证数据安全，建议您运行以下命令，删除默认用户。

        RabbitMQ默认的账号用户名和密码都是`guest`。

        ```
        rabbitmqctl delete_user guest
        ```

    4.  创建RabbitMQ管理员用户。

        1.  运行以下命令，创建一个新用户。

            ```
            rabbitmqctl add_user <用户名\> <密码\>
            ```

            其中，<用户名\>和<密码\>为您自定义的信息。

        2.  运行以下命令，将创建的新用户设置为管理员。

            ```
            rabbitmqctl set_user_tags <用户名\> administrator
            ```

        3.  运行以下命令，赋予新创建的用户所有权限。

            ```
            rabbitmqctl set_permissions -p / <用户名\> ".*" ".*" ".*"
            ```

5.  在本地主机中，使用浏览器访问`Linux实例的公网IP:15672`。

    显示如下页面，说明RabbitMQ安装成功。

    ![RabbitMQ登录页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9845938161/p39377.png)

6.  输入已创建的RabbitMQ管理员用户名和密码后，单击**Login**，进入RabbitMQ管理界面。

    RabbitMQ管理界面展示信息如下所示：

    ![RabbitMQ主页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9845938161/p39379.png)


## 通过云助手设置RabbitMQ开机自启动

1.  配置RabbitMQ的rabbitmq-server文件。

    1.  运行以下命令，编辑rabbitmq-server文件。

        ```
        vim /root/rabbitmq_server-3.7.8/sbin/rabbitmq-server
        ```

    2.  按下shift+:组合键，然后输入`set nu`查看文件的行号。

    3.  按下shift+:组合键，然后输入`189`跳转至189行。

    4.  按下i键，进入编辑模式。

        在189行新增以下内容：

        ```
        export PATH=$PATH:/usr/local/erlang/bin
        export HOME=/root/rabbitmq_server-3.7.8/
        ```

        配置完成后，如下图所示。

        ![rabbitmq-server](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9845938161/p263925.png)

    5.  按下Esc键，然后输入`:wq`并回车，保存退出文件。

2.  调用ECS API [RunCommand](/cn.zh-CN/API参考/云助手/RunCommand.md)，设置RabbitMQ开机自启动。

    调用API的具体操作，请参见[快速入门](/cn.zh-CN/API参考/快速入门.md)。设置RabbitMQ开机自启动，您必须设置以下参数：

    |参数|说明|取值或示例值|
    |--|--|------|
    |RegionId|ECS实例所在的地域ID。|示例值：`cn-hangzhou`|
    |Name|云助手命令的名称。|示例值：`start-rabbitmq`|
    |Type|运维命令的语言类型。|取值：`RunShellScript`|
    |CommandContent|命令的明文内容。|取值：`/root/rabbitmq_server-3.7.8/sbin/rabbitmq-server -detached`**说明：** 该命令用于启动RabbitMQ。 |
    |RepeatMode|设置命令执行的方式。|取值：`EveryReboot`|
    |InstanceId.N|部署RabbitMQ的ECS实例ID。|示例值：`i-bp12f1b0i3r7adm3****`|

    调用成功的JSON返回示例值如下所示，后续当您重启ECS实例后，都会触发启动RabbitMQ的云助手命令。

    ```
    {
      "RequestId": "8B4BFE47-F1E3-48D1-B405-CA783B697046",
      "CommandId": "c-hz01gvo1ri9****",
      "InvokeId": "t-hz01gvo1rig****"
    }
    ```


