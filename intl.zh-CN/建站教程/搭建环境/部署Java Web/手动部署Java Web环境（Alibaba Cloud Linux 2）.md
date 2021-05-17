# 手动部署Java Web环境（Alibaba Cloud Linux 2）

本篇教程介绍如何在Alibaba Cloud Linux 2系统的ECS实例上部署Java web项目，适用于刚开始使用阿里云进行建站的个人用户。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。
-   如果在中国内地地域中使用云服务器ECS，请确保账号已完成实名认证。
-   已创建一台ECS实例。详细步骤请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。

本篇教程在示例步骤中使用了以下实例规格和软件版本。操作时，请您以实际软件版本为准。

-   实例规格：ecs.c6.large
-   操作系统：Alibaba Cloud Linux 2.1903 LTS 64位
-   JDK版本：JDK 1.8.0\_262
-   Tomcat版本：8.5.59

    **说明：** 本示例中，使用Tomcat 8.5.59版本为例。源代码版本会不断升级，您可以获取合适的安装包版本。


## 步骤一：准备工作

1.  在安全组入方向添加规则放行所需端口。具体步骤，请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

    本示例中，SSH协议的22端口和HTTP协议的8080端口。

2.  远程连接Linux实例。具体步骤，请参见[通过密码认证登录Linux实例](/intl.zh-CN/实例/连接实例/使用VNC连接实例/通过密码认证登录Linux实例.md)。

