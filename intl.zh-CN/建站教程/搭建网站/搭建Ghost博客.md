# 搭建Ghost博客

Ghost是一个基于Node.js开发的免费开源博客平台，用于简化个人博客和在线出版物的在线发布过程。本文介绍了在CentOS 7操作系统的ECS实例上部署Ghost博客的详细步骤。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.alibabacloud.com/register/intl_register.htm)。

随着业务的扩展，您可以使用阿里云的产品平台，平滑地横向和纵向扩展服务容量，例如：

-   扩展单个ECS实例的CPU和内存规格，增强服务器的处理能力。
-   增加多台ECS实例，并利用负载均衡，在多个实例中进行负载的均衡分配。
-   利用弹性伸缩（Auto Scaling），根据业务量自动增加或减少ECS实例的数量。
-   利用对象存储OSS（Object Storage Service），存储静态网页和海量图片、视频等。

本文将使用一台实例规格为ecs.c6.large的ECS实例搭建Ghost博客，适用于初次使用阿里云进行建站的个人用户。

**说明：** 搭建Ghost博客分为开发模式（development）和生产模式（production），建议您在第一次搭建Ghost博客时使用开发模式，方便对Ghost博客的调试。

## 操作步骤

使用云服务器ECS搭建Ghost网站的操作步骤如下：

