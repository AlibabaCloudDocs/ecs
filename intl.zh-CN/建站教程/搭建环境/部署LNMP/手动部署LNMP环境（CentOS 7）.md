---
keyword: [LNMP, CentOS 7, Nginx, MySQL, PHP7]
---

# 手动部署LNMP环境（CentOS 7）

Nginx是一款小巧而高效的Web服务器软件，可帮您在Linux系统下快速方便地搭建出LNMP Web服务环境。本教程介绍如何手动在ECS实例上搭建LNMP环境，其中LNMP分别代表Linux、Nginx、MySQL和PHP。

-   已创建ECS实例并为实例分配公网IP地址，具体操作请参见[创建方式导航](/intl.zh-CN/实例/创建实例/创建方式导航.md)。
-   已在实例安全组的入方向添加安全组规则并放行22、80、443端口。具体操作请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。

    **说明：** 基于服务器数据安全考虑，本文仅说明部署与测试LNMP环境所必须放行的端口，您可以根据实际需求，放行其他应用所需的端口号。例如，远程连接MySQL数据库时，需要放行MySQL默认占用的3306端口。


本教程适用于熟悉Linux操作系统，刚开始使用阿里云进行建站的个人用户。

您也可以在[云市场](https://marketplace.alibabacloud.com/)购买LNMP镜像直接启动ECS实例，以便快速建站。

本篇教程在示例步骤中使用了以下配置的ECS实例。实际操作时，请以您的实例配置为准。

-   实例规格：ecs.c6.large
-   CPU：2 vCPU
-   内存：4GiB
-   操作系统：公共镜像CentOS 7.2 64位
-   网络类型：专有网络VPC
-   IP地址：公网IP

示例步骤将使用以下软件版本：

-   Nginx版本：Nginx 1.16.1
-   MySQL版本：MySQL 5.7.28
-   PHP版本：PHP 7.0.33

**说明：** 当您使用不同软件版本时，可能需要根据实际情况调整命令和参数配置。

## 步骤一：准备编译环境

1.  远程连接Linux实例。

2.  关闭防火墙。

    1.  运行systemctl status firewalld命令查看当前防火墙的状态。

        ![查看防火墙状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7712359951/p32172.png)

        -   如果防火墙的状态参数是inactive，则防火墙为关闭状态。
        -   如果防火墙的状态参数是active，则防火墙为开启状态。本示例中防火墙为开启状态，因此需要关闭防火墙。
    2.  关闭防火墙。如果防火墙为关闭状态可以忽略此步骤。

        -   如果您想临时关闭防火墙，运行命令systemctl stop firewalld。

            **说明：** 这只是暂时关闭防火墙，下次重启Linux后，防火墙还会开启。

        -   如果您想永久关闭防火墙，运行命令systemctl disable firewalld。

            **说明：** 如果您想重新开启防火墙，请参见[firewalld官网信息](https://firewalld.org/)。

3.  关闭SELinux。

    1.  运行getenforce命令查看SELinux的当前状态。

        ![查看SELinux状态](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7712359951/p21065.png)

        -   如果SELinux状态参数是Disabled，则SELinux为关闭状态。
        -   如果SELinux状态参数是Enforcing，则SELinux为开启状态。本示例中SELinux为开启状态，因此需要关闭SELinux。
    2.  关闭SELinux。如果SELinux为关闭状态可以忽略此步骤。

        -   如果您想临时关闭SELinux，运行命令setenforce 0。

            **说明：** 这只是暂时关闭SELinux，下次重启Linux后，SELinux还会开启。

        -   如果您想永久关闭SELinux，运行命令vim /etc/selinux/config编辑SELinux配置文件。回车后，把光标移动到`SELINUX=enforcing`这一行，按i键进入编辑模式，修改为`SELINUX=disabled`，按Esc键，然后输入:wq并按Enter键以保存并关闭SELinux配置文件。 最后重启系统使设置生效。

            **说明：** 如果您想重新开启SELinux，请参见[开启或关闭SELinux](/intl.zh-CN/最佳实践/安全/开启或关闭SELinux.md)。


## 步骤二：安装Nginx

**说明：** 本教程只提供一个版本的Nginx作为示例，如果您需要安装其他版本的Nginx，请参见[常见问题](#section_0ho_omf_0ct)。

1.  运行以下命令安装Nginx。

    ```
    yum -y install nginx
    ```

2.  运行以下命令查看Nginx版本。

    ```
    nginx -v
    ```

    返回结果如下所示，表示Nginx安装成功。

    ```
    nginx version: nginx/1.16.1
    ```


## 步骤三：安装MySQL

1.  运行以下命令更新YUM源。

    ```
    rpm -Uvh  http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
    ```

2.  运行以下命令安装MySQL。

    **说明：** 如果您使用的操作系统内核版本为el8，可能会提示报错信息No match for argument。您需要先运行命令yum module disable mysql禁用默认的mysql模块，再安装MySQL。

    ```
    yum -y install mysql-community-server
    ```

3.  运行以下命令查看MySQL版本号。

    ```
    mysql -V
    ```

    返回结果如下所示，表示MySQL安装成功。

    ```
    mysql  Ver 14.14 Distrib 5.7.28, for Linux (x86_64) using  EditLine wrapper
    ```

4.  运行以下命令启动MySQL。

    ```
    systemctl start mysqld
    ```

5.  运行以下命令设置开机启动MySQL。

    ```
    systemctl enable mysqld
    systemctl daemon-reload
    ```


## 步骤四：安装PHP

1.  更新YUM源。

    1.  运行以下命令添加epel源。

        ```
        yum install \
        https://repo.ius.io/ius-release-el7.rpm \
        https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
        ```

    2.  运行以下命令添加Webtatic源。

        ```
        rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
        ```

2.  运行以下命令安装PHP。

    ```
    yum -y install php70w-devel php70w.x86_64 php70w-cli.x86_64 php70w-common.x86_64 php70w-gd.x86_64 php70w-ldap.x86_64 php70w-mbstring.x86_64 php70w-mcrypt.x86_64  php70w-pdo.x86_64   php70w-mysqlnd  php70w-fpm php70w-opcache php70w-pecl-redis php70w-pecl-mongodb
    ```

3.  运行以下命令查看PHP版本。

    ```
    php -v
    ```

    返回结果如下所示，表示安装成功。

    ```
    PHP 7.0.33 (cli) (built: Dec  6 2018 22:30:44) ( NTS )
    Copyright (c) 1997-2017 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
        with Zend OPcache v7.0.33, Copyright (c) 1999-2017, by Zend Technologies                
    ```


## 步骤五：配置Nginx

1.  运行以下命令备份Nginx配置文件。

    ```
    cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
    ```

2.  修改Nginx配置文件，添加Nginx对PHP的支持。

    **说明：** 若不添加此配置信息，后续您使用浏览器访问PHP页面时，页面将无法显示。

    1.  运行以下命令打开Nginx配置文件。

        ```
        vim /etc/nginx/nginx.conf
        ```

    2.  按i进入编辑模式。

    3.  在`server`大括号内，修改或添加下列配置信息。

        ```
                #除下面提及的需要添加的配置信息外，其他配置保持默认值即可。
                #将location / 大括号内的信息修改为以下所示，配置网站被访问时的默认首页。
                location / {
                    index index.php index.html index.htm;
                }
        ```

        ```
                #添加下列信息，配置Nginx通过fastcgi方式处理您的PHP请求。
                location ~ .php$ {
                    root /usr/share/nginx/html;    #将/usr/share/nginx/html替换为您的网站根目录，本教程使用/usr/share/nginx/html作为网站根目录。
                    fastcgi_pass 127.0.0.1:9000;   #Nginx通过本机的9000端口将PHP请求转发给PHP-FPM进行处理。
                    fastcgi_index index.php;
                    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                    include fastcgi_params;   #Nginx调用fastcgi接口处理PHP请求。
                }                
        ```

        添加配置信息后，如下图所示。

        ![nginx-configuration](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7902649951/p69697.png)

    4.  按下Esc键后，输入:wq并回车以保存并关闭配置文件。

3.  运行以下命令启动Nginx服务。

    ```
    systemctl start nginx 
    ```

4.  运行以下命令设置Nginx服务开机自启动。

    ```
    systemctl enable nginx
    ```


## 步骤六：配置MySQL

1.  运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码。

    ```
    grep 'temporary password' /var/log/mysqld.log
    ```

    返回结果如下：

    ```
    2016-12-13T14:57:47.535748Z 1 [Note] A temporary password is generated for root@localhost: p0/G28g>lsHD
    ```

    **说明：** 下一步重置root用户密码时，会使用该初始密码。

2.  运行以下命令配置MySQL的安全性。

    ```
    mysql_secure_installation
    ```

    安全性的配置包含以下五个方面：

    1.  重置root账号密码。

        ```
        Enter password for user root: #输入上一步获取的root用户初始密码
        The 'validate_password' plugin is installed on the server.
        The subsequent steps will run with the existing configuration of the plugin.
        Using existing password for root.
        Estimated strength of the password: 100 
        Change the password for root ? (Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
        New password: #输入新密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
        Re-enter new password: #再次输入新密码
        Estimated strength of the password: 100 
        Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
        ```

    2.  输入Y删除匿名用户账号。

        ```
        By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
        Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  #是否删除匿名用户，输入Y
        Success.
        ```

    3.  输入Y禁止root账号远程登录。

        ```
        Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
        Success.
        ```

    4.  输入Y删除test库以及对test库的访问权限。

        ```
        Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
        - Dropping test database...
        Success.
        ```

    5.  输入Y重新加载授权表。

        ```
        Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
        Success.
        All done!
        ```


更多信息，请参见[MySQL文档](http://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。

## 步骤七：配置PHP

1.  新建phpinfo.php文件，用于展示PHP信息。

    1.  运行以下命令新建文件。

        ```
        vim <网站根目录>/phpinfo.php  #将`<网站根目录>`替换为您配置的网站根目录。
        ```

        网站根目录是您在nginx.conf文件中`location ~ .php$`大括号内配置的`root`值，如下图所示。

        ![lnmp-root-dir](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7902649951/p69633.png)

        本教程配置的网站根目录为/usr/share/nginx/html，因此命令为：

        ```
        vim /usr/share/nginx/html/phpinfo.php
        ```

    2.  按i进入编辑模式。

    3.  输入下列内容，函数`phpinfo()`​会展示PHP的所有配置信息。

        ```
        <?php echo phpinfo(); ?>
        ```

    4.  按Esc键后，输入:wq并回车以保存并关闭配置文件。

2.  运行以下命令启动PHP-FPM。

    ```
    systemctl start php-fpm
    ```

3.  运行以下命令设置PHP-FPM开机自启动。

    ```
    systemctl enable php-fpm
    ```


## 步骤八：测试访问LNMP平台

1.  打开浏览器。

2.  在地址栏输入`http://<ECS实例公网IP地址>/phpinfo.php`。

    返回结果如下图所示，表示LNMP环境部署成功。

    ![LNMP部署成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7902649951/p44922.png)


## 后续步骤

测试访问LNMP平台成功后，建议您运行以下命令将phpinfo.php文件删除，消除安全隐患。

```
rm -rf <网站根目录>/phpinfo.php   #将<网站根目录>替换为您在nginx.conf中配置的网站根目录
```

本教程配置的网站根目录为/usr/share/nginx/html，因此命令为：

```
rm -rf /usr/share/nginx/html/phpinfo.php
```

## 常见问题

如何使用其它版本的Nginx服务器？

1.  使用浏览器访问[Nginx开源社区](http://nginx.org/en/download.html)获取对应的Nginx版本的下载链接。

    请根据您的个人需求，选择对应的Nginx版本。本章节以Nginx 1.8.1为例。

2.  远程连接需要部署LNMP环境的ECS实例。
3.  运行wget命令下载Nginx 1.8.1。

    您可以通过Nginx开源社区直接获取对应版本的安装包URL，然后通过`wget URL`的方式将Nginx安装包下载至ECS实例。例如，Nginx 1.8.1的下载命令如下：

    ```
    wget http://nginx.org/download/nginx-1.8.1.tar.gz
    ```

4.  运行以下命令，安装Nginx相关依赖。

    ```
    yum install -y gcc-c++
    yum install -y pcre pcre-devel
    yum install -y zlib zlib-devel
    yum install -y openssl openssl-devel
    ```

5.  运行以下命令，解压Nginx 1.8.1安装包，然后进入Nginx所在的文件夹。

    ```
    tar zxvf nginx-1.8.1.tar.gz
    cd nginx-1.8.1
    ```

6.  依次运行以下命令，编译源码。

    ```
    ./configure \
     --user=nobody \
     --group=nobody \
     --prefix=/usr/local/nginx \
     --with-http_stub_status_module \
     --with-http_gzip_static_module \
     --with-http_realip_module \
     --with-http_sub_module \
     --with-http_ssl_module
    ```

    ```
    make && make install
    ```

7.  运行以下命令，进入Nginx的sbin目录，然后启动Nginx。

    ```
    cd /usr/local/nginx/sbin/
    ./nginx
    ```

8.  在本地主机中，使用浏览器访问`ECS实例公网IP`。

    出现如下图所示的页面，表示Nginx已成功安装并启动。

    ![nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7825911161/p228426.png)


