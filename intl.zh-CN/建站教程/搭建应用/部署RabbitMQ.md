# 部署RabbitMQ

本教程介绍如何通过ECS实例部署RabbitMQ。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   已创建网络类型为专有网络的安全组，并且安全组的入方向添加规则并放行80、5672及15672端口，如果您使用SSH远程连接Linux实例，还需要放行22端口。 具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

RabbitMQ是实现了高级消息队列协议（AMQP）的开源消息代理软件，用于在分布式系统中存储转发消息，有良好的易用性、扩展性和高可用性。RabbitMQ使用Erlang语言编写服务器端，并支持多种客户端，如Python、Ruby、.NET、Java、JMS、C、PHP、ActionScript、XMPP和STOMP，同时也支持AJAX。

手动部署：适合对Linux命令有基本了解的用户，能够个性化部署。手动部署使用以下操作系统和软件版本：

-   操作系统：公共镜像CentOS 7.3 64位
-   RabbitMQ版本：rabbitmq-server -3.6.9
-   erlang版本：erlang19.3
-   JDK版本：JDK1.8.0\_121

## 手动部署RabbitMQ

1.  安装依赖包。

    ```
    yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
    ```

2.  安装erlang。

    1.  下载erlang安装包。

        ```
        wget http://erlang.org/download/otp_src_19.3.tar.gz
        ```

    2.  解压缩erlang安装包。

        ```
        tar xzf otp_src_19.3.tar.gz
        ```

    3.  创建一个文件夹。

        ```
        mkdir /usr/local/erlang
        ```

    4.  编译并安装erlang。

        依次执行以下命令。

        ```
        cd otp_src_19.3
        ./configure --prefix=/usr/local/erlang --without-javac
        ```

        ```
        make && make install
        ```

3.  修改profile配置文件。

    1.  运行以下命令打开profile配置文件。

        ```
        vi /etc/profile
        ```

    2.  按下i键，然后在文件末尾处添加如下内容：

        ```
        export PATH=$PATH:/usr/local/erlang/bin
        ```

    3.  按下Esc键，然后输入`:wq`并回车，保存并关闭文件。

4.  生效环境变量并检查。

    1.  运行以下命令使环境变量生效。

        ```
        source /etc/profile
        ```

    2.  运行以下命令检查安装结果。

        ```
        erl -version
        ```

5.  下载并安装RabbitMQ。

    1.  下载RabbitMQ安装包。

        ```
        wget -P /root "https://www.rabbitmq.com/releases/rabbitmq-server/v3.6.9/rabbitmq-server-3.6.9-1.el7.noarch.rpm"
        ```

    2.  导入签名密钥。

        ```
        sudo rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
        ```

    3.  安装RabbitMQ Server。

        ```
        cd /root
        sudo yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
        ```

6.  配置RabbitMQ。

    1.  允许RabbitMQ开机自启动。

        ```
        sudo systemctl enable rabbitmq-server
        ```

    2.  启动RabbitMQ。

        ```
        sudo systemctl start rabbitmq-server
        ```

    3.  为保证数据安全，建议您删除默认用户。

        RabbitMQ默认的账号用户名和密码都是guest。

        ```
        sudo rabbitmqctl delete_user guest
        ```

    4.  创建管理员用户

        1.  创建一个新用户。

            ```
            sudo rabbitmqctl add_user <用户名> <密码>
            ```

        2.  将创建的新用户设置为管理员。

            ```
            sudo rabbitmqctl set_user_tags <用户名> administrator
            ```

        3.  赋予新创建的用户所有权限。

            ```
            sudo rabbitmqctl set_permissions -p / <用户名> ".*" ".*" ".*"
            ```

7.  运行以下命令，启用RabbitMQ的web管理界面。

    ```
    sudo rabbitmq-plugins enable rabbitmq_management
    ```

8.  使用浏览器访问`http://公网IP:15672`。

    显示如下页面，说明RabbitMQ安装成功。

    ![RabbitMQ登录页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0912649951/p39377.png)

9.  输入之前创建的用户名和密码后单击**Login**，进入RabbitMQ管理界面。

    ![RabbitMQ主页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0912649951/p39379.png)