-   [步骤一：创建Linux实例](#section_lll_v4o_d8l)
-   [步骤二：部署Web环境](#section_3as_stl_g30)
-   [步骤三：安装Ghost](#section_ab9_fr6_oj6)
-   [步骤四：购买域名](#section_vhr_y2k_pga)
-   [步骤五：备案](#section_6ph_sb6_rb4)
-   [步骤六：配置域名解析](#section_b35_s43_byu)

## 步骤一：创建Linux实例

本节介绍如何创建实例。对于个人使用的小型网站，一台ECS实例可以满足基本需求。

-   创建一台Linux实例。具体步骤，请参见[使用向导创建实例](/intl.zh-CN/实例/创建实例/使用向导创建实例.md)。
-   如果您有镜像，也可以使用自定义镜像创建实例。具体操作，请参见[使用自定义镜像创建实例](/intl.zh-CN/实例/创建实例/使用自定义镜像创建实例.md)。

在配置参数时，您需要注意以下几点：

-   **实例**：对于个人网站，实例规格为**1vCPU 2GiB**或**2vCPU 4GiB**就能满足基本需求。关于实例规格的详细介绍，请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。
-   **网络**：选择**专有网络**。
-   **公网带宽**：本文选择**分配公网IPv4地址**。如果不选中，表示不为实例分配公网IP地址。ECS实例如需访问公网，需要配置并绑定弹性公网IP地址。请根据实际需求进行选择。
-   **镜像**：本文选择公共镜像中的Linux操作系统，例如：CentOS 7.2 64位。

实例创建完成后，您会收到短信和邮件通知，告知您的实例名称、公网IP地址、内网IP地址等信息。您可以使用这些信息登录并管理实例。

很多重要信息都是通过绑定手机的短信接收，并且重要的操作（例如重启、停止等）都需要手机接收验证码，因此请务必保持绑定手机通信畅通。

## 步骤二：部署Web环境

本节以安装Nginx为例介绍如何部署Web环境。

部署Web环境之前，请确认以下信息：

-   您的实例可以连接公网。
-   已安装用于连接Linux实例的工具，例如：SecureCRT。

1.  打开SecureCRT ，设置登录实例所需的信息。

    1.  设置连接名称。

    2.  协议选择**SSH**。

    3.  输入主机IP地址和用户。

    4.  单击**确定**保存。

    ![设置登录信息](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p12471.png)

2.  输入用户名root和登录密码。

    ![输入用户名密码](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p12472.png)

3.  添加Nginx软件库。

    ```
    rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

    软件包中包含的软件及版本为：nginx/1.10.2

    **说明：** 您下载的版本可能与此不同，请以实际情况为准。

4.  安装Nginx。

    ```
    yum -y install nginx
    ```

5.  设置Nginx服务器自动启动。

    ```
    systemctl enable nginx.service
    ```

6.  启动Nginx并查看Nginx服务状态。

    ```
    systemctl start nginx.service
    systemctl status nginx.service
    ```

7.  在浏览器中输入IP地址，可以看到默认的Nginx网页。

    ![nginx网页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p12474.png)


## 步骤三：安装Ghost

1.  更新系统。确保您的服务器系统处于最新状态。

    ```
    yum -y update
    ```

2.  安装Node.js。

    1.  安装EPEL。

        ```
        yum install epel-release -y
        ```

    2.  安装Node.js和npm。

        ```
        yum install nodejs npm --enablerepo=epel
        ```

    3.  安装node.js管理工具。

        ```
        npm install -g n
        ```

    4.  安装稳定版本的node.js。

        本示例安装node.js的版本为`12.16.3`。

        ```
        n 12.16.3
        ```

    5.  运行命令n，选择已安装的node.js 12.16.3版本。

    6.  编辑环境配置文件。

        ```
        vim ~/.bash_profile
        ```

    7.  按i进入编辑模式，在文件末尾添加下列信息。

        ```
        export N_PREFIX=/usr/local/bin/node
        export PATH=$N_PREFIX/bin:$PATH
        ```

        编辑完成后按esc键，输入`:wq`保存并退出文件。

    8.  执行以下命令使配置生效。

        ```
        source ~/.bash_profile
        ```

    9.  安装进程管理器，来控制Node.js应用程序。

        进程管理器可以保持应用程序一直处于运行状态。

        ```
        npm install pm2 -g
        ```

    10. 运行`node -v`和`npm -v`命令，检查Node.js的版本。

3.  安装Ghost。

    1.  创建Ghost安装目录。

        ```
        mkdir -p /var/www/ghost
        ```

    2.  进入Ghost安装目录，下载最新版本的Ghost安装包。

        ```
        cd /var/www/ghost
        wget https://ghost.org/zip/ghost-latest.zip
        mv ghost-latest.zip ghost.zip
        ```

    3.  解压Ghost安装包。

        ```
        yum install unzip -y
        unzip ghost.zip
        ```

    4.  安装gcc和c++编译器。

        ```
        yum -y install gcc gcc-c++
        ```

    5.  使用npm安装Ghost。

        ```
        npm install -production
        ```

    6.  运行`npm start`命令启动Ghost，检查是否安装成功。

        启动成功示例如下，您可以按Ctrl+C组合键关闭Ghost。

        ```
        [2020-04-13 04:00:01] INFO Ghost is running in development...
        [2020-04-13 04:00:01] INFO Listening on: 127.0.0.1:2368
        [2020-04-13 04:00:01] INFO Url configured as: http://121.196.*.*/
        [2020-04-13 04:00:01] INFO Ctrl+C to shut down
        [2020-04-13 04:00:01] INFO Ghost boot 2.185s
        ```

    7.  修改/var/www/ghost/core/shared/config/env目录下的config.development.json文件。

        ```
        vi /var/www/ghost/core/shared/config/env/config.development.json
        ```

    8.  配置config.development.json文件中的URL为Ghost博客的域名。

        ![ghost1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p98140.png)

        按下esc退出编辑模式，并输入`:wq`保存并退出。

4.  配置Nginx作为Ghost的反向代理。

    1.  进入Nginx配置目录。

        ```
        cd /etc/nginx/conf.d/
        ```

    2.  新建Ghost博客的Nginx配置文件。

        ```
        vim /etc/nginx/conf.d/ghost.conf
        ```

    3.  将以下内容输入到ghost.conf中，把server\_name改成Ghost实际的域名。

        ```
        upstream ghost {
            server 127.0.0.1:2368;
        }
        server {
            listen      80;
            server_name myghostblog.com;
        
            access_log  /var/log/nginx/ghost.access.log;
            error_log   /var/log/nginx/ghost.error.log;
        
            proxy_buffers 16 64k;
            proxy_buffer_size 128k;
        
            location / {
                proxy_pass  http://ghost;
                proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
                proxy_redirect off;
        
                proxy_set_header    Host            $host;
                proxy_set_header    X-Real-IP       $remote_addr;
                proxy_set_header    X-Forwarded-For $proxy_add_X_forwarded_for;
                proxy_set_header    X-Forwarded-Proto https;
            }
        }
        ```

    4.  修改默认的配置文件default.conf为default.conf.bak，使Nginx只应用于ghost.conf。

        ```
        mv default.conf default.conf.bak
        ```

    5.  重启Nginx服务。

        ```
        systemctl restart nginx.service
        ```

5.  启动Ghost。

    ```
    cd /var/www/ghost/
    npm start
    ```

6.  访问Ghost博客。

    1.  在浏览器输入http://公网IP或http://域名，访问Ghost。

        ![Ghost网页](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p12480.png)

        **说明：** 如果访问出现502，请检查是否是防火墙的问题，可以关闭防火墙。

    2.  如果需要对博客进行编辑修改，在浏览器输入http://公网IP/ghost。

        ![修改博客](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3412649951/p12481.png)


## 步骤四：购买域名

您可以给自己的网站设定一个单独的域名。这样您的用户可以使用易记的域名访问您的网站，而不需要使用复杂的IP地址。

建议登录阿里云购买域名。详情请参见[注册通用域名](/intl.zh-CN/域名注册/注册通用域名.md)。

## 步骤五：备案

对于域名指向中国内地服务器的网站，必须进行网站备案。在域名获得备案号之前，网站无法开通使用。

阿里云有代备案系统，方便您进行备案。备案免费，审核时间一般为20天左右，请您耐心等待。

## 步骤六：配置域名解析

您需要在阿里云万网上配置域名解析之后，用户才能通过域名访问您的网站。具体操作请参见[设置域名解析](https://www.alibabacloud.com/help/doc-detail/58131.htm)。