3.  关闭防火墙。

    1.  运行systemctl status firewalld命令查看当前防火墙的状态。

        ![查看防火墙状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7712359951/p32172.png)

        -   如果防火墙的状态参数是inactive，则防火墙为关闭状态。
        -   如果防火墙的状态参数是active，则防火墙为开启状态。本示例中防火墙为开启状态，因此需要关闭防火墙。
    2.  关闭防火墙。如果防火墙为关闭状态可以忽略此步骤。

        -   如果您想临时关闭防火墙，运行命令systemctl stop firewalld。

            **说明：** 这只是暂时关闭防火墙，下次重启Linux后，防火墙还会开启。

        -   如果您想永久关闭防火墙，运行命令systemctl disable firewalld。

            **说明：** 如果您想重新开启防火墙，具体操作，请参见[firewalld官网信息](https://firewalld.org/)。

4.  关闭SELinux。

    1.  运行命令getenforce查看SELinux的当前状态。

        ![查看SELinux状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7712359951/p21065.png)

        -   如果SELinux状态参数是Disabled， 则SELinux为关闭状态。
        -   如果SELinux状态参数是Enforcing，则SELinux为开启状态。本示例中SELinux为开启状态，因此需要关闭SELinux。
    2.  关闭SELinux。如果SELinux为关闭状态可以忽略此步骤。

        -   如果您想临时关闭SELinux，运行命令setenforce 0。

            **说明：** 这只是暂时关闭SELinux，下次重启Linux后，SELinux还会开启。

        -   如果您想永久关闭SELinux，运行命令vi /etc/selinux/config编辑SELinux配置文件。回车后，把光标移动到`SELINUX=enforcing`这一行，按`i`键进入编辑模式，修改为`SELINUX=disabled`， 按`Esc`键，然后输入`:wq`并回车来保存并关闭SELinux配置文件。

            **说明：** 如果您想重新开启SELinux，具体操作，请参见[开启或关闭SELinux](/intl.zh-CN/最佳实践/安全/开启或关闭SELinux.md)。

    3.  重启系统使设置生效。

5.  基于安全考虑，创建一般用户www来运行Tomcat。

    ```
    useradd www
    ```

6.  运行以下命令创建网站根目录。

    ```
    mkdir -p /data/wwwroot/default
    ```

7.  将网站根目录的所属用户设置为www。

    ```
    chown -R www.www /data/wwwroot
    ```


## 步骤二：安装JDK1.8

1.  通过yum命令查找JDK1.8软件包。

    ```
    yum -y list java*
    ```

2.  安装列表中的JDK1.8软件包。

    ```
    yum -y install java-1.8.0-openjdk-devel.x86_64
    ```

3.  查看JDK版本。

    ```
    java -version
    ```

    本示例中版本信息如下所示。

    ```
    openjdk version "1.8.0_262"
    OpenJDK Runtime Environment (build 1.8.0_262-b10)
    OpenJDK 64-Bit Server VM (build 25.262-b10, mixed mode)
    ```

4.  配置环境变量。

    1.  打开配置文件。

        ```
        vim /etc/profile
        ```

    2.  在配置文件末尾，按i进入编辑模式。

    3.  添加以下信息。

        **说明：** `JAVA_HOME`值为当前JDK安装的路径。本示例中，运行命令cd /usr/lib/jvm/进入`jvm`路径下，然后运行ls查看JDK安装后文件的路径。

        ```
        JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.1.al7.x86_64
        PATH=$PATH:$JAVA_HOME/bin
        CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
        export JAVA_HOME CLASSPATH PATH
        ```

    4.  按下Esc键，输入`:wq`并回车以保存并关闭文件。

    5.  立即生效环境变量。

        ```
        source /etc/profile
        ```


## 步骤三：安装Apache Tomcat

1.  运行以下命令下载Tomcat 8安装包。

    ```
    wget https://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.59/bin/apache-tomcat-8.5.59.tar.gz
    ```

    **说明：** Tomcat下载地址会更新。新版本的下载地址，请访问[Tomcat官网](https://tomcat.apache.org/)获取。

2.  解压Tomcat 8安装包。

    ```
    tar -zxvf apache-tomcat-8.5.59.tar.gz
    ```

3.  移动Tomcat所在目录。

    ```
    mv apache-tomcat-8.5.59 /usr/local/tomcat/
    ```

4.  将文件的所属用户设置为www。

    ```
    chown -R www.www /usr/local/tomcat/
    ```

    在/usr/local/tomcat/目录下：

    -   bin：存放Tomcat的一些脚本文件，包含启动和关闭Tomcat服务脚本。
    -   conf：存放Tomcat服务器的各种全局配置文件，其中最重要的是server.xml和web.xml。
    -   webapps：Tomcat的主要Web发布目录，默认情况下把Web应用文件放于此目录。
    -   logs：存放Tomcat执行时的日志文件。
5.  配置server.xml文件。

    1.  运行以下命令切换到/usr/local/tomcat/conf/目录。

        ```
        cd /usr/local/tomcat/conf/
        ```

    2.  运行以下命令重命名server.xml文件。

        ```
        mv server.xml server.xml_bk
        ```

    3.  新建一个server.xml文件。

        1.  运行命令`vi server.xml`创建server.xml文件。
        2.  按下i键，添加以下内容。

            ```
            <?xml version="1.0" encoding="UTF-8"?>
            <Server port="8006" shutdown="SHUTDOWN">
            <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
            <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
            <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
            <Listener className="org.apache.catalina.core.AprLifecycleListener"/>
            <GlobalNamingResources>
            <Resource name="UserDatabase" auth="Container"
             type="org.apache.catalina.UserDatabase"
             description="User database that can be updated and saved"
             factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
             pathname="conf/tomcat-users.xml"/>
            </GlobalNamingResources>
            <Service name="Catalina">
            <Connector port="8080"
             protocol="HTTP/1.1"
             connectionTimeout="20000"
             redirectPort="8443"
             maxThreads="1000"
             minSpareThreads="20"
             acceptCount="1000"
             maxHttpHeaderSize="65536"
             debug="0"
             disableUploadTimeout="true"
             useBodyEncodingForURI="true"
             enableLookups="false"
             URIEncoding="UTF-8"/>
            <Engine name="Catalina" defaultHost="localhost">
            <Realm className="org.apache.catalina.realm.LockOutRealm">
            <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
              resourceName="UserDatabase"/>
            </Realm>
            <Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
            <Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
            <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
            prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
            </Host>
            </Engine>
            </Service>
            </Server>
            ```

        3.  按esc键，输入`:wq`并回车以保存并关闭文件。
6.  设置JVM内存参数。

    1.  运行`vi /usr/local/tomcat/bin/setenv.sh`命令创建/usr/local/tomcat/bin/setenv.sh文件。

    2.  按下i键，添加以下内容。

        指定`JAVA_OPTS`参数，用于设置JVM的内存信息以及编码格式。

        ```
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        ```

    3.  按下esc键，输入`:wq`并回车以保存并关闭文件。

7.  设置Tomcat自启动脚本。

    1.  运行以下命令下载Tomcat自启动脚本文件。

        **说明：** 该脚本来源于社区，仅供参考。阿里云对其可靠性以及操作可能带来的潜在影响，不做任何暗示或其他形式的承诺。如果您运行wget命令下载失败，您可以通过浏览器访问`https://raw.githubusercontent.com/oneinstack/oneinstack/master/init.d/Tomcat-init`直接获取脚本内容。

        ```
        wget https://raw.githubusercontent.com/oneinstack/oneinstack/master/init.d/Tomcat-init
        ```

    2.  运行以下命令重命名Tomcat-init。

        ```
        mv Tomcat-init /etc/init.d/tomcat
        ```

    3.  运行以下命令为/etc/init.d/tomcat添加可执行权限。

        ```
        chmod +x /etc/init.d/tomcat
        ```

    4.  运行以下命令设置启动脚本JAVA\_HOME。

        **说明：** 脚本中JDK的路径信息必须与您安装的JDK路径保持一致，否则Tomcat会启动失败。

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.1.al7.x86_64@' /etc/init.d/tomcat
        ```

8.  运行以下命令设置Tomcat开机自启动。

    ```
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

9.  运行以下命令启动Tomcat。

    ```
    service tomcat start             
    ```


## 步骤四：部署测试项目并验证

将需要部署的Java Web项目文件WAR包上传到网站根目录下，并将网站根目录下文件所属用户改为www。您可以使用支持文件传输功能的远程连接工具或搭建FTP站点上传项目文件。本示例中，网站根目录为/data/wwwroot/default，运行以下命令直接在网站根目录下新建一个Tomcat测试页面，并进行访问。

1.  部署测试文件。

    ```
    echo Tomcat test > /data/wwwroot/default/index.jsp
    ```

2.  在本地浏览器地址栏中输入`http://公网IP:8080`进行访问。

    返回页面如下图所示，表示安装成功。

    ![返回结果](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9012649951/p12137.png)


