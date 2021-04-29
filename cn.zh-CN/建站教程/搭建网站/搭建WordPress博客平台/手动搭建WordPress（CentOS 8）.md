# 手动搭建WordPress（CentOS 8）

WordPress是使用PHP语言开发的博客平台，在支持PHP和MySQL数据库的服务器上，您可以用WordPress架设自己的网站，也可以用作内容管理系统（CMS）。本教程介绍如何在Linux操作系统的ECS实例上搭建WordPress网站。

-   已注册阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   已创建网络类型为专有网络的安全组，并且安全组的入方向添加规则并放行80端口，如果您使用SSH远程连接Linux实例，需要放行22端口。 若尚未添加规则，请先[添加安全组规则](/cn.zh-CN/安全/安全组/添加安全组规则.md)。
-   已创建Linux操作系统的ECS实例，并且手动部署LNMP环境，详情请参见[手动部署LNMP环境（CentOS 8）](/cn.zh-CN/建站教程/搭建环境/部署LNMP环境/手动部署LNMP环境（CentOS 8）.md)。本教程使用的相关资源版本如下。
    -   实例规格：ecs.c6.large
    -   操作系统：公共镜像CentOS 8.1 64位
    -   Nginx版本：1.16.1
    -   MySQL版本：8.0.17
    -   PHP版本：7.3.5
    -   WordPress版本：5.4.2

**说明：** 当您使用不同软件版本时，可能需要根据实际情况调整命令和参数配置。

本教程适用于熟悉Linux操作系统，刚开始使用阿里云进行WordPress网站搭建的企业或个人用户。您也可以使用云市场提供的WordPress镜像快速搭建WordPress网站。详情请参见[云市场镜像搭建WordPress](/cn.zh-CN/建站教程/搭建网站/搭建WordPress博客平台/云市场镜像搭建WordPress.md)。

## 搭建WordPress网站

1.  通过ECS控制台，远程连接部署好LNMP环境的ECS实例，配置WordPress数据库。

    1.  远程连接ECS实例。

        详情请参见[使用用户名密码验证连接Linux实例](/cn.zh-CN/实例/连接实例/使用第三方客户端工具连接实例/使用用户名密码验证连接Linux实例.md)。

    2.  进入MySQL数据库。

        使用`root`用户登录MySQL，并输入密码。密码为您在搭建环境时为数据库设置的密码。

        ```
        mysql -uroot -p
        ```

    3.  为WordPress网站创建数据库。

        本教程中数据库名为wordpress。

        ```
        create database wordpress;
        ```

    4.  创建一个新用户管理WordPress库，提高安全性。

        MySQL在5.7版本后默认安装了密码强度验证插件validate\_password。您可以登录MySQL后查看密码强度规则。

        ```
        show variables like "%password%";
        ```

        本教程中创建新用户`user`，新用户密码为`PASSword123.`。

        ```
        create user 'user'@'localhost' identified by 'PASSword123.';
        ```

    5.  赋予用户对数据库wordpress的全部权限。

        ```
        grant all privileges on wordpress.* to 'user'@'localhost';
        ```

    6.  使配置生效。

        ```
        flush privileges;
        ```

    7.  退出MySQL。

        ```
        exit;
        ```

2.  下载并解压WordPress，然后移动至网站根目录。

    1.  进入Nginx网站根目录，下载WordPress。

        ```
        cd /usr/share/nginx/html
        wget https://wordpress.org/wordpress-5.4.2.zip
        ```

        **说明：** 下载过慢或失败时，可以尝试运行命令wget http://cn.wp101.net/latest-zh\_CN.zip下载WordPress（`cn.wp101.net`为WordPress简体中文网站，通过该命令下载的WordPress默认为中文版本）。同时您需要注意，后续操作中压缩包的名称必须替换为`latest-zh_CN.zip`。

    2.  解压WordPress压缩包。

        ```
        unzip wordpress-5.4.2.zip
        ```

    3.  将WordPress安装目录下的`wp-config-sample.php`文件复制到`wp-config.php`文件中，并将`wp-config-sample.php`文件作为备份。

        ```
        cd /usr/share/nginx/html/wordpress
        cp wp-config-sample.php wp-config.php
        ```

    4.  编辑`wp-config.php`文件。

        ```
        vim wp-config.php
        ```

    5.  按i键切换至编辑模式，根据配置完成的wordpress数据库信息，修改MySQL相关配置信息，修改代码如下所示。

        WordPress网站的数据信息将通过数据库的`user`用户保存在wordpress库中。

        ```
        // ** MySQL 设置 - 具体信息来自您正在使用的主机 ** //
        /** WordPress数据库的名称 */
        define('DB_NAME', 'wordpress');
        
        /** MySQL数据库用户名 */
        define('DB_USER', 'user');
        
        /** MySQL数据库密码 */
        define('DB_PASSWORD', 'PASSword123.');
        
        /** MySQL主机 */
        define('DB_HOST', 'localhost');
        ```

    6.  修改完成后，按下Esc键后，输入`:wq`并回车，保存退出配置文件。

3.  修改Nginx配置文件。

    1.  运行以下命令打开Nginx配置文件。

        ```
        vi /etc/nginx/conf.d/default.conf
        ```

    2.  按i键进入编辑模式。

        在`location /`大括号内，将`root`后的内容替换为wordpress根目录。本示例中根目录为/usr/share/nginx/html/wordpress。

        ![nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6500430061/p167509.png)

        在`location ~ .php$`大括号内，将`root`后的内容替换为wordpress根目录。

        ![nginx](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6500430061/p167510.png)

        修改完成后按Esc键，输入`:wq`保存并退出配置文件。

    3.  运行以下命令重启Nginx服务。

        ```
        systemctl restart nginx
        ```

4.  安装并登录WordPress网站。

    1.  在本地物理机上使用浏览器访问`ECS实例公网IP`，进入WordPress安装页面。

    2.  填写网站基本信息，然后单击**安装WordPress**。

        填写信息参数说明：

        -   站点标题：WordPress网站的名称。例如：demowp。
        -   用户名：用户登录WordPress时使用的用户名，请注意安全性。例如：testwp。
        -   密码：建议用户设置安全性高的密码。例如：Wp.123456。
        -   您的电子邮件：用于接收通知的电子邮件。例如：1234567890@aliyun.com。
    3.  单击**登录**。

    4.  输入在安装WordPress时设置的用户名`testwp`和密码`Wp.123456`，然后单击**登录**。

        成功进入您个人的WordPress网站。


## 解析WordPress网站域名

通过实例公网IP地址直接访问您的WordPress网站会降低服务端的安全性。如果您已有域名或者想为WordPress网站注册一个域名，可以参考以下步骤。本示例注册域名为`www.WordPress.EcsQuickStart.com`。

1.  注册域名。

    详情请参见[注册通用域名](/cn.zh-CN/域名注册/注册通用域名.md)。

2.  备案。

    如果您的域名指向的网站托管在阿里云中国内地节点服务器，您需要进行备案。如果您是首次备案，请参见[首次备案流程]()，其他情况请参见[ICP备案流程概述]()。

3.  解析域名。将域名指向实例公网IP。

    域名解析是使用域名访问您的网站的必备环节。具体操作流程，请参见[设置域名解析](http://help.aliyun.com/document_detail/29716.html)。

4.  返回ECS控制台，远程连接已搭建WordPress网站的ECS实例，登录MySQL数据库。

    ```
    mysql -uroot -p
    ```

5.  使用wordpress数据库。

    ```
    use wordpress;
    ```

6.  将实例公网IP替换为新域名。

    ```
    update wp_options set option_value = replace(option_value, 'http://实例公网IP', 'http://www.WordPress.EcsQuickStart.com') where option_name = 'home' OR option_name = 'siteurl';
    ```

7.  退出MySQL。

    ```
    exit;
    ```

    成功为WordPress网站设置新域名。


## 常见问题

-   问题描述：WordPress中设置固定链接后，跳转页面无法访问。

    解决方案：网站设置伪静态有利于搜索引擎收录网站。您在对WordPress站点设置固定链接前，需要先在Nginx服务器中设置伪静态规则。操作步骤如下：

    1.  登录搭建WordPress的ECS实例。
    2.  运行以下命令打开Nginx配置文件。

        ```
        vi /etc/nginx/conf.d/default.conf
        ```

    3.  按i键进入编辑模式，在`location /`大括号内，添加如下代码。

        ```
        if (-f $request_filename/index.html){
        rewrite (.*) $1/index.html break;
        }
        if (-f $request_filename/index.php){
        rewrite (.*) $1/index.php;
        }
        if (!-f $request_filename){
        rewrite (.*) /index.php;
        }
        ```

        添加完成后按Esc键，并输入`:wq`并回车，保存退出文件。

    4.  运行以下命令重启Nginx服务。

        ```
        systemctl restart nginx
        ```

-   问题描述：WordPress中更新版本、上传主题或插件时，提示需要FTP登录凭证或无法创建目录。

    解决方案：

    1.  登录搭建WordPress的ECS实例。
    2.  运行以下命令打开WordPress配置文件。

        ```
        vim /usr/share/nginx/html/wordpress/wp-config.php
        ```

    3.  按i键进入编辑模式，在最下方，添加如下代码。

        ```
        define("FS_METHOD","direct");
        define("FS_CHMOD_DIR", 0777);
        define("FS_CHMOD_FILE", 0777);
        ```

        添加完成后按Esc键，并输入`:wq`并回车，保存退出文件。

    4.  返回WordPress仪表盘，刷新页面，可解决需要FTP登录凭证的问题。

        如果仍存在无法创建目录的问题，需再次返回ECS实例，运行以下命令，将网站根目录的权限用户更新为Nginx对应的用户，本示例环境中为`nginx`用户。

        ```
        chown -R nginx /usr/share/nginx/html/wordpress
        ```


